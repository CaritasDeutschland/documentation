---
id: setup-frontend
title: Setting up the frontend
---

The frontend app for the Caritas Online Beratung has two responsibilities:

1. Be the executable frontend app for the Caritas Online Beratung
2. Provide build tools and app code as a library, so this app can be developed and published in a themed setup

## General setup

**Node.js** is a JavaScript runtime which will allow us to run a host of tools. In fact node.js even runs a tiny webserver which will enable you to browse the components of the frontend.
**NPM** is the Node Package Manager and is used to install all packages.

1. Install as instructed on <http://nodejs.org>.
2. (On Windows if asked) choose to also install NPM and add Node.js to your path.
3. Check the installation of Node.js and NPM by running `node -v` or `npm -v` from your command line.
4. Open your command line / terminal / bash
5. Navigate to the project folder
6. Run `npm install`

> IMPORTANT NOTE ON PERMISSIONS: If you experience permission problems while installing Node.js (especially on Mac or Linux machines), never use `sudo` to install packages with `npm`.
> Please ask your IT Admins to give you proper permissions or let them do the installation. See <https://docs.npmjs.com/getting-started/fixing-npm-permissions> for instructions.

## App setup

For starting the frontend locally you have two options:

- set up the project locally with your local databases etc. and starting it via docker, go on with [Setup local backend](setup-frontend#setup-local-backend)
- set up the project on a (dev) server and start the frontend locally and work against said server, go on with [Starting without local backend](setup-frontend#starting-without-local-backend)

### Setup local backend

To run the application locally you'll need to setup the backend first.

Please follow these steps:

1. [Setup the backend locally](../backend/install-and-running-locally)
2. [Create core data and import users](../backend/create-core-data-import-users)
3. [Start the services](../backend/starting-and-stopping-the-services)

### Starting with local backend

After you're are finished with the setup steps and all services work, run these steps to get your project on the road:

1. Open your command line / terminal / bash
2. Navigate to the project folder
3. Adjust the [CORS configuration](../backend/cors-configuration)
4. Setup your `.env` file according to the `.env.sample`.

- Remove the `API_URL_FOR_LOCAL_DEVELOPMENT` and `CSRF_WHITELIST_HEADER_FOR_LOCAL_DEVELOPMENT` as you won't need it.

5. Afterwards you can start the frontend with `npm start`
6. Adjust the backend setup to use the local frontend. For this you can edit `nginx/conf/locations/common.conf` and modify the line mentioning `proxy_pass` to point to your frontend host, including the port (e.g. `proxy_pass http://caritas.local:9000/;`).
7. [Start the backend](../backend/starting-and-stopping-the-services)
8. The frontend opens at your configured host. To avoid CORS issues during the login, remove the port and login by just using the host.

### Starting without local backend

After you're are finished with the setup steps and all services work, run these steps to get your project on the road:

1. Open your command line / terminal / bash
2. Navigate to the project folder
3. Setup your `.env` file according to the `.env.sample`:

- set `API_URL_FOR_LOCAL_DEVELOPMENT` to the domain you're developing against.
- set `CSRF_WHITELIST_HEADER_FOR_LOCAL_DEVELOPMENT` to the `X-WHITELIST-HEADER` you define in the CORS setup: [CORS configuration for local frontend development](../backend/cors-configuration#cors-settings-for-local-frontend-development)

4. Afterwards you can start the frontend with `npm start`.

### Test

With `npm test` you can run the Cypress end-to-end tests with a mocked backend.

### Build

By running `npm run build`, you can build the app for production. The built assets are copied to the `build` folder.

## Library setup

### Theming and configuration

To use this project as a dependency, you have to:

1. Add an `.npmrc` file with this entry:

```bash
@caritasdeutschland:registry=https://npm.pkg.github.com/
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}
```

2. [Configure a `GITHUB_TOKEN` environment parameter](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) in the shell (ideally loaded on startup)

Then you can install the library with `npm install @caritasdeutschland/caritas-online-beratung-frontend`.

Afterwards you should fork these files from [the frontend repository](https://github.com/CaritasDeutschland/caritas-onlineBeratung-frontend) into the consuming repository:

```
src
  pages
    app.html
    under-construction.html
  resources
    scripts
      i18n
        defaultLocale.ts
        informalLocale.ts
      config.ts
    styles
      settings.scss
  initApp.tsx
  initError.tsx
  initLogin.tsx
```

They can be used to provide the necessary configuration and theming to the consuming app.

In `settings.scss` you should replace the file content with `@import '~@caritasdeutschland/caritas-online-beratung-frontend/defaults';` to use the current defaults and only override what's necessary. By defining a `setup-fonts` mixin, you can import custom fonts from the stylesheet.

Furthermore in `defaultLocale.ts` you should `import {defaultLocale as defaults} from '@caritasdeutschland/caritas-online-beratung-frontend';` and only override the labels that need to be changed. The same applies analogously to `informalLocale`.

### CLI scripts

Additionally, these scripts are available:

```sh
# Run the dev server
@caritasdeutschland/caritas-online-beratung-frontend start

# Build the app for production
@caritasdeutschland/caritas-online-beratung-frontend build
```
