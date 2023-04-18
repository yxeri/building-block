# building-block

This is a barebones Next project with volta, eslint (using airbnbs ruleset), husky and commitlint (using conventional commits ruleset) pre-configured.

## Requirements[](https://)

Install Volta ([https://volta.sh](https://volta.sh)) with `curl https://get.volta.sh | bash`

## What's included

- [Next.js](https://nextjs.org) - React Framework[](https://)
- [Airbnb Eslint config](https://www.npmjs.com/package/eslint-config-airbnb) - A pre-configured set of rules for Eslint
- [Airbnb Typescript Eslint config](https://www.npmjs.com/package/eslint-config-airbnb-typescript) - A pre-configured set of rules for Eslint that covers Typescript
- [Eslint Prettier config](https://github.com/prettier/eslint-config-prettier) - A pre-configured set of rules for Eslint that disabled some formatting rules to avoid collisions when using Prettier together with Eslint
- [Husky](https://typicode.github.io/husky/#/) - Allows running commands on [Git hooks](https://git-scm.com/docs/githooks), such as `pre-commit` and `commit-msg`
- [commitlint](https://commitlint.js.org/#/) - Linter for commit messages (following the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) standard in this project)
- [lint-staged](https://github.com/okonet/lint-staged) - Allows linting to be done only on staged files

## How this project was set up

1. `yarn create next-app --typescript` to install Ne[](https://)xt.js
2. `volta pin node@19.4` to add a specific version of Node in package.json, which Volta can use to decide which version to run in the project directory
3. `volta pin yarn@1.22.19` to add a specific version of Yarn in package.json, which Volta can use to decide which version to run in the project directory
4. `volta install node` to install the specific version of Node.
5. `volta install yarn` to install the specific version of Yarn.
6. `npx install-peerdeps --dev eslint-config-airbnb ` to install Airbnb eslint config
7. `yarn add -D eslint-config-airbnb-typescript @typescript-eslint/eslint-plugin
@typescript-eslint/parser` to install Airbnb TS eslint config
8. `yarn add -D prettier eslint-config-prettier ` to install Prettier and Prettier config for eslint
9. `yarn add -D lint-staged` to install lint-staged
10. `npx husky-init && yarn   ` to install husky
11. `yarn add -D @commitlint/cli @commitlint/config-conventional  ` to install commitlint
12. `echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js` to create the config file for commitlint
13. `yarn husky add .husky/commit-msg  'yarn commitlint --edit ${1}'` to add linting on commit messages in Husky
14. `yarn husky add .husky/pre-push 'yarn build'` to add a check that building the project works before trying to push new code to the repo
15. Edit .husky/pre-commit and add `yarn lint-staged`, replacing the existing command (usually `npm test`)
16. .eslintrc.json in root:

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

13. .prettierrc.json in root:

```
{
  "trailingComma": "all",
  "tabWidth": 2,
  "semi": true,
  "singleQuote": true
}
```

14. .lintstagedrc.json in root:

```
{
  "*.{js,jsx,ts,tsx,md,html,css}": "prettier --write",
  "*.{js,jsx,ts,tsx}": "eslint --fix"
}
```

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

## Making the project ready to run

1. Run `volta install node`. It will install/use the version of node that is pinned to this project (see package.json "volta"). The specific node version was pinned with `volta pin node@19.4`
2. Run `volta install yarn`
3. Run `yarn install`
4. Success!
