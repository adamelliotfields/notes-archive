# Express Scaffolding
This is the resulting folder structure when using the Express Generator.

```
root
├── bin
|   └── www.js
├── public
|   ├── images
|   ├── javascripts
|   └── stylesheets
├── routes
├── views
└── app.js
```

All routes are defined separately in the `routes` directory by creating a new `express.Router()` object.  

All routes, middleware and view engines are mounted in `app.js`.  

The server is started in `bin/www.js` by passing `app` to `http.createServer()`.  
