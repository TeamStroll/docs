# Linters

## What is a Linter?

Linters are programs, which can be commonly run inside of your IDE, whose primary purpose is to aid in your development process by either catching syntax errors, or aiding in the maintainance of coding style.  At Stroll we make use of eslint for our JS and sass-lint for our Scss.

## How do I Install These?

To install eslint:

`npm i -g eslint`

To install sass-lint:

`npm install -g sass-lint`

You will then need to add [`.eslintrc`](./linters/eslintrc) and [`.sass-lint.yml`](./linters/sass-lint.yml) to your dotfiles.

You'll also probably need to install the plugins for these on your IDE.
