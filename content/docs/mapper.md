---
title: 'Mapper'
date: 2021-03-04
weight: 2
---

🗃️ Mapper is the main database interface app. It contains the user management, data entry and organisation and exposes a REST API.


## Overview

### Backend

The backend is a Rails application that exposes various API endpoints.

#### Rake tasks

There are two sets of code lists prepared that you can easily import to get started. They are available in their respective original language.

The feminizidmap.org code lists are in German, to import the full set run:

``` bash
$ rails codelists:feminizidmap:add_default
```

The [femicidios-latam code lists](https://github.com/idatosabiertos/femicidios-latam/tree/master/standard/schema/codelists) are in Spanish, to import the full set run:

``` bash
$ rails codelists:femicidio_latam:add_default
```

To see all available subtasks run `rails --tasks`.


### Frontend

The frontend is a VueJS application.

## Development setup

## Deployment setup

### Heroku

You can run mapper on Heroku's 'hobby' infrastructure. You need two heroku apps, one for the backend and one for the frontend. Attach a postgres and redis addon to the backend app.
Add the required environment variables to each and you're done. See the github/deploy workflow for reference.

@todo add individual steps for Heroku setup and deployment
