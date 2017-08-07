# Sass
Sass (Syntactically Awesome Style Sheets) is a style sheet language and CSS preprocessor. Sass can be written in the original syntax (the indented syntax) or the newer SCSS (Sassy CSS) syntax. Sass extends CSS by providing mechanisms available to more traditional programming languages like variables, conditionals, loops, and objects; plus mixins, extends, and placeholders.

Sass can be compiled into CSS at runtime, or `watch`ed to translate into CSS whenever the Sass file is saved.

The official implementation of Sass is open-source and coded in Ruby.

### Installing Sass
Hint: You need Ruby.

```sh
gem install sass
```

### Compiling Sass
Sass can't be directly interpreted by your browser, so it must first be converted, or compiled, to CSS before the browser can directly understand it.

Compiling refers to converting code to lower level code so that it can be executed. By compiling SCSS to CSS, it can be interpreted by your browser and the results will appear on a webpage.

```sh
sass main.scss main.css
```

### Watching Sass
The `--watch` command tells Sass to watch our `scss` directory for changes and update the style sheet inside the `css` directory.

```sh
sass --watch scss:css
```

The default flag is `--nested`, but you can also do `--expanded` (traditional CSS), `--compact` (each rule is only 1 line), or `--compressed` (minified).

### Sass Source Map
After a successful compile, Sass will generate a source map. You can enable it in Chrome Dev Tools, so inspecting an element in your browser will show the SCSS rule as opposed to the compiled CSS rule.

### Nesting
Nesting is the process of placing selectors inside the scope of another selector.

Selectors that are nested inside the scope of another selector are referred to as children. The former selector is referred to as the parent. This is just like the relationship observed in HTML elements.

```scss
.parent {
  color: blue;
  .child {
    font-size: 12px;
  }
}
```

The above SCSS would compile to the following CSS:

```css
.parent {
  color: blue;
}

.parent .child {
  font-size: 12px;
}
```

You can also nest properties:

```scss
.parent {
  font: {
    family: Roboto, sans-serif;
    size: 12px;
    decoration: none;
  }
}
```

Would compile to:

```css
.parent {
  font-family: Roboto, sans-serif;
  font-size: 12px;
  font-decoration: none;
}
```

### Variables
Variables in SCSS allow you to assign an identifier of your choice to a specific value.

```scss
$translucent-white: rgba(255,255,255,0.3);
```

You can also assign data types to variables like numbers, strings, booleans, or null.

In addition, SCSS has lists and maps. Lists are separated by either spaces or commas; maps are key-value pairs in parens (similar to an object).

```scss
1.5em Helvetica bold; // list
Helvetica, Arial, sans-serif; //list

(key1: value1, key2: value2); //map
```

By default, variables are only available within the level of nested selectors where they're defined. If they're defined outside of any nested selectors, they're available everywhere. They can also be defined with the `!global` flag to make them available everywhere.

### `@content` Directive
It is possible to pass a block of styles to the mixin for placement within the styles included by the mixin. The styles will appear at the location of any @content directives found within the mixin.

```scss
$color: white;
@mixin colors($color: blue) {
  background-color: $color;
  @content;
  border-color: $color;
}

.colors {
  @include colors { color: $color; }
}
```

### Parent Selector
The `&` character is known as the parent selector. It is used when nesting multiple selectors. It is particularly useful when using pseudo classes or appending `__element` or `--modifier` classes to a base class.

```scss
.button {
  &:hover {
  }
}
```

### Mixins
Mixins let you make groups of CSS declarations that you want to reuse throughout your site. Mixins also can take in a paramater. When you pass in a value to the mixin, it will be applied everywhere.

```scss
@mixin backface-visibility($visibility) {
  backface-visibility: $visibility;
  -webkit-backface-visibility: $visibility;
  -moz-backface-visibility: $visibility;
  -ms-backface-visibility: $visibility;
  -o-backface-visibility: $visibility;
}

.notecard {
  .front, .back {
    width: 100%;
    height: 100%;
    position: absolute;

    @include backface_visibility(hidden);
  }
}
```

Optionally, you can give a mixing a default value to be applied, if no value is passed in later.

```scss
@mixin backface-visibility($visibility: hidden) {

}

@include backface_visibility;
```

Mixins can take multiple arguments with and without defaults. 

```scss
@mixin dashed-border($width, $color: #FFF) {
  border: {
     color: $color;
     width: $width;
     style: dashed;
  }
}

div {
  @include dashed-border(3px, green);
}
```

Mixins can take arguments as a list or map as well. This makes it easy to update styles in the future.

```scss
@mixin stripes($direction, $width-percent, $stripe-color, $stripe-background: #FFF) {
  background: repeating-linear-gradient(
    $direction,
    $stripe-background,
    $stripe-background ($width-percent - 1),
    $stripe-color 1%,
    $stripe-background $width-percent
  );
}

/* map */
$college-ruled-style: ( 
  direction: to bottom,
  width-percent: 15%,
  stripe-color: blue,
  stripe-background: white
);

.definition {
  width: 100%;
  height: 100%;
  @include stripes($college-ruled-style...);
 }
```

You can also use `&` with mixins.

```scss
@mixin text-hover($color) {
  &:hover {
    color: $color; 
  }
}

@include text-hover(red);
```

### String Interpolation
String Interpolation is the process of placing a variable string in the middle of two other strings. Interpolation is useful when you want to make use of variables in selectors or file names. 

```scss
@mixin photo-content($file) {
  content: url('#{$file}.jpg');
  object-fit: cover;
}

.photo { 
  @include photo-content('profile');
  width: 60%;
  margin: 0px auto; 
}
```

### Functions
Functions can perform arithmetic or use built-in functions. All functions must include a return value.

```scss
@function double($value) {
  @return $value * 2;
}
```

### Built-in Functions
Sass includes a number of built-in functions (not limited to):

`fade-in()` changes a color by increasing its opacity by a given percentage.

`fade-out()` changes a color by decreasing its opacity by a given percentage.

`lighten()` changes a color by lightening it by a given percentage.

`darken()` changes a color by darkening it by a given percentage.

`complement()` finds the complementary color on the color spectrum.

`desaturate()` desaturates a color by a given percentage.

`percentage()` converts a unitless number to a percentage.

`variable-exists()` returns whether a variable with the given name exists in the current scope.

`map-get()` is used to retrieve values from a map.

```scss
$palettes: (
  black: (
    light: lighten($black, 10%),
    base: $black,
    dark: darken($black, 10%)
  )
);

map-get(map-get($palettes, black), light);
```

You can also use arithmetic operators `+`, `-`, `*`, `/`, and `%`.

### Loops
Each-loops in Sass iterate on each of the values in a list. 

```scss
$list: (orange, purple, teal);

@each $item in $list {
  .#{$item} {
    background: $item;
  }
}
```

For-loops in Sass can be used to style numerous elements or assigning properties all at once. 

```scss
$total: 10;

@for $i from 1 through $total {
  .ray:nth-child(#{$i}) {
    background: blue;
  }
}

.ray {
  height: 30px;
}
```

### Conditionals
In Sass, `if()` can branch one of two ways based on a condition. It can be used in-line to assign the value of a property. You can also add branches using `@else if` and `@else`.

```scss
@mixin deck($suit) {
  @if($suit == hearts || $suit == spades){
    color: blue;
  }
  @else if($suit == clovers || $suit == diamonds){
   color: red;
  }
  @else{
   //some rule
  }
}
```

### Extend
`@extend` will apply the rules of one class to another, without needing to have both classes in the HTML element.

```scss
.lemonade {
  border: 1px yellow;
  background-color: #fdd;
}

.strawberry {
  @extend .lemonade;
  border-color: pink;
}
```

### Placeholders
Placeholders are classes created solely for extending. Placeholders prevent rules from being rendered unless they are extended. Placeholders are defined by the `%` prefix.

```scss
 %drink {
  font-size: 2em;
  background-color: $lemon-yellow;
 }

 .lemonade {
  @extend %drink;
 }
```

### `@warn` and `@error`
You can display error messages in your console or even in the browser using `@warn` and `@error`.

### Sustainable Sass
In addition to having a solid file structure, a big part of staying organized is splitting up the logic into smaller manageable components, called partials.

Partials are the files you split up to organize specific functionality in the codebase. Partials use a `_` prefix notation in the filename to tell Sass to hold off on compiling the file individually and instead wait for it to be imported into the main style sheet. To import a partial into the main file, omit the underscore. 

Sass extends the `@import` rule to allow including other SCSS and Sass files.

All imported SCSS files are imported into a main SCSS file which is then compiled to a single CSS file.

### BEM Pattern
**BEM:** Block, Element, Modifier. 

First define the block class, then the element class, then the modifier class.

`$block`

`$block__element`

`$block__element--modifier`

### SMACSS
SMACSS is a style guide that helps organize and structure CSS for projects on any scale. The core of SMACSS is categorization. There are five types of categories:

**Base:** Base rules are the defaults. They are almost exclusively single element selectors, but could include attribute selectors, pseudo-class selectors, child selectors, or sibling selectors.

**Layout:** Layout rules divide the page into sections. Layouts hold one or more modules together. 

**Module:** Modules are the reusable, modular parts of our design. They are the callouts, sidebar sections, lists, etc.

**State:** State rules are ways to describe how our modules or layouts look when in a particular state (hidden vs expanded, active vs inactive, etc). 

**Theme:** Theme rules are similar to state rules in that they describe how modules or layouts look. Note: most sites don't require a theme layer.

### Sass Frameworks
**Bootstrap 4:** Bootstrap originally consisted of a series of Less stylesheets that implemented various components. Bootstrap 4 has moved to an updated grid system using Sass.

**Foundation:** A mobile-first, responsive front-end framework built with Sass/SCSS. Through the use of Sass mixins, Foundation components are easily styled and extended.

**Compass:** Compass is a CSS authoring framework written in Ruby using Sass. It is maintained by Chris Epstein, one of the maintainers of Sass.

**Bourbon:** Bourbon is a mixin library for Sass. Bourbon also includes the Neat library, which is a Sass grid system; Bitters, a scaffolding library; and Refills, a component library.  
