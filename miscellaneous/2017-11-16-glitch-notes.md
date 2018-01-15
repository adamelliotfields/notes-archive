# Glitch Notes
> Notes on using Glitch.me

Glitch is a code sandbox/playground for both client-side and server-side code. Each Glitch project
is an AWS EC2 instance running a custom Ubuntu distribution.


### Watch Configuration

By default, Glitch will run `npm install` and `npm run start` everytime a file changes. You have
limited control over this by modifying a `watch.json` file in the project root.

The following configuration will only run `npm install` if the `package.json` is changed; and
`npm run start` if any `.js` or `.env` files change outside of the `build` folder.

The throttle property sets a delay for how long to wait before installing/restarting.

**`watch.json`**

```json
{
  "throttle": 10000,
  "install": {
    "include": [
      "^package\\.json$"
    ]
  },
  "restart": {
    "exclude": [
      "^.next/"
    ],
    "include": [
      "^\\.env$",
      "\\.js$"
    ]
  }
}
```


### `package.json`

Every `package.json` must have an `engines` object and a `start` script. As you add dependencies,
Glitch will install them.

**`package.json`**

```json
{
  "private": true,
  "name": "adamelliotfields-next-demo",
  "version": "1.0.0",
  "description": " ",
  "author": "Adam Fields (https://adamelliotfields.github.io)",
  "homepage": "https://adamelliotfields-next-demo.glitch.me",
  "repository": "github:adamelliotfields/next-demo",
  "license": "MIT",
  "main": "index.js",
  "engines": {
    "node": "9.x"
  },
  "dependencies": {
    "cors": "^2.8.4",
    "express": "^4.16.2",
    "isomorphic-unfetch": "2.0.0",
    "next": "^4.1.4",
    "react": "^16.1.1",
    "react-dom": "^16.1.1"
  },
  "scripts": {
    "start": "next build && node ."
  }
}
```


### `.env`

Any environmental variables need to be stored in the `.env` file in the project root. Other users
will be able to see the file, but not your values, so it can be used for keys, secrets, and tokens.

**`.env`**

```
PORT=3000
NODE_ENV=production
```


### `.data`

Any files you dont want exposed publicly can be stored in the `.data` folder. This could be a
SQLite or NeDB database file.


### Port

Glitch gives your app a `process.env.PORT` of `3000` by default, although you can change it. It
really doesn't matter since your app will be accessible to the web at port `80`.


### CORS

In order to use your API outside of the glitch.me domain, you'll need to enable CORS.

**`index.js`**

```javascript
const Express = require('express');
const cors = require('cors');

const app = Express();

app.use(cors({
  origin: '*',
  methods: ['GET'],
  allowedHeaders: ['Origin', 'X-Requested-With', 'Content-Type', 'Accept'],
  preflightContinue: false,
  optionsSuccessStatus: 204
}));

app.listen(process.env.PORT);
```


### GitHub

1. Open the console
2. Run `rm -rf .git` to delete the existing Git folder
3. Run `git init`
4. Run `git remote add origin https://github.com/username/repository.git`

You may need to adjust your `watch.json` to ensure the project is installed, built, and started on a
`git pull`.
