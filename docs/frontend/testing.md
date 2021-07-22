---
id: testing
title: Testing
---

## Cypress

We use the JavaScript Testing Framework [Cypress](https://www.cypress.io/) for End to End testing. So to say a helper robot that behaves like a user to click around the app and verify that it functions correctly. API-calls and the associated data required to test the application are mocked.

### Selecting Elements in Cypress tests

To select DOM-elements for cypress tests we are using `data-cy` attributes to
provide context to the selectors and isolate them from CSS or JS changes. You
can find more information on the
[Best-Practices-Page](https://docs.cypress.io/guides/references/best-practices.html#Selecting-Elements)
in the Cypress Documentation.

### Run the Cypress tests

`npm run test` to run all cypress tests in the terminal without opening a browser.

`npm run dev` to start the frontend process and open the Cypress GUI to manually start specific cypress tests.

In addition, a github action automatically executes the command `npm run test` on every push. This ensures that changes can only be merged when all tests have been run successfully.
