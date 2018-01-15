# NPM Peer Dependencies with JQ
[jq](https://github.com/stedolan/jq) is a command line utility for parsing JSON. You can use it read the `peerDependencies` field in a `package.json` (or any field), and pipe that output to `npm install`.

These are contrived examples; there are npm packages like `npm-install-peers` or `install-peerdeps` that can do this for you (although neither work for global installs).

### Install JQ
Linux: `sudo apt-get install jq`  
macOS: `brew install jq`  
Windows: `choco install jq`

### Install from local `package.json`
*Global:*
```
cat /usr/local/lib/node_modules/<package>/package.json | jq --raw-output ".peerDependencies | keys | join(\" \")" | xargs npm install --global
```

*Local:*
```
cat ./package.json | jq --raw-output ".peerDependencies | keys | join(\" \")" | xargs npm install --save
```

### Install from NPM Registry
*Get the latest version number:*  
```
LATEST=$(curl http://registry.npmjs.com/<package> | jq ".\"dist-tags\" | .latest")
```

*Install that version and its peer dependencies:*  
```
curl http://registry.npmjs.com/<package> | jq --raw-output ".versions | .$LATEST | .peerDependencies" | keys | \"<package> \" + join(\" \")" | xargs npm install --global
```

### Install from unpkg.com
*If you know the version:*  
```
curl https://unpkg.com/<package>@<version>/package.json | jq --raw-ouput ".peerDependencies | keys | \"<package> \" + join(\" \")" | xargs npm install --global
```

*Pass -L to curl to be redirected to the latest version:*
```
curl -L https://unpkg.com/<package>/package.json | jq --raw-ouput ".peerDependencies | keys | \"<package> \" + join(\" \")" | xargs npm install --global
```

### Windows
I haven't been able to get it working in Windows. No matter what I've tried, `npm install` interprets the passed arguments as a single string, i.e., `"foo bar"` instead of `foo bar`.
