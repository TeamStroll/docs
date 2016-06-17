# NPM

# Adding New Modules to NPM

For modules need in all environments run: `npm i [package name] --save` (`i` is an alias for `install`).  The `--save` functions to save this change to your package.json file so your colleagues only have to run `npm i` to build the dev environment.

For dev only modules, run: `npm i [package name] --save-dev`

To remove a module, run: `npm r [package name] --save`
