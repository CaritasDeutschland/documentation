---
id: starting-and-stopping-the-services
title: Starting and stopping the services
---

## Set master keys
After the start of Message-, User- and UploadService one has to provide the
master key for message encryption to the services.
If you want to do it manually, you need to call the [REST API
endpoints](../backend/login-data-access-links.md) to set the master key with
the technical (Keycloak) user and correct CSRF header and cookie key value
pairs. In the body you should provide the key, e.g.:

__Note: The master key for UserService, UploadService and MessageService must be the same__!

``{
	"masterKey": "<masterKey>"
}``

* MessageService: POST on https://<host>/service/messages/key
* UploadService: POST on https://<host>/service/uploads/messages/key
* UserService: POST on https://<host>/service/users/messages/key

Alternatively, you can use the provided start scripts:
Open the file `masterkey.js` and make sure the `postData` and `options` are
correct. The master key itself needs to be set as the `MASTERKEY` environment
parameter in `.env`.

## Starting all services
Start all services by running `npm start` in the base folder of your backend
(where `docker-compose.yml` is located). This makes sure that the services are
started in the correct order and sets the master keys.
If you experience timeouts while
trying to set the master keys please check that the services are able to reach
Keycloak (and vice versa) in your firewall settings.

## Stopping all services
Stop all services by running `npm run down` or `docker-compose down` in the base
folder of your backend (where `docker-compose.yml` is located).

## Troubleshooting
* Start all services by running `docker-compose up` (without *-d*). All log outputs of the single components will then be printed to console.
* Alternatively you can inspect the logs of a specific container by calling `docker logs <container name>`
