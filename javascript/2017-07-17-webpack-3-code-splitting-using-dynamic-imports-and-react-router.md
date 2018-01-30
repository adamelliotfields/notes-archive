## Webpack 3 Code Splitting using Dynamic Imports and React Router
> :calendar: *July 17, 2017*

This is a simple example adapted from Hassan Ali's [post](https://hackernoon.com/code-splitting-for-react-router-with-webpack-and-hmr-bb509968e86f) on Hacker Noon.

This example uses `async/await` which requires using [regenerator-runtime](https://github.com/facebook/regenerator/tree/master/packages/regenerator-runtime) as well as the [transform-async-to-generator](https://babeljs.io/docs/plugins/transform-async-to-generator) Babel plugin. Note that this plugin is included in the Stage 3 preset; so if you're using that (or Stage 0, 1, or 2) you'll be all set.

See also:
1. [Webpack Code Splitting](https://webpack.js.org/guides/code-splitting/)
2. [React Router Code Splitting](https://reacttraining.com/react-router/web/guides/code-splitting) (requires [bundle-loader](https://github.com/webpack-contrib/bundle-loader))
3. [react-async-component](https://github.com/ctrlplusb/react-async-component) (useful for code splitting + ssr)
4. [react-router-loader](https://github.com/luqin/react-router-loader)

### 1. Create a component as usual

```javascript
import React from 'react';

const Hello = (props) => <h1 {...props}>Hello World</h1>;

// Important: Don't forget to make it the default export
export default Hello;
```

### 2. Create a Higher Order Component
A higher order component is a function that returns a component. Read more [here](https://facebook.github.io/react/docs/higher-order-components.html).

```javascript
import React, { Component } from 'react';

// The loader parameter is a function that includes our dynamic import
const asyncComponent = (loader) => (
  class AsyncComponent extends Component {
    state = { Component: null };
    
    // Don't forget the async keyword here
    async componentDidMount () {
      const component = await loader();

      this.setState({ Component: component });
    }

    render () {
      const { Component } = this.state;

      if (Component) {
        return <Component {...this.props} />;
      } else {
        // Optional: Render a loading spinner or text on initial mount
        // Return null otherwise
        return <p>Loading...</p>;
      }
    }
  }
);

export default asyncComponent;
```

### 3. Configure your entry file (`index.js`)

```javascript
import 'regenerator-runtime/runtime';
import React from 'react';
import { render } from 'react-dom';
import { BrowserRouter, Switch, Route } from 'react-router-dom';

import asyncComponent from './components/asyncComponent.jsx';
// Home is just a regular component to be bundled normally
import Home from './components/Home.jsx';

const Hello = asyncComponent(async function () {
  // The inline comment below is a Webpack "magic comment" to name our chunk hello.js
  // chunkFilename needs to also be set in your Webpack config
  const module = await import(/* webpackChunkName: 'hello' */ './components/Hello.jsx');
  return module.default;
});

render(
  <BrowserRouter>
    <div>
      // Navbar would go here
      <Switch>
        <Route exact path='/' component={Home} />
        // Use React Router's render attribute to pass props to the component
        <Route path='/hello' render={() => <Hello className='display-4 text-center' />} />
      </Switch>
      // Footer would go here
    </div>
  </BrowserRouter>,
  document.getElementById('root')
);
```

### 4. Configure your Webpack config
Basic Webpack production config. The key things to note here are the usage of chunkhash and chunkFilename. If you don't use a chunkFilename, Webpack will use a number (i.e., `01.js`).

Appending a chunkhash to our filenames will allow for long-term browser caching, and cache busting when the hash changes (if we edit a component).

```javascript
const path = require('path');
const webpack = require('webpack');
const HTMLPlugin = require('html-webpack-plugin');

module.exports = {
  entry: path.join(__dirname, 'src', 'index.js'),
  output: {
    filename: 'js/[name].[chunkhash].js',
    chunkFilename: 'js/[name].[chunkhash].js',
    path: (path.join(__dirname, 'build'))
  },
  devtool: 'source-map',
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel-loader'
      }
    ]
  },
  plugins: [
    new webpack.DefinePlugin({
      'process.env.NODE_ENV': JSON.stringify(process.env.NODE_ENV)
    }),
    new webpack.optimize.ModuleConcatenationPlugin(),
    new webpack.optimize.CommonsChunkPlugin({
      name: 'vendor',
      minChunks: function (module) {
        return module.context && module.context.indexOf('node_modules') !== -1;
      }
    }),
    new webpack.optimize.UglifyJsPlugin({
      comments: false,
      sourceMap: true
    }),
    new HTMLPlugin({
      template: path.join(__dirname, 'src', 'templates', 'index.ejs'),
      filename: 'index.html'
    }),
  ]
};
```

That's it. When going to the home route (`/`), only main.js and vendor.js will be downloaded and executed. When visiting the `/hello` route, Webpack will inject a `<script>` tag with `hello.js` and execute it once it's downloaded.

Since `asyncComponent` is part of the main bundle, the loading text will appear instantly. Because the Hello component is so small, even on slow connections the loading text will be almost inperceivable. You can experiment with throttling in the Chrome Developer Tools Network tab (even on GPRS, you'll still only see the loading text for a split second). For small components, it might be better to use a fade-in keyframe animation.

Note that this is a very simple example, and there are more advanced examples out there. But for a simple single-page app, like your github.io page, this technique will work just fine.
