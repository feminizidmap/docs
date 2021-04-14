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
