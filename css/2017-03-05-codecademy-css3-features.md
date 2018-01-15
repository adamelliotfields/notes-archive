# Codecademy CSS3 Features
CSS3 is the latest version of CSS and contains a number of exciting, new features that make it easier for web developers to create great styling for websites.

### `REM` VALUES
You will encounter rem values as you learn about the CSS font-size property, and other CSS properties that specify element size. In the case of the font-size property, a rem value displays a font-size relative to the font-size of the *root* element, called simply `html`.

For example, consider the following CSS:

```css
html {
  font-size: 20px;
}

p {
  font-size: 0.75rem;
}
```

In the code, `font-size` is set to `20px` for the `html` selector. The `p` selector has a `font-size` of `0.75rem`, which displays a size 2/3 that of `html`, or `15px`.

### FLEXBOX
The CSS3 flexbox feature makes it much easier for web developers to arrange HTML elements vertically or horizontally. Website layouts designed with flexbox can respond to users with various screen widths, including mobile devices. To access the feature in CSS, the display property must be set to flex, as seen below:

```css
.main {
  display: flex;
}
```

HTML elements that are children of an element with the "main" class are now flex items and can be arranged using flexbox properties. Here two such such properties:
 - `flex-wrap`: arranges flex items into a single line or wraps them across multiple lines of a webpage layout.
 - `justify-content`: can orient flex items in a number of different positions on a webpage, including the center.

Interested in learning more about flexbox? [Here is a great supplemental resource](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes).

### `BACKGROUND-IMAGE`
The CSS3 background-image property is used to set a background image for an HTML element.

For example, consider the following CSS:

```css
body {
  background-image: url("http://image-gallery.io/mountain-scene.png");
}
```

### `BACKGROUND-SIZE`
The CSS background-size property controls the size of an HTML element's background image. Used along with the background-image property, background-size values control how a background image is proportioned and scaled. One such value is *cover* as seen in the following CSS:

```css
body {
  background-image: url("http://image-gallery.io/mountain-scene.png");
  background-size: cover; 
}
```

Here, the image covers the entire HTML body element.
