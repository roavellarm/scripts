This article will help you install and configure `prettier` and `eslint` correctly for **React-Native** projects. The configurations will be set to follow the common programming good practices and code styles (`Airbnb`).

Do the following steps from your project directory:

### 1) Install `eslint`, `prettier` and other packeges (needed to make eslint to work correctly with prettier) in devDependencies.

```bash
$ yarn add -D eslint@^7.2.0 prettier@latest eslint-config-prettier@latest eslint-plugin-prettier@latest eslint-plugin-react@^7.20.0 eslint-config-airbnb@latest eslint-plugin-import@^2.21.2 eslint-plugin-jsx-a11y@^6.3.0 eslint-plugin-react-hooks@^4 --save &&  ./node_modules/.bin/eslint --init
```

You will be prompted with some questions. Answer them as follow:

01: _How would you like to use ESLint? (Use arrow keys)_

- Answer: _`To check syntax, find problems, and enforce code style`_

02: _What type of modules does your project use?_

- Answer: _`JavaScript modules (import/export)`_

03: _Which framework does your project use?_

- Answer: _`React`_

04: _Does your project use TypeScript?_

- Answer: Write `N` and press `ENTER`

05: _Where does your code run?_

- Answer: `Browser`.

06: _How would you like to define a style for your project?_

- Answer: _`Use a popular style guide`_

07: _Which style guide do you want to follow?_

- Answer: Select _`Airbnb`_ (https://github.com/airbnb/javascript)

08: _What format do you want your config file to be in?_

- Answer: _`JSON`_

09: _Would you like to install them now with npm?_

- Answer: _`N`_

From now on you have your ESLint configuration file created (`.eslintrc`).

### 2) Configure the `.eslintrc` file located in the root directory of the project as follow:

```JSON
{
  "env": { "browser": true, "es2020": true },
  "extends": ["plugin:react/recommended", "airbnb", "prettier"],
  "parserOptions": {
    "ecmaFeatures": { "jsx": true },
    "ecmaVersion": 11,
    "sourceType": "module"
  },
  "plugins": ["react", "prettier", "react-hooks"],
  "rules": {
    "prettier/prettier": "error",
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
    "react/jsx-props-no-spreading": "off",
    "no-underscore-dangle": "off",
    "import/no-named-as-default": "off",
    "import/no-named-as-default-member": "off",
    "import/prefer-default-export": "off",
    "jsx-a11y/no-static-element-interactions": "off",
    "react/no-array-index-key": "off",
    "react/style-prop-object": "off",
    "react/jsx-filename-extension": ["error", { "extensions": [".js", ".jsx"] }]
  },
  "settings": {
    "import/resolver": {
      "node": { "moduleDirectory": ["node_modules", "src/"] }
    }
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
