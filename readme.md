# Eslint Config V2.2.2
* My personal settings for ESLint ~~and Prettier~~.
* Largely ~~based on~~ lifted from [eslint-config-wesbos](https://github.com/wesbos/eslint-config-wesbos) 😉
  - ~~But with added adjustments for how ESLint and Prettier play together.~~
  - V2.1.0 removes Prettier
## What it does
* Lints JavaScript based on the latest standards
* ~~Fixes issues and formatting errors with Prettier~~
* Lints + Fixes inside of html script tags
* Lints + Fixes React via eslint-config-airbnb
* You can see all the [rules here](https://github.com/matthewatkins/eslint-config-atkins/blob/master/.eslintrc.js)

## Installing

You can use eslint globally and/or locally per project.

It's usually best to install this locally once per project, that way you can have project specific settings as well as sync those settings with others working on your project via git.


## Local / Per Project Install

1. If you don't already have a `package.json` file, create one with `npm init`.

2. Then we need to install everything needed by the config:

```
npx install-peerdeps --dev eslint-config-atkins
```

3. You can see in your package.json there are now a big list of devDependencies.

4. Create a `.eslintrc` file in the root of your project's directory (it should live where package.json does). Your `.eslintrc` file should look like this:
```json
{
  "extends": ["atkins"]
}
```

Tip: You can alternatively put this object in your `package.json` under the property `"eslintConfig":`. This makes one less file in your project.

5. You can add two scripts to your package.json to lint and/or fix:

```json
"scripts": {
  "lint": "eslint .",
  "lint:fix": "eslint . --fix"
},
```

6. Now you can manually lint your code by running `npm run lint` and fix all fixable issues with `npm run lint:fix`. You probably want your editor to do this though.

## Settings

If you'd like to overwrite eslint or prettier settings, you can add the rules in your `.eslintrc` file. The [ESLint rules](https://eslint.org/docs/rules/) go directly under `"rules"`.

```js
{
  "extends": [
    "atkins"
  ],
  "rules": {
    "no-console": 2,
  }
}
```

**NOTE** The following reading is mostly inaccurate now since removing Prettier.

Further ESLint ~~/ Prettier~~ configuration help can be found by reading [this article and following step 1. "Remove conflicting rules and run serially"](https://blog.logrocket.com/automate-formatting-and-fixing-javascript-code-with-prettier-and-eslint/)

## With VS Code

You should read this entire thing. Serious!

Once you have done one, or both, of the above installs. You probably want your editor to lint and fix for you. Here are the instructions for VS Code:

1. Install these VS Code extensions [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint), [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode), and [Format Code Action](https://marketplace.visualstudio.com/items?itemName=rohit-gohri.format-code-action).
2. Now we need to setup some VS Code settings via `Code/File` → `Preferences` → `Settings`. It's easier to enter these settings while editing the `settings.json` file, so click the `{}` icon in the top right corner:
  - NOTE: You can also add these per project by putting them in a `settings.json` file inside of a `.vscode` directory in the root of your project.

  ```js
  // ...
  // first enable formatOnSave
  "editor.formatOnSave": true,
  // then, turn it off for JS and JSX, we will do this via eslint
  "[javascript]": {
    "editor.formatOnSave": false
  },
  "[javascriptreact]": {
    "editor.formatOnSave": false
  },
  // show eslint icon at bottom toolbar
  "eslint.alwaysShowStatus": true,
  // run Prettier then ESLint plugin to run on save
  "editor.codeActionsOnSave": ["source.fixAll.eslint"],
  // ...
  ```

Finally you'll usually need to restart VS code. They say you don't need to, but it's never worked for me until I restart.

## With Create React App

1. Run `npx install-peerdeps --dev eslint-config-atkins`
2. Open your `package.json` and replace `"extends": "react-app"` with `"extends": "atkins"`

## With Gatsby

1. Run `npx install-peerdeps --dev eslint-config-atkins`
2. If you have an existing `.prettierrc` file, delete it.
3. follow the `Local / Per Project Install` steps above

## With Yarn

It should just work, but if they aren't showing up in your package.json, try `npx install-peerdeps --dev eslint-config-atkins -Y`

## IF IT'S NOT WORKING

Start fresh. Sometimes global modules can goof you up. This will remove them all:

```
npm remove eslint-config-atkins babel-eslint eslint eslint-config-prettier eslint-config-airbnb eslint-plugin-html eslint-plugin-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react prettier eslint-plugin-react-hooks
```

Then if you are using a local install, remove your `package-lock.json` file and delete the `node_modules/` directory.

Then follow the above instructions again.
