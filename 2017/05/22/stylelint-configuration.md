# Stylelint Configuration
[Stylelint](https://stylelint.io) is a powerful linter, similar to ESLint, that can be configured using rules. Stylelint is powered by PostCSS, so it understands CSS-like syntaxes like SugarSS.  

### Install Stylelint
Stylelint must be installed globally by NPM.  

```
npm install --global stylelint
```

### Install a Styleguide
You can customize your own rules from scratch, or install a styleguide. I recommend `stylelint-config-standard`.

```
npm install --global stylelint-config-standard
```

### Configure Stylelint
You need to create a `.stylelintrc.json` in your home (`~/`) directory which contains your rules. Like ESLint, you can also have a config file in your project folder with rules specific to your project.  

*Note: I'm using NVM, so the location of my global node modules is not the default.*  

*Note: The additional rules are for SugarSS syntax. You can omit them if you're not using it.*  

```
{
  "extends": "C:\\Users\\Adam\\AppData\\Roaming\\nvm\\v7.10.0\\node_modules\\stylelint-config-standard",
  "rules": {
    "block-closing-brace-empty-line-before": null,
    "block-closing-brace-newline-after": null,
    "block-closing-brace-newline-before": null,
    "block-closing-brace-space-before": null,
    "block-opening-brace-newline-after": null,
    "block-opening-brace-space-after": null,
    "block-opening-brace-space-before": null,
    "declaration-block-semicolon-newline-after": null,
    "declaration-block-semicolon-space-after": null,
    "declaration-block-semicolon-space-before": null,
    "declaration-block-trailing-semicolon": null
  }
}
```

### Install Editor Plugins
**Atom:** [linter-stylelint](https://atom.io/packages/linter-stylelint)  
**VS Code:** [stylelint](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint)  
**Sublime:** [SublimeLinter-contrib-stylelint](https://packagecontrol.io/packages/SublimeLinter-contrib-stylelint)  
