---
title: 'Briefkasten'
date: 2021-03-04
weight: 10
---

📮 Briefkasten is a standalone app used for case reporting. It renders a form from configuration and forwards submitted content to the desired email address.

## Overview

- [Development](/docs/briefkasten#development)
- [Deployment](/docs/briefkasten#deployment)

## Development setup

Briefkasten is a small Ruby app using the [Sinatra](http://sinatrarb.com/) web framework.

Using Ruby 3.0.1 (install it eg via [rbenv](https://github.com/rbenv/rbenv))

There are some libs you need on your system, for Debian-based systems that would be

``` bash
$ sudo apt install libsqlite3-dev sendmail
```
Then install Ruby dependencies.

``` bash
$ bundle install
```
Copy the the `env.sample` file over and adjust the values

``` bash
$ cp env.sample .env
```
source it `$ source .env`

Time to start up the app!

``` bash
$ bundle exec thin start
```
You should see the app at `localhost:3000`.

### Use mailcatcher and SMTP

The default method of sending mail is `sendmail`.

But you can use `mailcatcher` to send emails and debug them in a browser-based email client, too, the gem is already added.

Start `mailcatcher` in a different terminal window with `$ bundle exec mailcatcher` and comment out this line in `app.rb`

`mail.delivery_method :sendmail`

in favor of this line

`mail.delivery_method :smtp, address: "localhost", port: 1025`

and restart thin.

## Deployment
