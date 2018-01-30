# Tern Configuration
> :calendar: *May 22, 2017*

[Tern](http://ternjs.net/) is a JavaScript code analysis and autocompletion engine that is editor agnostic.  

### Install Tern
The Tern backend is installed via NPM, and an editor extension must be installed separately.  

```
npm install --global tern
```

### Configure Tern
You'll also need to create a `.tern-config` file in your home (`~/`) directory.  

You can also have individual settings for each project using a `.tern-project` file in the project folder.  

Available [libs](https://github.com/ternjs/tern/tree/master/defs).  

Available [plugins](https://github.com/ternjs/tern/tree/master/plugin).  

There are more configuration settings, so definitely check out the [docs](http://ternjs.net/doc/manual.html).  

*Note: Tern is not limited to just jQuery or AngularJS. Tern reads the files in your `node_modules` folder to generate autocompletion suggestions and method definition tooltips. It works great with React.*  

```
{
  "ecmaVersion": 6,
  "libs": ["browser", "ecmascript", "jquery"],
  "plugins": {
    "complete_strings": {},
    "doc_comment": { "strong": true },
    "commonjs": {},
    "es_modules": {},
    "modules": {},
    "node": {},
    "node_resolve": {},
  }
}
```

### Install Editor Plugins

**Atom:** [atom-ternjs](https://atom.io/packages/atom-ternjs)  
**Sublime:** [tern_for_sublime](https://packagecontrol.io/packages/tern_for_sublime)  
