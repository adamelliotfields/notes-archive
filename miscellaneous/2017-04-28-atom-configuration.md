# Atom Configuration
This is my setup for Atom.  

Atom has a massive ecosystem of packages, which I view as both a pro and a con. On the pro side, you can customize Atom to your heart's content, and many of the most popular packages are actively maintained and updated. On the con side, if you're just getting started with Atom, you have thousands of packages to filter through, and many are duplicates of other packages or abandoned (which could break with an Atom update). Because of all the packages, you'll get prompted to install updates fairly frequently.  

If you're just getting started, I'd recommend VS Code for JavaScript development. If you want to get started with Atom right away, here are my recommended packages and settings.  

### Packages
To install these packages, simply copy this snippet into a file (I call it `packages.txt`):  

```
busy-signal
docblockr
emmet
file-icons
highlight-selected
hyperclick
intentions
js-hyperclick
language-babel
linter
linter-eslint
linter-jsonlint
linter-markdown
linter-stylelint
linter-ui-default
minimap
minimap-find-and-replace
minimap-highlight-selected
multi-cursor
neon-syntax
```

And run this command from Terminal (in the directory of `packages.txt`):  

`apm install --packages-file packages.txt`  

Think of this as akin to running `npm install` with a `package.json` full of project dependencies. I have a feeling this uses Node's `readline` module, so make sure each package is on its own line when you paste it. Also, I'd recommend doing this when Atom is closed.  

If you want to generate your own `packages.txt` for backup purposes, run:  

`apm list --installed --bare > packages.txt`  

[docblockr](https://github.com/nikhilkalige/docblockr)  
This package will help build your JSDoc comments for functions. When the cursor is directly above a function declaration or statement, press `/**` + `TAB` and your doc block will pre-populate for you.  

[emmet](https://github.com/emmetio/emmet-atom)  
Emmet is used for HTML and CSS. Check out the Emmet [cheatsheet](https://docs.emmet.io/cheat-sheet/) for all it can do.  

[file-icons](https://github.com/file-icons/atom)  
File icons for your Tree View.  

[highlight-selected](https://github.com/richrace/highlight-selected)  
Double-click on any word, and every instance of that word will be highlighted throughout the file.  

[hyperclick](https://github.com/facebooknuclide/hyperclick)  
Gives Atom click-to-definition for variables, functions, and modules. Requires a the `js-hyperclick` provider.  

[js-hyperclick](https://github.com/AsaAyers/js-hyperclick)  
Provider for `hyperclick`.  

[language-babel](https://github.com/gandm/language-babel)  
Syntax highlighting for ES2015 and beyond, as well as JSX. Also provides auto-indenting and tag closing for JSX.  

[linter](https://github.com/steelbrain/linter)  
Base linter package for Atom. Requires providers for each language.  

[linter-eslint](https://atom.io/packages/linter-eslint)  
Linter provider for JavaScript files. You'll need to `npm install --global eslint` and have an `.eslintrc.json` file in your home directory. I wrote a Gist on getting it set up [here](https://gist.github.com/adamelliotfields/a6e351873bc0409e1d25d617cbf17341).  

[linter-jsonlint](https://github.com/AtomLinter/linter-jsonlint)  
Linter provider for JSON files. Never miss a comma again!  

[linter-markdown](https://github.com/AtomLinter/linter-markdown)  
Linter provider for Markdown files.  

[linter-stylelint](https://github.com/AtomLinter/linter-stylelint)  
Linter provider for CSS files. You'll need to install and configure Stylelint. Read my Gist [here](https://gist.github.com/adamelliotfields/00fe56382f8e161483994e4256da26c4).  

[minimap](https://github.com/atom-minimap/minimap)  
Displays a minimap of your code, similar to the built in minimap in VS Code and Sublime. Works even better with providers.  

[minimap-find-and-replace](https://github.com/atom-minimap/minimap-find-and-replace)  
Minimap provider to show find-and-replace search results.  

[minimap-highlight-selected](https://github.com/atom-minimap/minimap-highlight-selected)  
Minimap provider to show highlight selected results.  

[multi-cursor](https://github.com/joseramonc/multi-cursor)  
Allows you to edit multiple lines simultaneously. Really useful for editing CSV files if you're into that sort of thing. Hold `ALT` and press the up or down arrows to activate it.  

[neon-syntax](https://github.com/anomaly256/neon-syntax)  
Neon syntax coloring with a subtle glowing effect.  

Note that the `busy-signal`, `intentions`, and `linter-ui-default` packages are required by `linter` and will be installed automatically if you delete them from my `packages.txt`.  

As for Facebook's monstrous Nuclide suite, I found that it added a ton of features that I never used and really added seconds to my Atom initial startup time.  

### Settings
This is my `settings.cson` file, which is a Coffeescript file located in the `~/.atom/` directory. I encourage you to tweak your settings to your own personal preferences, but this will get you up and running right away:  

Note that I'm using the [Hack](https://github.com/chrissimpkins/Hack) font. If you don't want to install a font, I recommend Menlo on macOS, Consolas on Windows, and Ubuntu Mono on Ubuntu.  

```
"*":
  "":
    source:
      gfm:
        whitespace:
          removeTrailingWhitespace: false
  core:
    closeDeletedFileTabs: true
    excludeVcsIgnoredPaths: false
    openEmptyEditorOnStart: false
    projectHome: "C:\\Users\\Adam\\GitHub"
    telemetryConsent: "limited"
    themes: [
      "one-dark-ui"
      "neon-syntax"
    ]
    titleBar: "custom"
    warnOnLargeFileLimit: 1
  editor:
    fontFamily: "Hack"
    fontSize: 20
    invisibles: {}
    preferredLineLength: 100
    showIndentGuide: true
    showInvisibles: true
    tabType: "soft"
    undoGroupingInterval: 500
  "js-hyperclick":
    jumpToImport: true
  "linter-eslint":
    disableWhenNoEslintConfig: false
    eslintrcPath: "C:\\Users\\Adam\\eslintrc.json"
    globalNodePath: "C:\\Program Files\\nodejs"
    useGlobalEslint: true
    rulesToSilenceWhileTyping: [
      "no-trailing-spaces"
      "no-multiple-empty-lines"
      "eol-last"
    ]
  "linter-stylelint":
    disableWhenNoConfig: false
  "linter-ui-default":
    showPanel: true
    showProviderName: true
    showTooltip: false
  "markdown-preview":
    useGitHubStyle: true
  minimap:
    plugins:
      "find-and-replace": true
      "find-and-replaceDecorationsZIndex": 0
      "highlight-selected": true
      "highlight-selectedDecorationsZIndex": 0
  welcome:
    showOnStartup: false
  whitespace: {}
```

That's really all there is to it. Install the packages (don't forget `eslint` and `stylelint`), paste the settings, and you're done.  
