## Using Styled Components with Rollup

I was playing around with Styled Components and so far think it is the easiest way to individually-style your React components. Styled Components uses ES2015's [tagged template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_template_literals) so you can pass a multiline string full of plain CSS rules to the `styled` factory function like so:

```
import styled from 'styled-components';

const Div = styled.div`
  background: blue;
  color: white;
`;
```

This returns a React component that renders a `<div>`, and assigns a random `className` to it. The styles for the class will be injected into a `<style>` tag in the `<head>` of the DOM.  

You can use any CSS you want - including `::before` and `::after` pseudo elements, as well as `keyframes` animations (the latter requiring an easy to use helper method).  

Styled Components also allows you to inject global styles into the DOM, which is useful for `font-face`, `html`, and `body` rules, using the `injectGlobal` helper method, like so:

```
import styled, { injectGlobal } from 'styled-components';

injectGlobal`
  html {
    height: 100vh;
  }
  body {
    height: 100%;
    font-size: 1rem;
  }
`;
```

Sounds good right? Everything worked great when using a simple Webpack config:

```
const path = require('path');
const BabiliPlugin = require('babili-webpack-plugin');

const babili = new BabiliPlugin({}, { comments: false });

module.exports = {
  entry: path.join(__dirname, 'source', 'jsx', 'index.jsx'),
  module: {
    rules: [
      {
        test: /.jsx?$/,
        loader: 'babel-loader',
        exclude: /node_modules/,
        query: {
          presets: 'react',
          plugins: ['external-helpers', 'styled-components']
        }
      }
    ]
  },
  plugins: [babili],
  devtool: 'source-map',
  output: {
    path: path.join(__dirname, 'build'),
    filename: 'bundle.min.js'
  }
};
```

My bundle was about 900kb before minification, and 265kb after (90kb gzipped). I then wanted to try Rollup, as I was interested in seeing how it compared to Webpack. Here is my config:

```
import replace from 'rollup-plugin-replace';
import nodeResolve from 'rollup-plugin-node-resolve';
import commonJS from 'rollup-plugin-commonjs';
import babel from 'rollup-plugin-babel';
import babili from 'rollup-plugin-babili';

export default {
  entry: 'source/jsx/index.jsx',
  dest: 'build/bundle.min.js',
  plugins: [
    replace({
      'process.env.NODE_ENV': JSON.stringify('production')
    }),
    nodeResolve({
      jsnext: true
    }),
    commonJS({
      namedExports: {
        'node_modules/react/react.js': ['Component', 'createElement'],
        'node_modules/react-dom/index.js': ['render'],
        'node_modules/styled-components/lib/index.js': ['injectGlobal', 'keyframes']
      }
    }),
    babel({
      exclude: 'node_modules/**',
      presets: ['react'],
      plugins: ['external-helpers', 'styled-components']
    }),
    babili({
      comments: false
    })
  ],
  format: 'iife',
  sourceMap: true
};
```

Rollup's bundle came in at just under 600kb, and only 180kb after minification. Even in `development` mode, they were still 10% smaller than Webpack. Pretty cool.  

In order to get Styled Components `injectGlobal` to work, I had to wrap it in an anonymous function that was exported, import it so Rollup would know it wasn't dead code, then invoke it:

`Global.jsx`

```
import { injectGlobal } from 'styled-components';

export default function () {
  injectGlobal`
    // css
  `
}
```

`index.jsx`

```
import Global from './Global.jsx';

Global();
```

This did the trick. Although, since I started writing this Gist, I've started using Rollup to simply inject the CSS to a `<style>` tag at the top of the page (essentially the same thing as Styled Components `injectGlobal`).  

Either way, the take home for me is that both Rollup and Styled Components are great tools to add to your kit when working with React.  

The end.  
