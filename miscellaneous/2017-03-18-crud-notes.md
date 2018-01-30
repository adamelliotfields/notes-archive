# CRUD
> :calendar: *March 18, 2017*

There are 4 main database operations:
 - CREATE
 - READ
 - UPDATE
 - DELETE

### CREATE
*PostgreSQL*

`CREATE DATABASE database_name` will create a new database.

`CREATE TABLE table_name(column_names)` will create a new table with the specified columns.

`INSERT INTO table_name VALUES(value_names)` will create a new row with the speciifed values for each column.

*MongoDB*

`use db` creates a database (db is the name of the database).

`db.createCollection()` creates a collection with specified options; if you are not specifying options, you do not need to explicitly create a collection as Mongo will create a collection automatically when first inserting a document.

`db.collection.insertOne()` inserts a single document into a collection.

`db.collection.insertMany()` inserts an array of documents into a colletion.

### READ
*PostgreSQL*

`SELECT column_names FROM table_name` returns all rows with the specified columns from a table.

*MongoDB*

`db.collection.find()` queries a collection for documents matching the query criteria.

### UPDATE

*PostgreSQL*

`UPDATE table_name SET column_name=value WHERE id=value` sets a new value to a specific cell. Value must be in single-quotes for text.

*MongoDB*

`db.collection.updateOne()` updates a single document in a collection.

`db.collection.updateMany()` updates multiple documents in a collection.

`db.collection.replaceOne()` replaces a single document in a collection.

### DELETE

*PostgreSQL*

`DELETE FROM table_name WHERE id=value` deletes a row from the specified table.

*MongoDB*

`db.collection.deleteOne()` deletes a single document from a collection.

`db.collection.deleteMany()` deletes multiple documents from a collection.
