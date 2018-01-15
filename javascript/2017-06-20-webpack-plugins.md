# Webpack Plugins
This is a running list of Webpack plugins I've tried and like (i.e., they actually work).

### [case-sensitive-paths-webpack-plugin](https://github.com/Urthen/case-sensitive-paths-webpack-plugin)
Enforces the entire path of all required modules match the exact case of the actual path on disk.

### [clean-webpack-plugin](https://github.com/johnagan/clean-webpack-plugin)
Deletes the build folder before bundling.

### [copy-webpack-plugin](https://github.com/kevlened/copy-webpack-plugin)
Copies individual files or entire directories to the build folder.

### [duplicate-package-checker-webpack-plugin](https://github.com/darrenscerri/duplicate-package-checker-webpack-plugin)
Warns you if multiple versions of the same package exist in your build.

### [extract-text-webpack-plugin](https://github.com/webpack-contrib/extract-text-webpack-plugin)
Moves all bundled CSS into a separate `.css` file.

### [favicons-webpack-plugin](https://github.com/jantimon/favicons-webpack-plugin)
Generates 37 icon files from a single `.png` file and injects the necessary `<link>` tags using `html-webpack-plugin`.

*Note: It's easier to just use [RealFaviconGenerator.net](https://realfavicongenerator.net).*

### [friendly-errors-webpack-plugin](https://github.com/geowarin/friendly-errors-webpack-plugin)
Cleans, aggregates and prioritizes error messages.

### [happypack](https://github.com/amireh/happypack)
Distributes your loaders across multiple worker threads (Node processes) to dramatically reduce build times.

### [hard-source-webpack-plugin](https://github.com/mzgoddard/hard-source-webpack-plugin)
Creates a cache of your initial build so future builds will be significantly faster.

### [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin)
Simplifies the creation of HTML files to serve your bundles. At the bare minimum, it can inject a `<script>` tag into your `index.html`. Can be used standalone or extended with additional plugins.

### [html-webpack-include-assets-plugin](https://github.com/jharris4/html-webpack-include-assets-plugin)
Allows you to add a list of assets to be injected by `html-webpack-plugin`. Useful for files copied to the build folder by `copy-webpack-plugin`.

### [npm-install-webpack-plugin](https://github.com/webpack-contrib/npm-install-webpack-plugin)
Automatically runs `npm install` when you require a new package in your build (when running `webpack-dev-server`).

### [offline-plugin](https://github.com/NekR/offline-plugin)
Uses ServiceWorker and AppCache to make your bundled assets available offline.

### [script-ext-html-webpack-plugin](https://github.com/numical/script-ext-html-webpack-plugin)
Enhances `html-webpack-plugin` by allowing the use of custom attributes for `<script>` tags.

### [style-ext-html-webpack-plugin](https://github.com/numical/style-ext-html-webpack-plugin)
Takes the extracted CSS from `extract-text-webpack-plugin` and replaces the `<link>` tags from `html-webpack-plugin` and replaces them with `<style>` tags.

### [sw-precache-webpack-plugin](https://github.com/goldhand/sw-precache-webpack-plugin)
Generates a service worker to cache your emitted bundled assets.

### [webpack-bundle-analyzer](https://github.com/th0r/webpack-bundle-analyzer)
Creates an in-browser interactive treemap of your bundled modules.

### [webpack-parallel-uglify-plugin](https://github.com/gdborton/webpack-parallel-uglify-plugin)
Allows you to run UglifyJS on multiple bundles in parallel instead of sequentially.

### [webpack-shell-plugin](https://github.com/1337programming/webpack-shell-plugin)
Allows you include shell commands to be run before and after your build task.

### [zip-webpack-plugin](https://github.com/erikdesjardins/zip-webpack-plugin)
Creates a zip of all emitted files.
