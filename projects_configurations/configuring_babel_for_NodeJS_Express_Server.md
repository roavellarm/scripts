# Configuring babel for Node.js/Express Server

ECMAScript is a Javascript Standardization which gets updated every year, it is
a good practice to update our code as well. ES6 Features.

Sometimes, the browser doesn't compatible with the latest javascript standards.

To solve this kind of problem, we need something like a babel which is nothing
but a transpiler for javascript.

### Babel Setup

Firstly, we need to install two main packages to setup babel in the project.

- **babel-core** - babel-core is the main package to run any babel setup or
  configuration
- **babel-node** - babel-node is the package used to transpile from ES(Any
  Standard) to plain javascript.
- **babel-preset-env** - this package is used to make use of upcoming features
  which node.js couldn't understand. Like, some feature will be new and take
  time to implement in the node.js by default.

### Best Practice

Mainly, the reason for using the babel is to make use of Javascript new features
in the codebase. We don't know whether the node.js in the server will
understand the particular code or not unless it is a vanilla javascript.

So, it is always recommended to transpile the code before
deployment. There are
two kinds of babel transpiling code.

- One is for Production
- One is for Development

## Development Setup

```BASH
$ yarn init --y
$ yarn add --save express body-parser cors
$ yarn add --save nodemon
```

Here, we initialize the `package.json` and install the basic express server with
nodemon.

Next, we need to install `@babel/core` and `@babel/node` packages.

```BASH
$ npm install @babel/core @babel/node --save-dev
```

After that, we need to create a file called `.babelrc` which contains all the
babel configuration.

```JSON
{
  "presets": [
    "@babel/preset-env"
  ]
}
```

Now, the setup is ready. We need to create a script which transpile our code on
run time.

```JSON
"scripts": {
  "dev": "nodemon --exec babel-node index.js"
}
```

Finally, add the following code in the `index.js` and run the script.

```JS
import express from 'express'
import bodyParser from 'body-parser'

const app = express()

app.use(bodyParser.json())

app.get('/',(req, res) => res.send("Hello Babel"))

app.listen(4000,() => console.log(`app is listening to port 4000`))
```

```BASH
$ npm run dev
```

Finally, you will see the output like **_Hello Babel_**.

## Production Setup

Mainly, we cannot transpile the code in run time in production. So, what we need
to do is, to compile the code into vanilla javascript and deploy the compiled
version to the node.js production server.

Add the following command for building a compiled version of code:

```JSON
"scripts": {
  "build" : "babel index.js --out-file index-compiled.js",
  "dev": "nodemon --exec babel-node index.js"
}
```

Babel compiles the `index.js` file and writes the compiled version in
index-compiled.js

Meanwhile, when you run the command, you will get the compiled version like

Finally, we need to deploy the compiled version in the node.js production
server.
