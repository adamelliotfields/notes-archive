# ESLint Configuration
> :calendar: *April 22, 2017*

These are my global ESLint settings, using [semistandard](https://github.com/Flet/semistandard) with global support for jQuery. This is useful to have for general JavaScript web/Node development. For working with specific technologies like AngularJS, React, Mocha/Jest, etc, you should set up a local, project-specific configuration.  

ESLint takes a global/global or local/local approach. This means if you don't have a local ESLint in your project, it will look for a global install and use the globally installed plugins/configs. If you have a local installation (in your project), it will conversely look for locally installed plugins/configs.  

### Install `eslint` and dependencies globally
A global install ensures global access to linter functionality in text editors and the CLI. If you are using NVM or N for Node Version Management, note that you'll have to do this for every version of Node (although, I tend to write my applications in the latest version of Node, and only switch versions to see if the break when running on an older version).  

```
npm install --global eslint
npm install --global eslint-plugin-import eslint-plugin-node eslint-plugin-promise eslint-plugin-standard
npm install --global eslint-config-standard eslint-config-semistandard
```  

### Save ESLint Configuration in home directory (`~/`)
Paste this snippet and save as `.eslintrc.json`. Your home directory is `/Users/<username>` on macOS or `C:\Users\<username>` on Windows.    

```
{
  "env": { "jquery": true },
  "extends": ["semistandard"]
}
```  

### AngularJS
Drop jQuery support and add `eslint-plugin-angular` and `eslint-config-angular`.  

```
yarn add --dev eslint
yarn add --dev eslint-plugin-import eslint-plugin-node eslint-plugin-promise eslint-plugin-standard eslint-plugin-angular
yarn add --dev eslint-config-standard eslint-config-semistandard eslint-config-angular
```

```
{
  "extends": ["semistandard", "angular"]
}
```

### React
Drop jQuery support and add `eslint-plugin-react` and `eslint-config-standard-react` and `eslint-config-standard-jsx`.  

```
yarn add --dev eslint
yarn add --dev eslint-plugin-import eslint-plugin-node eslint-plugin-promise eslint-plugin-standard eslint-plugin-react
yarn add --dev eslint-config-standard eslint-config-semistandard eslint-config-standard-jsx eslint-config-standard-react
```

```
{
  "extends": ["semistandard", "standard-react"]
}
```

### Rules
*Note: semistandard extends standard and adds semicolons; standard-react extends standard-jsx.*  

[semistandard](https://github.com/Flet/eslint-config-semistandard/blob/master/eslintrc.json)  
[standard](https://github.com/feross/eslint-config-standard/blob/master/eslintrc.json)  
[angular](https://github.com/dustinspecker/eslint-config-angular/blob/master/index.js)  
[standard-react](https://github.com/feross/eslint-config-standard-react/blob/master/eslintrc.json)  
[standard-jsx](https://github.com/feross/eslint-config-standard-jsx/blob/master/eslintrc.json)  

### Install `eslint` editor extensions
**Atom**: [linter-eslint](https://atom.io/packages/linter-eslint)  
**VS Code**: [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)  
**Sublime Text**: [SublimeLinter-contrib-eslint](https://packagecontrol.io/packages/SublimeLinter-contrib-eslint)  

### Configure Atom (`/~/.atom/config.cson`)

```
"linter-eslint":
  eslintrcPath: "/Users/adamfields/eslintrc.json"
  globalNodePath: "/usr/local/"
  useGlobalEslint: true
```  

### Configure VS Code (File > Preferences > Settings)
```
  "eslint.options": { "configFile": "C:\\Users\\Adam\\.eslintrc.json" },
  "javascript.validate.enable": false
```
