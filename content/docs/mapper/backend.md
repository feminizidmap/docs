---
title: Mapper backend
date: 2021-04-14
weight: 4
---

# Backend

The backend is a Rails application that exposes various API endpoints.

## Configuration

## API

## Rake tasks

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
