# NPM Packages
> :calendar: *April 30, 2017*

This is a running list of NPM packages worth remembering, more so as a reference for myself, but you may find some gems in here as well. Not really *gems* though because this isn't Ruby.  

For a more definitive list, check out Sindre Sorhus' [Awesome NPM](https://github.com/sindresorhus/awesome-npm) and [Awesome Node](https://github.com/sindresorhus/awesome-nodejs).  

Packages in **bold** are global packages I install with every fresh install of Node.  

[axios](https://www.npmjs.com/package/axios)  
Promise-based HTTP client for the browser and Node. Use this to make AJAX calls in your React apps.  

[baconjs](https://www.npmjs.com/package/baconjs)  
Functional programming library for working with streams.  

[bluebird](https://www.npmjs.com/package/bluebird)  
JavaScript Promise library. Useful when developing apps for versions of Node that don't support native ES2015 promises.  

[boxen](https://www.npmjs.com/package/boxen)  
Create boxes in the command line.  

[browserify](https://www.npmjs.com/package/browserify)  
Use NPM packages in your front-end code. Simply use the `require()` function like you would in Node, and Browserify will bundle everything up together.  

**[browser-sync](https://www.npmjs.com/package/browser-sync)**  
Browser Sync creates a dev server synced across all connected devices. When developing an app, I'll also test it on my iPhone and iPad, and Browser Sync syncronizes user inputs across all devices (i.e., clicking a button my desktop also clicks the button my mobile devices). Browser Sync is also useful for running an HTTPS server (without needing certificates) and also circumventing the CORS limitation of some APIs (using the `--https` and `--cors` flags).  

[camo](https://github.com/scottwrobinson/camo)  
ODM for MongoDB and NeDB using ES2015 classes and promises.  

[co](https://github.com/tj/co)  
Control flow for promises using generators and `yield`.  

[cheerio](https://www.npmjs.com/package/cheerio)  
Takes a blob of HTML, which can be the body of a HTTP GET request, and allows you to traverse and manipulate it using jQuery syntax.  

**[create-react-app](https://www.npmjs.com/package/create-react-app)**  
Create React App is a tool developed by Facebook engineer and React guru [Dan Abramov](https://twitter.com/dan_abramov). It initializes your project by creating all the necessary files and folders you need to start coding right away. To run the app on a dev server, simply run `yarn start`. To transpile and bundle your JavaScript for production, run `yarn build`.  

[create-react-native-app](https://www.npmjs.com/package/create-react-native-app)  
`create-react-app` for mobile apps.  

[concurrently](https://www.npmjs.com/package/concurrently)  
Run multiple NPM script commands in parallel using `concurrently "command 1" "command 2"` instead of `command 1 & command 2`. You can also pass the `--kill-others` flag to kill all processes if one failed.  

**[david](https://www.npmjs.com/package/david)**  
An improved `npm outdated`.  

**[download-cli](https://www.npmjs.com/package/download-cli)**  
Downloads and extracts a file. Also has an API for incorporating into your apps.  

[dust](https://www.npmjs.com/package/dust)  
Asynchronous templates for Node and the browser. Developed at LinkedIn.  

[enquirer](https://www.npmjs.com/package/enquirer)  
Create intuitive command line prompts in your app.  

**[eslint](https://www.npmjs.com/package/eslint)**  
Lint your JavaScript using defined rules. Can be extended using plugins.  

[express](https://www.npmjs.com/package/express)  
The most popular web framework for Node.js.  

[express-generator](https://www.npmjs.com/package/express-generator)  
Generate initial folder structure and starter files for an Express app.  

[faker](https://www.npmjs.com/package/faker)  
Generate fake user data for your apps.  

[fs-extra](https://www.npmjs.com/package/fs-extra)  
A drop-in replacement for Node's native fs module. Includes additional methods so you don't need to use libraries like `mkdirp`.  

[generate-github-markdown-css](https://www.npmjs.com/package/generate-github-markdown-css)  
Gets the CSS that GitHub uses to display Markdown files and generates a stylesheet. If you want a pre-made stylesheet, download [github-markdown-css](https://www.npmjs.com/package/github-markdown-css).  

[getstorybook](https://www.npmjs.com/package/getstorybook)  
React Storybook is a UI component testing environment that isolates each individual component (i.e., see the various states of a button).   

[gh-got](https://www.npmjs.com/package/gh-got)  
GitHub API client.  

[ghost](https://www.npmjs.com/package/ghost)  
Blogging platform for Node.  

[got](https://www.npmjs.com/package/got)  
Lightweight alternative to [request](https://www.npmjs.com/package/request) with native Promise support built in.  

**[gulp-cli](https://www.npmjs.com/package/gulp-cli)**  
Global access to the `gulp` command.  

[hapi](https://www.npmjs.com/package/hapi)  
Developer-friendly Node framework used at lots of big companies.  

[hpm-cli](https://www.npmjs.com/package/hpm-cli)  
A plugin manager for the [Hyper](https://hyper.is) terminal emulator.  

[http-server](https://www.npmjs.com/package/http-server)  
A simple HTTP server you can use to prototype your app or static website. Use this if you don't want/need the additional features of Browser Sync. Can also be used in an NPM script.  

[immutable](https://www.npmjs.com/package/immutable)  
Create immutable data structures in JavaScript.  

**[is-online-cli](https://www.npmjs.com/package/is-online-cli)**  
Check if you're connected to the internet.  

**[jest-cli](https://www.npmjs.com/package/jest-cli)**  
JavaScript testing framework from Facebook that works out-of-the-box.  

[keystone](https://www.npmjs.com/package/keystone)  
Node CMS built on Express and MongoDB.  

[koa](https://www.npmjs.com/package/koa)  
Futuristic Node framework using async/await and generators. Requires a minimum of Node 7.6.0.  

[less](https://www.npmjs.com/package/less)  
A JavaScript CSS preprocessor that runs on Node or in the browser. Check out [less-middleware](https://www.npmjs.com/package/less-middleware) to render your less files in your Express app.  

[lev](https://www.npmjs.com/package/lev)  
A CLI for performing basic CRUD operations on a LevelDB database.  

[level](https://www.npmjs.com/package/level)  
A Node.js wrapper for Google's LevelDB.  

[listr](https://www.npmjs.com/package/listr)  
Create task lists in the Terminal.  

[live-server](https://www.npmjs.com/package/live-server)  
Simple HTTP server with live reloading.  

**[localtunnel](https://www.npmjs.com/package/localtunnel)**  
Turn your dev server running on localhost into a live server you can send to a friend.  

[lodash](https://www.npmjs.com/package/lodash)  
Functional JavaScript utility library.  

[loopback](https://www.npmjs.com/package/loopback)  
Open source Node framework from IBM for building RESTful APIs. Has native support for various databases using optional plugins.  

[lowdb](https://www.npmjs.com/package/lowdb)  
A simple JSON database using the Lodash API.  

[marko](https://www.npmjs.com/package/marko)  
Reactive component and template library from eBay.  

[meow](https://www.npmjs.com/package/meow)  
Tool for creating help interfaces in CLI apps.  

[mkdirp](https://www.npmjs.com/package/mkdirp)  
Use this as a cross-platform way to create directories. Can be used in your app or within your package.json in a build script.  

[mocha](https://www.npmjs.com/package/mocha)  
Popular JavaScript testing framework. Extendable using libraries like Chai or Sinon.  

[moment](https://www.npmjs.com/package/moment)  
Parse and display dates and times effortlessly.  

[mongoose](https://github.com/Automattic/mongoose)  
Robust ODM for MongoDB.  

[ncp](https://www.npmjs.com/package/ncp)  
Recursively copy directories in your Node app.  

[nedb](https://www.npmjs.com/package/nedb)  
A 100% JavaScript persistent or in-memory database using a subset of MongoDB's API.  

[nedb-repl](https://www.npmjs.com/package/nedb-repl)  
A Mongo-like shell for NeDB.  

[next](https://www.npmjs.com/package/next)  
Framework for server-side rendering React apps.  

**[nodemon](https://www.npmjs.com/package/nodemon)**  
Nodemon is a simple command line utility that watches your Node app for changes so you don't have to keep running `node app.js` everytime you make a change.  

[npm-gui](https://www.npmjs.com/package/npm-gui)  
NPM GUI is a browser-based GUI for NPM packages - either global, or whatever project you're currently in. I use it to keep my global NPM packages up to date.  

**[opn-cli](https://www.npmjs.com/package/opn-cli)**  
CLI for [opn](https://www.npmjs.com/package/opn). Opens files or URLs from the command line, e.g., `opn https://google.com` or `opn app.js`. You can also include it in your NPM scripts, which is useful if you want to open the browser on the port your app is running on. Combine it with Concurrently to run the server and open the browser simultaneously, i.e., `concurrently "node server.js" "opn http://localhost:1337"`.  

[ora](https://github.com/sindresorhus/ora)  
Create a loading spinner in the Terminal.  

[pageres-cli](https://www.npmjs.com/package/pageres-cli)  
Take a screenshot of any website from the command line.  

[peerflix](https://github.com/mafintosh/peerflix)  
Streams a torrent to VLC.  

[phenomic](https://www.npmjs.com/package/phenomic)  
Static site generator based on React.  

[postcss](https://www.npmjs.com/package/postcss)  
PostCSS is a JavaScript utility for transforming your CSS using plugins. You could lint your CSS, minify your CSS, or even automatically add vendor prefixes.  

[prepack](https://www.npmjs.com/package/prepack)  
JavaScript compiler from Facebook that partially evaluates your code so it runs faster.  

[prettier](https://www.npmjs.com/package/prettier)  
Formats your code to a consistent style without any configuration.  

[prompt](https://www.npmjs.com/package/prompt)  
Create simple user input prompts.  

**[psi](https://www.npmjs.com/package/psi)**  
Google PageSpeed Insights from the terminal.  

[pug](https://www.npmjs.com/package/pug)  
Template engine influenced by HAML.  

[react](https://www.npmjs.com/package/react)  
Facebook's front-end library for building reactive user interface components. Also include [react-dom](https://www.npmjs.com/package/react-dom) to render your components to the DOM.  

[react-engine](https://www.npmjs.com/package/react-engine)  
PayPal's Express view engine for rendering React components on the server. I've found it to be faster than [express-react-views](https://www.npmjs.com/package/express-react-views).  

[request](https://www.npmjs.com/package/request)  
Simplified HTTP request client. Can be wrapped with `request-promise` or `request-promise-native` to add Promise support.  

[restify](https://www.npmjs.com/package/restify)  
Lightweight Node framework for building RESTful APIs.  

[rimraf](https://www.npmjs.com/package/rimraf)  
`rm -rf` in a Node app.  

[sequelize-cli](https://www.npmjs.com/package/sequelize-cli)  
Installing the Sequelize CLI globally gives you global access to the `sequelize init` command when starting your project.  

[shelljs](https://www.npmjs.com/package/shelljs)  
Write Bash scripts in JavaScript. Check out [shx](https://www.npmjs.com/package/shx) for a command line version that can be used in NPM scripts.  

[shrink-ray](https://www.npmjs.com/package/shrink-ray)  
Compresses your files using gzip or brotli, depending on which browser your request comes from. Faster and better compression than the [compression](https://www.npmjs.com/package/compression) library.  

[slap](https://www.npmjs.com/package/slap)  
Terminal text editor written in JavaScript. Works great on macOS. Mouse doesn't work on Windows; runs really slow on Cloud 9.  

**[speed-test](https://www.npmjs.com/package/speed-test)**  
Get your ping and bandwidth from speedtest.net in the Terminal.  

[socket.io](https://www.npmjs.com/package/socket.io)  
Realtime communication in Node.  

[standard](https://www.npmjs.com/package/standard)  
JavaScript style guide, linter, and code fixer all in one.  

**[stylelint](https://www.npmjs.com/package/stylelint)**  
Like ESLint, but for CSS. Also works with Sass, Less, and PostCSS.  

[surge](https://www.npmjs.com/package/surge)  
The Surge command line tool will publish your web application to Surge with a single command. You can also use [GitHub Pages](https://pages.github.com/); but Surge gives you more features like a custom domain name. Their Plus plan is $13/mo per project, and gives you HTTPS and CORS.  

[table](https://www.npmjs.com/package/table)  
Create tables in your command line apps.  

[torrent](https://www.npmjs.com/package/torrent)  
Download torrents from the command line.  

[trash-cli](https://www.npmjs.com/package/trash-cli)  
Cross-platform (macOS, Windows, Linux) command-line tool for sending files to the trash instead of permanently deleting them.  

[twit](https://www.npmjs.com/package/twit)  
Twitter API client.  

[webpack](https://www.npmjs.com/package/webpack)  
Compiles and bundles your code into a single bundle.js file. Has a large plugin ecosystem, including a dev server with live reloading.  

**[windows-build-tools](https://www.npmjs.com/package/windows-build-tools)**  
Installs Microsoft Visual C++ Build Tools as well as Python 2.7 which are required to build many popular NPM packages on Windows.  

[yargs](https://www.npmjs.com/package/yargs)  
Create CLI apps that take command line arguments.  

**[yarn](https://www.npmjs.com/package/yarn)**  
Node package manager from Facebook.  
