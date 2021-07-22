---
id: tools-and-technologies
title: Tools and Technologies
---

## Prettier

We use [Prettier](https://prettier.io/) to format all files inside the `src`
directory. This is done on every commit and on every pull request using github
actions. The exact Prettier configuration can be found in the `package.json`
file in the root directory of the frontend repository.

## ESLint

We use [ESLint](https://eslint.org/) to identify problematic patterns found in
JavaScript and Typescript code. We have extended the recommended ESlint and
React rules with some further rules which can be found in the `package.json`
file in the root directory of the frontend repository.

The linter is executed on every pull request using github actions. This will
highlight potential errors that need to be adjusted before a merge to the target
branch is allowed.

## Typescript

We use [Typescript](https://www.typescriptlang.org/) to add static types to our
JavaScript code. The precise defining through typing makes code management
easier, increases the readability and helps us to spot bugs early.
