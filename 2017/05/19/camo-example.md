# Camo Example

### MongoDB

```javascript
const camo = require('camo');

const Document = camo.Document;

// Create the Kitten model and schema
// Creates the 'kittens' collection in the database unless overridden by 'static collectionName'
class Kitten extends Document {
  constructor () {
    super();
    this.name = {
      type: String,
      required: true
    };
  }

  // Override the default collection name
  static collectionName () {
    return 'cats';
  }

  // Pre-validate hook
  // Occurs before Model.create
  preValidate () {
    console.log('Validating data...');
  }

  // Pre-save hook
  // Occurs before document.save
  preSave () {
    console.log('Saving new document...');
  }
}

let db;
(async function () {
  try {
    // Connect to MongoDB database
    db = await camo.connect('mongodb://localhost:27017/camo');
    console.log('Connected to database...');

    // Delete all documents
    await Kitten.deleteMany({});
    
    // Create a new Kitten document
    const fluffy = Kitten.create({ name: 'Fluffy' });

    // Save the fluffy document
    await fluffy.save();

    // Find all documents
    const results = await Kitten.find({});
    console.log('\n' + 'Documents found:');
    console.log(results);

    // Close the database connection
    await db.close();
    console.log('\n' + 'Database connection closed.');

  // Catch errors here
  } catch (err) {
    console.log(err.message);
    await db.close();
  }
}());
```

### NeDB

```javascript
const camo = require('camo');

const Document = camo.Document;

// Create the Kitten model and schema
// Creates 'kittens.db' unless overridden by 'static collectionName'
class Kitten extends Document {
  constructor () {
    super();
    this.name = {
      type: String,
      required: true
    };
  }

  // Override the default collection name
  static collectionName () {
    return 'cats';
  }

  // Pre-validate hook
  // Occurs before Model.create
  preValidate () {
    console.log('Validating data...');
  }

  // Pre-save hook
  // Occurs before document.save
  preSave () {
    console.log('Saving new document...');
  }
}

(async function () {
  try {
    // Connect to NeDB database
    // Creates 'nedb' folder at the project root
    await camo.connect('nedb://nedb');
    console.log('Connected to database...');

    // Delete all documents
    await Kitten.deleteMany({});
    
    // Create a new Kitten document
    const fluffy = Kitten.create({ name: 'Fluffy' });

    // Save the fluffy document
    await fluffy.save();

    // Find all documents
    const results = await Kitten.find({});
    console.log('\n' + 'Documents found:');
    console.log(results);

  // Catch errors here
  } catch (err) {
    console.log(err.message);
  }
}());
```
