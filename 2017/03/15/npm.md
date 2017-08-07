# NPM

### Installing npm
```
curl http://npmjs.org/install.sh | sh
```

### Update npm
There are several ways you can update `npm`.
```
curl http://npmjs.org/install.sh | sh
```

**or**

```
npm install npm -g 
```

### Search for npm packages
```
npm search hook.io 
```

**Protip:** _Try searching via the browser with [http://browsenpm.org](http://browsenpm.org/)_

### View details of a npm package
```
npm view hook.io 
```

### Interactively create a `package.json`
This will ask you a bunch of questions, and then write a `package.json` for you.

It attempts to make reasonable guesses about what you want things to be set to, and then writes a `package.json` file with the options you've selected.

If you already have a `package.json` file, it'll read that first, and default to the options in there.

It is strictly additive, so it does not delete options from your `package.json` without a really good reason to do so.

If you invoke it with `-f`, `--force`, `-y`, or `--yes`, it will use only defaults and not prompt you for any options.

```
npm init
```

### Installing a npm package locally
For the purpose of this demo, we will use `http-server`.

`http-server` is a package we've written which provides an easy to use wrapper around node's core http.Server class. This module makes for a good example, since it's API provides both a CLI binary and a requirable node.js module.

```
npm install http-server 
```

This performs a **local** install of `http-server` in our **current working directory**

You may also notice a new **`node_modules/`** folder. You can ignore this for now.

`npm install` takes 3 exclusive, optional flags which save or update the package version of your main `pakage.json`:

`-S` or `--save`: Package will appear in your dependencies.
`-D` or `--save-dev`: Package will appear in your devDependencies.
`-O` or `--save-optional`: Package will appear in your optionalDependencies.

When using any of the above options to save dependencies to your `package.json`, there is an additional, optional flag:

`-E` or `--save-exact`: Saved dependencies will be configured with an exact version rather than using npm's default semver range operator.

### Installing a npm package into an application

```
mkdir mynewapp/
cd mynewapp
npm install http-server
touch test.js
```

**run script**

```
node test.js 
```

**Notice how we: `require('http-server')`? What kind of wizardry is this?**

`http-server` is not the name of a native node.js module. It's the name of the package we just installed from `npm`. `node` and `npm` are smart enough to automatically load modules from our local `node_modules/` folder.

### Understanding Global versus Local installs in npm 
By default, `npm` will install all packages into the **local** directory you are working in. This is a **good** thing. It can however, be slightly confusing if you have worked with inferior package management systems in the past.

### Global Package Installation
If you want to have a package available globally use:

```
npm install http-server -g
```

The `-g` flag will indicate that `http-server` should be installed **globally**, and be available for all node scripts to require.

Now, we can **`require('http-server')`** in any node script on our system.

In addition, since the `http-server` package has specified a `bin` property, it will also install a binary script called `http-server` globally.

_Now you can simply run the command:_

```
http-server
```

### Checking for outdated packages
This command will check the registry to see if any (or, specific) installed packages are currently outdated.

```
npm outdated
```

### Updating a package
This command will update all the packages listed to the latest version (specified by the tag config), respecting semver.

It will also install missing packages. As with all commands that install packages, the `--dev` flag will cause devDependencies to be processed as well.

If the `-g` flag is specified, this command will update globally installed packages.

If no package name is specified, all packages in the specified location (global or local) will be updated.

```
npm update -g http-server
```

### Uninstalling a package locally

```
cd mynewapp/
npm uninstall http-server
```

### Uninstalling a package globally

```
npm uninstall http-server -g
```

### Installing a specific version of a package 

```
cd mynewapp/
npm install http-server@0.3.0
```

### Listing installed packages
This command will print to `stdout` all the versions of packages that are installed, as well as their dependencies, in a tree-structure.

Positional arguments are `name@version-range` identifiers, which will limit the results to only the paths to the packages named. Note that nested packages will also show the paths to the specified packages.

```
npm ls
```

### Cloning a module from Github
This is important. In some cases, there will be patches, forks, or branches that we will want to use for our module, but have not yet been published to `npm`. Thankfully, the source code for most `npm` modules is also available on [Github.com](http://github.com)

```
git clone git://github.com/nodeapps/http-server.git
cd http-server/
npm link
```

_Our cloned version of `http-server` is now linked locally_

### Linking any npm package locally
If you have a local directory containing an `npm` package, you can link this package locally. This is good for development purposes and for situations when we do not want to publish our package to the public `npm` repository.

```
cd http-server/
npm link

```
_Our local version of `http-server` is "linked" on our local machine_

### Linking local npm packages to multiple applications 

As we've seen before, `npm` will install packages into the local directory by default. `npm link` works pretty much the same way.

```
mkdir newapp/
cd newapp/
npm link http-server
```

_This indicates that we've now linked `http-server` into our new application `newapp`. If we had not run `npm link http-server` we would have gotten a missing module error_

### Unlinking a npm package from an application

```
cd newapp/
npm unlink http-server
```

### Unlinking a npm package from your system

```
cd http-server/
npm unlink
```

### Create a new npm package

```
mkdir mypackage/
cd mypackage/
npm init
```

### Creating a new user account on npm

```
npm adduser
```

### Publishing a npm package

```
cd mypackage/
npm publish
```

### Unpublishing a npm package

```
npm unpublish http-server
```

### Managing owners of packages
If you want multiple users to be able to publish to the same package:

```
npm owner add marak http-server
npm owner rm marak http-server
npm owner ls http-server
```

### Removing extraneous packages
This command removes "extraneous" packages. If a package name is provided, then only packages matching one of the supplied names are removed.

Extraneous packages are packages that are not listed on the parent package's dependencies list.

```
npm prune
```
