# Sublime Text Configuration
Sublime Text is a powerful text editor that can be extended with a robust ecosystem of packages. I'm also following the progress of [Lime](https://github.com/limetext/lime), which is an open source port of Sublime written in Go.

### Install Package Control
Follow the instructions [here](https://packagecontrol.io/installation).

### Install Packages
Most packages work out of the box, but a few require additional configuration. Each package comes with default settings, which can be overridden by creating a user settings file. Only the rules defined in the user settings file will override the default rules.  

User settings files are located in `C:\Users\Adam\AppData\Roaming\Sublime Text 3\Packages\User` on Windows and `/Users/adamfields/Library/Application Support/Sublime Text 3/Packages/User` on macOS.  

To configure a package's settings in Sublime, go to Preferences > Package Settings > Settings - User.  

**[Babel](https://packagecontrol.io/packages/Babel)**  
Language support for ES6+ JavaScript and JSX.  

**`Babel.sublime-settings`**  

```
{ "node_modules": { "windows": "C:\\Users\\Adam\\AppData\\Roaming\\nvm\\v7.10.0\\node_modules" } }
```

*Note: I'm using NVM, so the location of my `node_modules` folder is not the default.*  

*Note: You need to set Babel syntax. Go to View > Syntax > Open all with current extension as > Babel > JavaScript (Babel)*  

**[Color Highlighter](https://packagecontrol.io/packages/Color%20Highlighter)**  
Highlights your CSS color values with the appropriate color.  

**`ColorHighlighter.sublime-settings`**  

```
{ "file_exts": [".sss", ".css", ".sass", ".scss", ".less", ".styl", ".html", ".js", ".sublime-settings", ".tmTheme", ".stTheme", ".erb", ".haml", ".back", ".py", ".md"] }
```

*Note: I'm using SugarSS, so I needed to add the `.sss` extension.*  

**[Colorsublime](https://packagecontrol.io/packages/Colorsublime)**  
Preview color schemes and install them all within Sublime.  

**[DocBlockr](https://packagecontrol.io/packages/DocBlockr)**  
Makes it easy to create JSDoc-style comments.  

**[Emmet](https://packagecontrol.io/packages/Emmet)**  
Shortcuts for HTML and CSS.  

**[Fix Mac Path](https://packagecontrol.io/packages/Fix%20Mac%20Path)**  
Necessary for Sublime to use non-system binaries like Node (only applicable on macOS).  

**[GitGutter](https://packagecontrol.io/packages/GitGutter)**  
Shows Git line diffs in the gutter. Shows changes in a tooltip when highlighting the gutter icon.  

**`GitGutter.sublime-settings`**  

```
{ "git_binary": "C:\\Program Files\\Git\\cmd\\git.exe" }
```

**[HyperClick](https://packagecontrol.io/packages/HyperClick)**  
Jump to function definitions in other files.  

**[MarkdownEditing](https://packagecontrol.io/packages/MarkdownEditing)**  
Improved syntax highlighting for Markdown files.  

**[PackageResourceViewer](https://packagecontrol.io/packages/PackageResourceViewer)**  
Edit Sublime packages in Sublime. Useful for changing font sizes in themes.  

**[SublimeLinter](https://packagecontrol.io/packages/SublimeLinter)**  
Linting framework. Requires language-specific plugins to work.  

*Note: You can change the gutter icon and enable tooltips in the settings. I have tooltips off because they compete with Tern tooltips.*   

**[SublimeLinter-contrib-eslint](https://packagecontrol.io/packages/SublimeLinter-contrib-eslint)**  
SublimeLinter plugin for ESLint. Requires ESLint to be installed and configured. See my Gist [here](https://gist.github.com/adamelliotfields/a6e351873bc0409e1d25d617cbf17341).  

**[SublimeLinter-contrib-stylelint](https://packagecontrol.io/packages/SublimeLinter-contrib-stylelint)**  
SublimeLinter plugin for Stylelint. Requires Stylelint to be installed and configured. See my Gist [here](https://gist.github.com/adamelliotfields/00fe56382f8e161483994e4256da26c4).  

**[SublimeLinter-json](https://packagecontrol.io/packages/SublimeLinter-json)**  
SublimeLinter plugin for JSON files.  

**[Syntax Highlighting for PostCSS](https://packagecontrol.io/packages/Syntax%20Highlighting%20for%20PostCSS)**  
Language support for PostCSS and SugarSS files.  

**[tern_for_sublime](https://packagecontrol.io/packages/tern_for_sublime)**  
JavaScript code analysis and autocompletion engine. Requires Tern to be installed and configured. See my Gist [here](https://gist.github.com/adamelliotfields/d129b52ee6828ec695e3740f6ac30a6a).  

**`Tern.sublime-settings`**  

```
{ "tern_argument_hints": true, "tern_argument_completion": true }
```

**`Preferences.sublime-settings`**  

```
{ "auto_complete_triggers": [{ "characters": "<", "selector": "text.html" }, { "characters": ".", "selector": "source.js" }] }
```

*Note: You need to add the above to your Sublime user preferences settings to trigger Tern autocompletion.*  

*UPDATE: I'm no longer using Tern as it frequently crashes.*  

**[Theme - SoDaReloaded](https://packagecontrol.io/packages/Theme%20-%20SoDaReloaded)**  
Similar to the original Soda theme (the most popular Sublime theme), but with included file icons.  

### Minimal Build
* Babel
* Colorsublime
* Fix Mac Path
* HyperClick
* PackageResourceViewer
* SublimeLinter
* Linter-eslint
* Linter-json
* SoDaReloaded  

### Edit Settings
To edit settings in Sublime, go to Preferences > Settings.  

I'm using the [Hack](https://github.com/chrissimpkins/Hack) font. If you don't want to install a new font, I recommend Menlo on macOS, Consolas on Windows, and Ubuntu Mono on Ubuntu.  

*Note: `"font_options": ["directwrite"]` is Windows only. I recommend `"no_round"` on macOS (you'll need to bump the font size on Retina displays as well).*

```
{
	"always_show_minimap_viewport": true,
	"auto_complete_commit_on_tab": true,
	"auto_complete_cycle": true,
	"auto_complete_triggers":
	[
		{
			"characters": "<",
			"selector": "text.html"
		},
		{
			"characters": ".",
			"selector": "source.js"
		}
	],
	"auto_complete_with_fields": true,
	"color_scheme": "Packages/Colorsublime - Themes/Neon.tmTheme",
	"draw_indent_guides": true,
	"draw_white_space": "all",
	"ensure_newline_at_eof_on_save": true,
	"font_face": "Hack",
	"font_options":
	[
		"directwrite"
	],
	"font_size": 14,
	"highlight_line": true,
	"highlight_modified_tabs": true,
	"rulers":
	[
		100
	],
	"scroll_past_end": false,
	"shift_tab_unindent": true,
	"show_encoding": true,
	"show_line_endings": true,
	"tab_size": 2,
	"theme": "SoDaReloaded Dark.sublime-theme",
	"translate_tabs_to_spaces": true
}
```
