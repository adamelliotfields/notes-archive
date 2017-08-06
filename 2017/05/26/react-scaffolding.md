# React Scaffolding
These are the resulting folder structures when using [Create React App](https://github.com/facebookincubator/create-react-app), [React Starter Kit](https://github.com/kriasoft/react-starter-kit), and [MERN.io](https://github.com/Hashnode/mern-starter).  

### Create React App

```text
root
├── build   # Compiled JavaScript and CSS
├── config  # Webpack configs, polyfills, and other settings
├── public  # Static assets
├── scripts # Build, start, and test scripts
└── src     # Pre-compiled JavaScript and CSS
```

### React Starter Kit

```text
root
├── build           # The folder for compiled output
├── docs            # Documentation files for the project
├── public          # Static files which are copied into the /build/public folder
├── src             # The source code of the application
│   ├── components  # React components
│   ├── data        # GraphQL server schema and data models
│   └── routes      # Page/screen components along with the routing information
├── test            # Unit and end-to-end tests
└── tools           # Build automation scripts and utilities
    └── lib         # Library for utility snippets
```

### MERN.io

```text
root
├── client           # Client directory contains all the shared components, routes, and modules
|   ├── components
|   ├── modules
|   └── util
└── server           # Express app sits in server/server.js
    ├── controllers
    ├── models
    ├── routes
    └── util
```
