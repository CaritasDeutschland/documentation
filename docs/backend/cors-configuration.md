---
id: cors-configuration
title: CORS configuration
---
## CORS settings for local frontend development
To be able to develop locally (Node server running locally) you have to enable CORS for multiple components:

1. Nginx: Set the allowed origin to your local domain or `*` in `./nginx/conf/cors.conf`.
2. LiveService: Set the `app.base.url` to your local domain or `*` in `./LiveService/LiveService.env`.
3. UserService, MessageService, UploadService: In the corresponding service settings, e.g. 
   `./UserService/UserService.env` add or set the following environment variable: 
   `CSRF_WHITELIST_HEADER_PROPERTY=`. The value of that variable must be send as an http header 
   with a random value from the client for development. e.g: 
   `CSRF_WHITELIST_HEADER_PROPERTY=X-WHITELIST-HEADER` then you need to send a header with the key 
   `X-WHITELIST-HEADER` and a random value.

It could also be necessary to install a CORS plugin in your browser to make CORS work correctly.

## CORS settings for production
The CORS settings on the production server need to be more strict:

1. Nginx: Set the allowed origin only to your productive domain in `./nginx/conf/cors.conf`.
2. LiveService: Set the `app.base.url` only to your productive domain in `./LiveService/LiveService.env`.
3. UserService, MessageService, UploadService: In the corresponding service settings, e.g.
   `./UserService/UserService.env` make sure that the following environment variable is not set:
   `CSRF_WHITELIST_HEADER_PROPERTY=`.
