# Gulp Browserify ES2015 Sourcemaps
The "official" [recipe](http://gulpjs.org/recipes/browserify-uglify-sourcemap.html) on the Gulp site assumes your code is ES5 or has been compiled by Babel to ES5.  

By using [gulp-uglify](https://github.com/terinjokes/gulp-uglify)'s composer, you can use whatever version of UglifyJS you want. [uglify-es](https://www.npmjs.com/package/uglify-es) has a built-in ES2015 parser and an API that is compatable with UglifyJS.

```
const gulp = require('gulp');
const composer = require('gulp-uglify/composer');
const uglify = require('uglify-es');
const browserify = require('browserify');
const source = require('vinyl-source-stream');
const buffer = require('vinyl-buffer');
const sourcemaps = require('gulp-sourcemaps');

gulp.task('javascript', () => {
  const minify = composer(uglify);                          // create a new minifier
  return browserify({ entries: 'src/app.js', debug: true }) // load the entry file and write inline sourcemaps
    .bundle()                                               // bundle
    .pipe(source('bundle.js'))                              // transform Browserify text stream to Gulp vinyl stream
    .pipe(buffer())                                         // transform vinyl stream to buffer
    .pipe(sourcemaps.init({loadMaps: true}))                // load Browserify inline sourcemaps
    .pipe(minify())                                         // minify
    .pipe(sourcemaps.write('./'))                           // write bundle.js.map
    .pipe(gulp.dest('build'));                              // write bundle.js
});
```
