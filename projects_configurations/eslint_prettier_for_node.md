This article will help you install and configure `prettier` and `eslint` correctly. The configurations will be set to follow the common programming good practices and code styles, for example the `Airbnb`.

Some steps here were taken from [this article](https://dev.to/collabcode/como-configurar-eslint-e-prettier-no-node-3kga).

Do the following steps from your node project directory:

### 1) Install `eslint`, `prettier` and other packeges (needed to make eslint to work correctly with prettier) in devDependencies.

```bash
$ yarn add -D eslint prettier eslint-config-prettier eslint-plugin-prettier --save
```

- Create `.eslintrc` by running:

```bash
$ ./node_modules/.bin/eslint --init
```

You will prompt with some questions. Answer them as follow:

01: _How would you like to use ESLint? (Use arrow keys)_

- Answer: _`To check syntax, find problems, and enforce code style`_

02: _What type of modules does your project use?_

- Answer: _`JavaScript modules (import/export)`_

03: _Which framework does your project use?_

- Answer: _`None of these`_

04: _Does your project use TypeScript?_

- Answer: Write `N` and press `ENTER`

05: _Where does your code run?_

- Answer: Press `i` to invert selection and let only the `Node` option selected.

06: _How would you like to define a style for your project?_

- Answer: _`Use a popular style guide`_

07: _Which style guide do you want to follow?_

- Answer: Select _`Airbnb`_ (https://github.com/airbnb/javascript)

08: _What format do you want your config file to be in?_

- Answer: _`JSON`_

09: _Would you like to install them now with npm?_

- Answer: _`Y`_

From now on you have your ESLint configuration file created (`.eslintrc`).

### 2) Configure the `.eslintrc` file located in the root directory of the project as follow:

```JSON
{
  "env": {
    "es6": true,
    "node": true
  },
  "extends": ["airbnb-base", "prettier"],
  "plugins": ["prettier"],
  "globals": {
    "Atomics": "readonly",
    "SharedArrayBuffer": "readonly"
  },
  "parserOptions": {
    "ecmaVersion": 2018,
    "sourceType": "module"
  },
  "rules": {
    "prettier/prettier": "error"
  }
}
```

- Configure the `.prettierrc` file as follow:

```JSON
{
  "tabWidth": 2,
  "singleQuote": true,
  "semi": false,
  "trailingComma": "es5"
}
```

- Add the lint execution command to `scripts` in `package.json` file:

```JSON
{
  "scripts": {
    "lint": "eslint --ext .js --ignore-path .gitignore .",
  }
}
```


- Make sure you vscode json settings file has the format on save on, like this:

```JSON
{
  "editor.formatOnSave": true,
}
```

## OPTIONAL

### Install husky to check linter on pre-commits

```bash
yarn add -D husky@latest --save
```

Paste this to the `package.json`:

```JSON
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "post-commit": "git update-index --again"
    }
  },
  "lint-staged": {
    "*.{js,jsx}": [
      "pretty-quick --staged",
      "git add"
    ],
    "*.js": [
      "eslint",
      "git add",
      "jest --bail --findRelatedTests"
    ]
  }
```

- Add precommit command to `scripts` in `package.json` file:

```JSON
{
  "scripts": {
    "precommit": "lint-staged"
  }
}
```
