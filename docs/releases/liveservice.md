---
id: liveservice
title: LiveService
---

## General description

This page describes changes/updates for the LiveService.

Only changes that are necessary to use the requested version are listed in this document.

If you want a changelog please see the [project changelog](https://github.com/CaritasDeutschland/caritas-onlineBeratung-liveservice/blob/master/CHANGELOG.md).

### Unreleased

### 2020-11-03

Update tag to `dockerImage.v.5.release-2020-11-03` in the `.env` file - the following changes are necessary:
 - extend the `docker-compose.yml` for the new service
 - add `LIVE_SERVICE_VERSION` to `.env` file (same directory as the `docker-compose.yml)
 - create a `LiveService` folder in the same directory as the `docker-compose.yml`
 - create a `LiveService.env` in the newly created `LiveService` folder
 - add the NGINX location (see [Backend-Repository](https://github.com/CaritasDeutschland/caritas-onlineBeratung-backend))
 - restart `nginx` and `liveservice `