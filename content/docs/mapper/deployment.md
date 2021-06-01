---
title: Mapper deployment
date: 2021-04-14
weight: 3
---

# Deployment setup

## Heroku

You can run mapper on Heroku's 'hobby' infrastructure. You need two heroku apps, one for the backend and one for the frontend. Attach a postgres and redis addon to the backend app.
Add the required environment variables to each and you're done. See the github/deploy workflow for reference.

@todo add individual steps for Heroku setup and deployment

## Docker

Copy the toplevel `env.sample` to `.env` and adjust the values. Unfortunately you also have to copy the `fontent/env.production.sample` to `frontend/.env.production`, too, as its build process runs before docker injects the env variables from the toplevel. Oh well. VUE_APP_API_URL is the BACKEND_URL.

Look into `docker-compose.yml` and adjust url paths as well (most likely FRONTEND_URL and BACKEND_URL).

Run `docker-compose up -d` to start the containers.

Add DNS records for frontend and backend services (should be what you put in FRONTEND_URL and BACKEND_URL).

If you use NGINX as webserver add a config similar to this one:

(Using the domains frontend.mapper.org and backend.mapper.org as placeholder names here, use your FRONTEND_URL and BACKEND_URL. Same for the ports (8080 for frontend, 300 for backend. Adjust accordingly!)

```
server {
    listen 80;
    listen [::]:80;
    server_name frontend.mapper.org;

    location / {
        return 301 https://$server_name$request_uri;
    }

    location /.well-known {
        root /var/www/mapper;
    }
}

server {
    listen 80;
    listen [::]:80;
    server_name backend.mapper.org;

    location / {
        return 301 https://$server_name$request_uri;
    }

    location /.well-known {
        root /var/www/mapper;
    }
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name backend.mapper.org;

    ssl on;
    ssl_certificate /etc/letsencrypt/live/frontend.mapper.org/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/frontend.mapper.org/privkey.pem;
    #include /etc/nginx/ssl.conf;

    client_max_body_size 10G;

    location / {
        proxy_set_header X-Scheme $scheme;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        add_header Strict-Transport-Security "max-age=15552000; includeSubDomains" always;
        proxy_pass http://localhost:3000;
    }
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name frontend.mapper.org;

    ssl on;
    ssl_certificate /etc/letsencrypt/live/frontend.mapper.org/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/frontend.mapper.org/privkey.pem;

    client_max_body_size 10G;

    gzip on;
    gzip_proxied any;
    proxy_http_version 1.1;

    location / {
        proxy_pass http://localhost:8080;
        proxy_redirect off;
        proxy_set_header X-Scheme $scheme;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        add_header Strict-Transport-Security "max-age=15552000; includeSubDomains" always;
    }
}

```

Don't forget to add certificates, too! (Using certbot and assuming the main domain to be `frontend.mapper.org` in the example here)

With DNS, certs, webserver configured and running and docker services started, you should now see your app!
