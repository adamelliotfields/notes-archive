# TypeScript Testing with React 16, Jest, and Enzyme 3

These are the steps required to start using the latest versions of React and Enzyme. Note that I'm
using Babel in addition to TypeScript using `awesome-typescript-loader` in Webpack. If you're not
using Babel, you can omit `.babelrc` and adjust your `tsconfig.json` and `jest.config.json`
accordingly.

You can download a working demo [here](https://github.com/adamelliotfields/react-typescript-webpack-babel-demo).

### Install

```json
{
  "dependencies": {
    "react": "^16.0.0",
    "react-dom": "^16.0.0"
  },
  "devDependencies": {
    "@types/enzyme": "^2.8.9",
    "@types/jest": "^21.1.1",
    "@types/react": "^16.0.7",
    "@types/react-dom": "^15.5.5",
    "babel-preset-react-latest": "^6.0.0",
    "enzyme": "^3.0.0",
    "enzyme-adapter-react-16": "^1.0.0",
    "jest": "^21.2.1",
    "raf": "^3.4.0",
    "react-test-renderer": "^16.0.0",
    "ts-jest": "^21.0.1",
    "typescript": "^2.5.3",
  }
}
```

### `tsconfig.json`

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "jsx": "preserve",
    "moduleResolution": "node",
    "allowSyntheticDefaultImports": true
  }
}
```

### `.babelrc`

*You can use any Babel presets or plugins that transpile ESNext and JSX here.*

```json
{
  "presets": ["react-latest"]
}
```

### `jest.setup.ts`

*This needs to be a .ts file as we're using `ts-jest` instead of `babel-jest`.*

```typescript
// React 16 will throw a warning that RequestAnimationFrame must be polyfilled
import 'raf/polyfill';

import { configure } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

configure({ adapter: new Adapter() });
```

### `jest.config.json`

```json
{
  "setupFiles": ["<rootDir>/jest.setup.ts"],
  "testMatch": ["**/?(*.)(spec|test).ts?(x)"],
  "globals": {
    "ts-jest": {
      "useBabelrc": true
    }
  },
  "transform": {
    "^.+\\.tsx?$": "<rootDir>/node_modules/ts-jest/preprocessor.js",
    "^.+\\.(css|scss|less)$": "<rootDir>/test/transforms/styleTransform.js",
    "^.+\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$": "<rootDir>/test/transforms/fileTransform.js"
  },
  "moduleFileExtensions": [
    "js",
    "jsx",
    "json",
    "ts",
    "tsx"
  ]
}
```

### `test/transforms/fileTransform.js`

*Mock any file imports, e.g., `import logo from './logo.svg'`*

```javascript
const path = require('path');

module.exports = {
  process: (src, filename, config, options) => `module.exports = ${JSON.stringify(path.basename(filename))};`
};
```

### `test/transforms/styleTransform.js`

*Mock any stylesheet imports, e.g., `import './App.css'`*

```javascript
module.exports = {
  process: () => 'module.exports = {};',
  getCacheKey: () => 'styleTransform'
};
```
