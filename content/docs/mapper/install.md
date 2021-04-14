---
title: Mapper development
date: 2021-04-14
weight: 2
---

# Development setup

## Frontend

The frontend is a standard [Vue.JS](https://v3.vuejs.org/) application, you need [NodeJS](https://nodejs.org/en/download/) installed to run the development environment and build the final app.

### Dependencies

I'll be using [yarn](https://classic.yarnpkg.com/en/docs/install/) as package manager and task runner in this guide, but npm is also fine.

### Environment variables

Edit the `.env.development` file, most importantly update the `VUE_APP_API_URL` if you make changes. If you're running the backend service in the default settings, then there is nothing to be done here.

### Development server

Inside `frontend` run `$ yarn install` to install dependencies,

then run `$ yarn serve` to start the development server on `localhost:8080` with hot-reload.


### Misc

Other commands are:

- `yarn build` to build the final app in the `dist` folder
- `yarn lint` to run the linter
- `yarn test:unit` to run unit tests


## Backend

The backend is a standard Rails application talking to a Postgres database and an attached Redis store.

### Dependencies

You need [Postgres](https://www.postgresql.org/download/) and [Redis](https://redis.io/download) and the right [Ruby version](https://github.com/feminizidmap/feminizid-mapper/blob/main/backend/.ruby-version) installed. Start both in the background and have your Postgres user credentials ready.

For easy Ruby version installation and management I recommend [rbenv](https://github.com/rbenv/rbenv) but rvm or chruby are also fine.

Inside `backend` run `$ bundle install` to install dependencies.

### Environment variables

Run `$ cp env.sample .env` to create a working copy for your local settings.

Edit the `DATABASE_URL` and `DATABASE_TEST_URL` with the credentials for your local Postgres user and database and `REDIS_URL` with, you guessed it, the Redis url.

To set a `SESSION_SECRET` for JWT, run `$ bin/rake secret` and copy the output in the `.env` file.

In default configuration the rest can stay the same.

### Development server

Finally you can start the server with `$ rails s`, with should start on `localhost:3000`.
