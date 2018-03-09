# Sequelize with SQLite3 Notes
> :calendar: *March 8, 2018*

> I'm just starting to learn sequelize. First 11 lines of code and I am searching issues??? - [@grantcarthew](https://github.com/grantcarthew)

These are some quick notes on getting started with Sequelize using a SQLite3 database. I'm
definitely more of a Mongo/Redis guy, so I'm trying to brush up on my SQL. Unfortunately, the
Sequelize docs leave much to be desired...

### Installation

```bash
# Install the Sequelize CLI globally as you don't need it in your application
npm install --global sequelize-cli

# You must have SQLite3 installed on your system:
#   Windows: scoop install sqlite
#   Mac:     brew install sqlite3
#   Ubuntu:  sudo apt-get install sqlite3
yarn add sequelize sqlite3
```

### Bootstrapping with Sequelize CLI

This creates the `config`, `models`, `migrations`, and `seeders` folders in the directory you run
command in. I'd recommend keeping these in the project root.

```bash
sequelize init
```

### Create Databases

You'll want to create *development*, *test*, and *production* databases. Sequelize can do this for
you if you're using a database server like MySQL or Postgres, but for SQLite3 you'll have to create
the database files yourself.

```bash
# Create the data folder
mkdir data && cd data

# Create the databases
touch database_development.db
touch database_test.db
touch database_production.db
```

### Edit Sequelize CLI Configuration

`sequelize init` created a `config.json` file in the `config` folder.

We just need to tell Sequelize the dialect, the paths to our databases, and that we want to store
our seed files in the database.

Because we aren't connecting to a database server, we don't need things like username, password, IP
address, port, etc.

Note that the path is relative to where the `sequelize` commands are run. In this example, we are
running them in the project root.

Also note that Sequelize uses the `NODE_ENV` environmental variable, so for production you'll want
to make sure you use `NODE_ENV=production` when running your app. By default, Sequelize will use the
*development* database.

```json
{
  "development": {
    "dialect": "sqlite",
    "storage": "data/database_development.db",
    "seederStorage": "sequelize"
  },
  "test": {
    "dialect": "sqlite",
    "storage": "data/database_test.db",
    "seederStorage": "sequelize"
  },
  "production": {
    "dialect": "sqlite",
    "storage": "data/database_production.db",
    "seederStorage": "sequelize"
  }
}
```

### Creating a Model and Migration

Models are the object mappings of your tables. In Java, this would be an Entity Class.

The migration will be used to create the schema (the column names and data types) for our table.
I'll be using a `Posts` table to represent a blog post.

Note that Sequelize will automatically create the `id`, `createdAt`, and `updatedAt` fields in the
migration.

I want to use `moment().toString()` for my dates, and `shortid()` for my IDs, so we'll update the
model and migration files manually.

```bash
# Change directory if you're still in data/
cd ..

sequelize model:generate \
--name Post \
--attributes id:string,title:string,body:text,createdAt:string,updatedAt:string
```

```javascript
// Migration
'use strict';

module.exports = {
  up: (queryInterface, Sequelize) => {
    return queryInterface.createTable('Posts', {
      id: {
        allowNull: false,
        // We don't need to auto-increment
        // autoIncrement: true,
        primaryKey: true,
        // Change this to STRING
        type: Sequelize.STRING
      },
      title: {
        type: Sequelize.STRING
      },
      body: {
        type: Sequelize.TEXT
      },
      createdAt: {
        allowNull: false,
        // Change this to STRING
        type: Sequelize.STRING
      },
      updatedAt: {
        allowNull: false,
        // Change this to STRING
        type: Sequelize.STRING
      }
    });
  },
  down: (queryInterface, Sequelize) => {
    return queryInterface.dropTable('Posts');
  }
};
```

```javascript
// Model
'use strict';

module.exports = (sequelize, DataTypes) => {
  var Post = sequelize.define('Post', {
    id: DataTypes.STRING,
    title: DataTypes.STRING,
    body: DataTypes.TEXT,
    createdAt: DataTypes.STRING,
    updatedAt: DataTypes.STRING
  }, {});

  Post.associate = (models) => {
    // associations can be defined here
  };

  return Post;
};
```

### Running a Migration

The migration will create the table using the schema from our model.

```bash
sequelize db:migrate
```

This runs the equivalent SQL:

```sql
CREATE TABLE Posts (
  id VARCHAR(255) NOT NULL PRIMARY KEY,
  title VARCHAR(255),
  body TEXT,
  createdAt VARCHAR(255) NOT NULL,
  updatedAt VARCHAR(255) NOT NULL
);
```

### Creating a Seed

Seeds are used to populate an empty table, so you don't have to manually `INSERT INTO`.

```bash
sequelize seed:generate \
--name post
```

This will generate a seed skeleton. We'll need to manually edit this in a text editor.

```javascript
'use strict';

const shortid = require('shortid');
const moment = require('moment');

module.exports = {
  up: (queryInterface, Sequelize) => {
    // Add altering commands here.
    // Return a promise to correctly handle asynchronicity.
    return queryInterface.bulkInsert('Posts', [{
      id: shortid(),
      title: 'Welcome',
      body: 'Hello World!',
      createdAt: moment().toString(),
      updatedAt: moment().toString()
    }], {});
  },

  down: (queryInterface, Sequelize) => {
    // Add reverting commands here.
    // Return a promise to correctly handle asynchronicity.
    return queryInterface.bulkDelete('Posts', null, {});
  }
};
```

### Running the Seed

```bash
sequelize db:seed:all
```

### Inspecting the Database

```bash
sqlite3 data/database_development.db
```

```sql
SELECT * FROM Posts;
```

| id        | title   | body         | createdAt                         | updatedAt                         |
|-----------|---------|--------------|-----------------------------------|-----------------------------------|
| SyEoDu1Yz | Welcome | Hello World! | Fri Mar 09 2018 00:35:17 GMT-0500 | Fri Mar 09 2018 00:35:17 GMT-0500 |

### Express Example

```javascript
const Express = require('express');
const Sequelize = require('sequelize');

const app = Express();

const sequelize = new Sequelize({
  dialect: 'sqlite',
  storage: 'data/database_development.db'
});

// The model exports a function that takes the Sequelize instance and class as arguments
// The Sequelize class is needed for the static DataType fields used in the model
const Post = require('./models/post')(sequelize, Sequelize);

app.get('/posts', async (request, response) => {
  // Use the raw option to return only the results array
  const posts = await Post.findAll({ raw: true });

  response.json({ posts });
});

app.get('/posts/:id', async (request, response) => {
  const id = request.params.id;
  const post = await Post.findOne({
    where: { id }
  });

  response.json({ post });
});

app.listen(8080, () => {
  console.log('Server listening at http://127.0.0.1:8080 ...');
});
```

```bash
# Pipe to jq to pretty-print JSON
curl http://127.0.0.1:8080/posts | jq .

{
  "posts": [
    {
      "id": "SkpfTqkYz",
      "title": "Welcome",
      "body": "Hello World!",
      "createdAt": "Fri Mar 09 2018 00:35:17 GMT-0500",
      "updatedAt": "Fri Mar 09 2018 00:35:17 GMT-0500"
    }
  ]
}
```

```bash
curl http://127.0.0.1:8080/posts/SyEoDu1Yz | jq .

{
  "post": {
    "id": "SkpfTqkYz",
    "title": "Welcome",
    "body": "Hello World!",
    "createdAt": "Fri Mar 09 2018 00:35:17 GMT-0500",
    "updatedAt": "Fri Mar 09 2018 00:35:17 GMT-0500"
  }
}
```

There's more to Sequelize, especially writing data, but this is enough to get started.
