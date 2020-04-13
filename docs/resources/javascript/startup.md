# JavaScript Project Startup

## Basic setup
* *.editorconfig*
```ini
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

* Setup git repository
* `touch .gitignore`
* `git init`
* *.gitignore*
```ini
node_modules
dist
.vscode/
.idea/
```

## NPM Setup
1. `npm init -f` - create *package.json*

1. Setup *eslint*
    * `./node_modules/.bin/eslint --init`
    * *Use a popular style guide*
    * *Standard*
    * *JSON*

1. Setup *tslint*
    * `./node_modules/.bin/tslint --init`

1. Setup *tsconfig.json*
    * `./node_modules/.bin/tsc --init`

## Npm Scripts
```json
  "scripts": {
    "start": "npm-run-all -n -p dev:server",
    "dev": "npm-run-all -n -p dev:server lint:watch",
    "dev:server": "cross-env webpack-dev-server --history-api-fallback --color --progress --hot --inline",
    "build": "npm-run-all -s build:webpack",
    "build:webpack": "cross-env NODE_ENV=production webpack --progress --hide-modules",
    "lint": "esw webpack.config.* src --color",
    "lint:watch": "npm run lint -- --watch",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```
