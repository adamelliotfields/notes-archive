# How to Symlink NVM Node Binaries
> :calendar: *July 15, 2017*

This only applies to Linux and macOS, as [nvm-windows](https://github.com/coreybutler/nvm-windows/)
takes care of this automatically.

In Webstorm, you have to define the path to the Node binary as well as the ESLint and Stylelint
binaries. If you're using NVM, the path to those binaries will change every time you update Node.

Symlinking the Node binary is also useful if you're running into issues with Express listening on
port 80 and `sudo node server.js` isn't working.

Note that the below commands symlink the current version of Node at the time you run the command.
When you upgrade Node, you will have to run these commands again.

If you want to use a version of Node specific to a project or a locally installed ESLint/Stylelint,
you can select them in your project specific settings.

### Node and NPM Binaries
`sudo ln -s "$NVM_DIR/versions/node/$(nvm version)/bin/node" "/usr/local/bin/node"`

`sudo ln -s "$NVM_DIR/versions/node/$(nvm version)/bin/npm" "/usr/local/bin/npm"`

### Node Modules
`sudo ln -s "$NVM_DIR/versions/node/$(nvm version)/lib/node_modules" "/usr/local/lib/node_modules"`

### Webstorm Preferences
Languages & Frameworks > Node.js and NPM
 - Set "Node interpreter" to `/usr/local/bin/node`

Languages & Frameworks > JavaScript > Code Quality Tools > ESLint
 - Set "Node interpreter" to `/usr/local/bin/node`
 - Set "ESLint package" to `/usr/local/lib/node_modules/eslint`

Languages & Frameworks > Stylesheets > Stylelint
 - Set "Node interpreter" to `/usr/local/bin/node`
 - Set "Stylelint package" to `/usr/local/lib/node_modules/stylelint`

### Updating
You'll need to remove the old symlinks before creating new ones, otherwise you'll get a
`File exists` message.

`sudo rm /usr/local/bin/node`

`sudo rm /usr/local/bin/npm`

`sudo rm /usr/local/lib/node_modules`
