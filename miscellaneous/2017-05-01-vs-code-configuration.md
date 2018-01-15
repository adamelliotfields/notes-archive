# VS Code Configuration
I recommend VS Code if you're looking for an editor that doesn't require hours of reading docs to get set up; or downloading dozens of plugins to get the functionality you want. VS Code's integrated autocompletion also *just works* out of the box. It also works really well on Windows, with a great integrated terminal (that can be configured to use CMD, PowerShell, or Bash).  

On Windows, I recommend installing VS Code outside of Chocolatey, so VS Code can manage its own autoupdating.  

### Extensions
[Babel](https://marketplace.visualstudio.com/items?itemName=dzannotti.vscode-babel-coloring)  
Syntax coloring for newer versions of JavaScript.  

[ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)  
An interface to ESLint. Requires ESLint to be installed and configured. See my Gist [here](https://gist.github.com/adamelliotfields/a6e351873bc0409e1d25d617cbf17341).  

[Stylelint](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint)  
An interface to Stylelint. Requires Stylelint to be installed and configured globally. See below.  

[VS Code Icons](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons)  
Add icons to your files. Makes your editing environment more aesthetically pleasing, while also making it easy to visually identify files and folders.  

### Stylelint Config
Read my Gist [here](https://gist.github.com/adamelliotfields/00fe56382f8e161483994e4256da26c4).  

If you are working with SugarSS files, you'll also need to add this line to your VS Code settings:  

```
"files.associations": { "*.sss": "css" }
```

Unfortunately, the VS Code Stylelint extension can only work with CSS, SCSS, or Less files, so you'll have to tell VS Code to treat `.sss` files like CSS.  

### Settings
File > Preferences > Settings  

*Note: I'm using the [Hack](https://github.com/chrissimpkins/Hack) font. If you don't want to install a font, I recommend Menlo on macOS, Consolas on Windows, or Ubuntu Mono on Ubuntu.  

```
{
  "css.validate": false,
  "editor.detectIndentation": false,
  "editor.fontFamily": "Hack",
  "editor.fontSize": 20,
  "editor.minimap.enabled": true,
  "editor.renderIndentGuides": true,
  "editor.renderWhitespace": "boundary",
  "editor.rulers": [100],
  "editor.tabSize": 2,
  "eslint.options": { "configFile": "C:\\Users\\Adam\\.eslintrc.json" },
  "eslint.nodePath": "C:\\Program Files\\nodejs\\node_modules",
  "files.associations": { "*.sss": "css" },
  "files.eol": "\n",
  "files.insertFinalNewline": true,
  "git.path": "C:\\Program Files\\Git\\cmd\\git.exe",
  "javascript.validate.enable": false,
  "stylelint.enable": true,
  "terminal.integrated.cursorBlinking": true,
  "terminal.integrated.fontSize": 16,
  "terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\WindowsPowerShell\\v1.0\\powershell.exe",
  "window.reopenFolders": "one",
  "workbench.iconTheme": "vscode-icons",
  "workbench.welcome.enabled": true,
  "vsicons.dontShowNewVersionMessage": true
}
```  
