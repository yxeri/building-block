# building-block

This is a barebones Next project with volta, eslint (using airbnbs ruleset), husky and commitlint (using conventional commits ruleset) pre-configured.

## Requirements[](https://)

Install Volta ([https://volta.sh](https://volta.sh)) with `curl https://get.volta.sh | bash`

## Installation

1. Run `volta install node`. It will install/use the version of node that is pinned to this project (see package.json "volta"). The specific node version was pinned with `volta pin node@19.4`
2. Run `yarn install`
3. Success!

## What's included

- [Next.js](https://nextjs.org) - React Framework[](https://)
- [Airbnb Eslint config](https://www.npmjs.com/package/eslint-config-airbnb) - A pre-configured set of rules for Eslint
- [Airbnb Typescript Eslint config](https://www.npmjs.com/package/eslint-config-airbnb-typescript) - A pre-configured set of rules for Eslint that covers Typescript
- [Eslint Prettier config](https://github.com/prettier/eslint-config-prettier) - A pre-configured set of rules for Eslint that disabled some formatting rules to avoid collisions when using Prettier together with Eslint
- [Husky](https://typicode.github.io/husky/#/) - Allows running commands on [Git hooks](https://git-scm.com/docs/githooks), such as `pre-commit` and `commit-msg`
- [commitlint](https://commitlint.js.org/#/) - Linter for commit messages (following the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) standard in this project)

## Configuring your IDE

### Webstorm

1. Settings > Tools > Actions On Save > Check eslint and Prettier

### Visual Studio Code

1. Install [Prettier - Code formatter plugin](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
   1. Settings > Editor: Format On Save > Check
2. Install [Eslint plugin](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
   1. Workspace settings > Code Actions On Save > settings.json
   2. Add:

```
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "eslint.validate": ["javascript"]
 }
```

## How this project was set up

1. `yarn create next-app --typescript` to install Next.js
2. `volta pin node@19.4` to add a specific version of Node in package.json, which Volta can use to decide which version to run in the project directory
3. `npx install-peerdeps --dev eslint-config-airbnb ` to install Airbnb eslint config
4. `yarn add -D eslint-config-airbnb-typescript typescript-eslint/eslint-plugin@^5.13.0 @typescript-eslint/parser@^5.0.0` to install Airbnb TS eslint config
5. `yarn add -D prettier eslint-config-prettier ` to install Prettier and Prettier config for eslint
6. `npx husky-init && yarn   ` to install husky
7. `yarn add -D @commitlint/cli @commitlint/config-conventional  ` to install commitlint
8. `echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js` to create the config file for commitlint
9. `npx husky add .husky/commit-msg  'npx --no -- commitlint --edit ${1}'` to add linting on commit messages in Husky
10. Edit .husky/pre-commit and add `npx next lint`, replacing the existing command (usually `npm test`)
11. .eslintrc.json in root:

```
{
  "extends": [
    "airbnb",
    "airbnb-typescript",
    "prettier"
  ],
  "parserOptions": {
    "project": "./tsconfig.json"
  },
  "rules": {
    "react/prop-types": 0,
    "react/jsx-props-no-spreading": 0,
    "react/function-component-definition": 0,
    "import/prefer-default-export": 0,
    "react/react-in-jsx-scope": 0,
    "react/require-default-props": 0
  },
  "ignorePatterns": ["*.config.js"]
}
```

9. .prettierrc.json in root:

```
{
  "trailingComma": "all",
  "tabWidth": 2,
  "semi": true,
  "singleQuote": true
}

```
