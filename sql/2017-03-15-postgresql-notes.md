# PostgreSQL Notes

### Install PostgreSQL

```bash
brew install postgresql
```

### Setting PGDATA in PATH
Setting PGDATA tells the database server where the data directory is.

```bash
export PGDATA = /usr/local/var/postgres
```

### Create a Database Cluster
A database cluster is a database storage area on disk. It is a collection of databases that is managed by a single instance of a running database server. After initialization, a database cluster will contain a database named `postgres`, which is the default database. The `template1` database is also created during initialization to be used as a template for creating future databases. 

In file system terms, a database cluster is a directory under which all data will be stored (called the data directory). 

```bash
initdb --pgdata
```

### Starting and Stopping the PostgreSQL Server
Before anyone can access the database, you must start the database server. The database server program is called `postgres`.

```bash
postgres
pg_ctl stop -m smart
```

You can also stop the `postgres` process by pressing `CTRL-C`. Alternatively, you can use Homebrew to start and stop the server.

```bash
brew services start postgres
brew services stop postgres
```

### PostgreSQL Interactive Terminal
`psql` is a terminal frontend to PostgreSQL. The default database it will connect to is `username`, unless a specific database name is given. 

`\c` or `\connect`: establishes a new connection to the PostgreSQL server.

`\d`: shows all columns, their types, the tablespace (if not the default) and any special attributes such as NOT NULL or defaults.

`\i` or `\include`: reads input from a file and executes it. 

`\l` or `\list`: list the databases in the server and show their names, owners, character set encodings, and access privileges.  

### Creating a Database
A second database, `template1`, is also created during database cluster initialization. Whenever a new database is created within the cluster, `template1` is essentially cloned. This means that any changes you make in template1 are propagated to all subsequently created databases. Because of this, avoid creating objects in template1 unless you want them propagated to every newly created database.

```sql
CREATE DATABASE database_name;
```

### Importing a CSV

```sql
CREATE TABLE table_name(column_names);

COPY table_name(column_names)
FROM '/path/to/csv.csv' CSV HEADER;
```

The `HEADER` keyword tells PostgreSQL to skip the first line in the CSV which is usually a header. 

By default, the delimiter is a comma when copying from CSV files.

Wrap any values that include commas in double-quotes.

Specifying column names is optional, but useful when you want the first column to be an automatically incrememnted sequence, for example.

### Exporting to a SQL File

```bash
pg_dump -d database_name -t table_name > /path/to/file.sql
```

### Show Columns

```sql
SELECT * FROM table_name WHERE false;
```

Or:

```sql
\d table_name
```

Or to see columns and their datatypes:

```sql
\d+ table_name
```

### Quoted Identifer
When using Aliases, you must wrap them in double-quotes. This is also known as a delimited identifier.

```sql
SELECT title AS "Title" FROM books;
```

### Functions
`CREATE FUNCTION` defines a new function.

```sql
CREATE FUNCTION add_contact(_name TEXT, _phone BIGINT, _email TEXT)
RETURNS void AS
$$
BEGIN
INSERT INTO contacts(name, phone, email)
    VALUES(_name, _phone, _email);
END;
$$
LANGUAGE plpgsql;
```

`SELECT function(params)` calls the function.

`\df` shows a list of all functions.

`DROP FUNCTION function(params)` deletes the function.

`CREATE OR REPLACE FUNCTION` will replace a function if it already exists.
