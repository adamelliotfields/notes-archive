# Homebrew Notes
> :calendar: *February 13, 2017*

### Installing Homebrew

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Global Commands

`man brew` shows the manual.

`brew update` updates Homebrew.

`brew outdated` shows what packages are due for upgrades.

`brew doctor` checks the system for potential problems.

`brew prune` removes dead symlinks from Homebrew.

`brew list` shows all installed packages.

`brew search` shows all available packages or searches for a specific package.

### Packages

`brew install` installs a package.

```sh
brew install node
```

`brew uninstall` uninstalls a package.

```sh
brew uninstall node
```

`brew upgrade` upgrades all packages or a specific package.

```sh
brew upgrade node
```

`brew pin` stops a package from being upgraded; `brew unpin` reverses this.

```sh
brew pin node
```

`brew list --versions` shows what versions are installed.

```sh
brew list --versions node
```

`brew switch` changes versions.

```sh
brew switch node 6.9.5
```

`brew desc` shows a package's information.

```sh
brew desc node
```

`brew info` shows information, versions, locations, dependencies, options, and caveats. 

```sh
brew info node
```

`brew cleanup` removes old versions of all packages or a specific package. `brew cleanup -n` shows what will be removed.

```sh
brew cleanup node
```

`brew tap` shows all installed taps if no repository is given; `brew untap` removes a tapped repository.

```sh
brew tap homebrew/php
```

### Dependencies

`brew deps` lists the dependencies for a given brew. 

```sh
brew deps --installed node
```

`brew uses` shows which brews use a particular brew as a dependency.

```sh
brew uses --installed pkg-config
```

`brew leaves` shows packages that are not dependencies. 

`brew missing` checks for missing dependencies.
