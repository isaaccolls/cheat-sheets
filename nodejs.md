# node

- version `node -v`
- run single script `node app.js`
- run single function `node -e 'require("./modules/Quiz/quiz_model").reset_weekly_user_coins()'`

# npm

- install npm `npm install -g npm`
- npm version `npm -v`
- new project `npm init` or `yarn init`

## manage

- install all dependencies from package.json `npm install` or `yarn`
- install express: framework to build api rest `npm install express --save` or `yarn add express`
- install bcrypt-nodejs: encrypt passwords `npm install bcrypt-nodejs --save`
- install body-parser: to parsing the response `npm install body-parser --save`
- install connect-multiparty: save files on server with node `npm install connect-multiparty --save`
- install jwt-simple: jwt `npm install jwt-simple --save`
- install moment: library for parsing, validating, manipulating and formatting dates `npm install moment --save`
- install mongoose: work with mongodb `npm install mongoose --save`
- install mongoose-pagination: mongoose query pagination `npm install mongoose-pagination --save`
- install nodemon: automatically restart the node application when file changes in the directory are detected `npm install nodemon --save-dev` or `yarn add [package-name] --dev`
- install specific package version `npm install [package-name]@[version-number]`
- uninstall package `npm uninstall mongoose --save` `yarn remove [package]`
- start project `npm start` or `npm start --host ip` or `yarn start`
- always run nodemon: add scripts on package.json `"start": "nodemon index.js"`
- run script (on package.json) `npm run deploy` or `yarn run deploy`

# nvm

- install nvm `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash`
- version `nvm --version`
- list versions available to install `nvm ls-remote`
- install some node version `nvm install 7.1.0`
- install current LTS version of Node.js.`nvm install --lts`
- list installed node versions `nvm ls`
- select node version to use `nvm use 7.1.0`
- select node version to use **persistent** `nvm alias default [version]`
- check node version `nvm current` or `node --version`
- check npm version `npm --version`
- install yarn `npm install -g yarn`

# eslint, prettier husky and lint-staged

install only the necessary

```bash
yarn add -D eslint\
  eslint-config-airbnb\
  eslint-plugin-import\
  eslint-plugin-jsx-a11y\
  eslint-plugin-react\
  eslint-plugin-react-hooks\
  prettier\
  eslint-config-prettier\
  eslint-plugin-prettier\
  husky\
  lint-staged\
  stylelint\
  stylelint-config-standard
```

## initialize eslint

- run `./node_modules/.bin/eslint --init`
- create `.prettierrc.json`
- run prettier alone `npx prettier --write "**/*.{html,css,scss,css.map,json,md,js,jsx}"`

## initialize husky

`yarn husky init` or `npx husky init`

add to `.husky/pre-commit`: `yarn lint-staged`

## lint-staged config

add to package.json

```json
{
  "lint-staged": {
    "*.{js,jsx}": ["prettier --write", "eslint --fix", "git add"],
    "*.{html,css,scss,json,md}": ["prettier --write", "git add"]
  }
}
```
