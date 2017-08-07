# SQL Notes
SQL, 'Structured Query Language', is a programming language designed to manage data stored in relational databases. SQL operates through simple, declarative statements. This keeps data accurate and secure, and helps maintain the integrity of databases, regardless of size.

The SQL language is widely used today across web frameworks and database applications. Knowing SQL gives you the freedom to explore your data, and the power to make better decisions. By learning SQL, you will also learn concepts that apply to nearly every data storage system.

### RDBMS
A relational database management system (RDBMS) is a program that lets you create, update, and administer a relational database. Most relational database management systems use SQL to access the database.

There are more similarities than differences between the different RDBMS, but the SQL syntax may be slightly different depending on which RDBMS you are using.

A relational database is a database that organizes information into one or more tables.

A table is a collection of data organized into rows and columns. Tables are sometimes referred to as relations.
 
A column is a set of data values of a particular type.

A row is a single record in a table.

### Data Types
All data stored in a relational database is of a certain data type. Some of the most common data types are:

 - `INT`: a positive or negative whole number 
 - `TEXT`: a text string
 - `VARCHAR`: a variable character field
 - `DATE`: the date formatted as YYYY-MM-DD for the year, month, and day 
 - `DATETIME`: the date and time formatted as YYYY-MM-DD hh:mm:ss
 - `TIMESTAMP`: the date and time with timezone
 - `REAL`: a decimal value
 - `NULL`: a special value that represents missing or unknown data

### PRIMARY KEY
A primary key is a unique identifier for each row in a given table. By specifying the primary key, SQL makes sure that none of the values are `NULL` and each value in the column is unique.

```sql
CREATE TABLE table_name(id INTEGER PRIMARY KEY, name TEXT);
```

### Foreign Key
A foreign key is a column that contains the primary key of another table in the database. Use foreign keys and primary keys to connect rows in different tables. 

### Statements
A statement is text that the database recognizes as a valid command. Statements always end in a semi-colon, `;`.

```sql
CREATE TABLE table_name (
    column_id data_type
  );
```

`CREATE TABLE` is a clause. Clauses perform specific tasks in SQL. By convention, clauses are written in capital letters. Clauses can also be referred to as commands.

`table_name` refers to the name of the table that the command is applied to.

`(column_id data_type)` is a parameter. A parameter is a list of columns, data types, or values that are passed to a clause as an argument.

### INSERT
The `INSERT` statement inserts new rows into a table. You can use the `INSERT` statement when you want to add new records.

```sql
INSERT INTO table_name (column_id) VALUES (value)
```

`INSERT INTO` is a clause that adds the specified row or rows.

`table_name` is the name of the table the row is added to.

`(column_id)` is a parameter identifying the column(s) that data will be inserted into.

`VALUES` is a clause that indicates the data being inserted.

`(value)` is a parameter identifying the value(s) being inserted. You can insert multiple rows by separating each tuple with a comma.

### SELECT
`SELECT` statements are used to fetch data from a database.

`SELECT` is a clause that indicates that the statement is a query. You will use `SELECT` every time you query data from a database.

`FROM` specifies the name of the table to query data from.

`*` is a special wildcard character. It allows you to select every column in a table without having to name each one individually. 

`SELECT` statements always return a new table called the result set.

Multiple columns can be queried at once by separating column names with a comma.

### DISTINCT
`DISTINCT` is used to return values in the result set. It filters out all duplicate values.

### UPDATE
The `UPDATE` statement edits a row in the table. You can use the `UPDATE` statement when you want to change existing records. 

```sql
UPDATE table_name
SET column = value;
WHERE id = column_id;
```

`UPDATE` is a clause that edits a row in the table.

`table_name` is the name of the table.

`SET` is a clause that indicates the column to edit.

`column` is the name of the column that's going to be updated.

`value` is the new value that is going to be inserted into the `column`.

`WHERE` is a clause that indicates which row(s) to update.

### ALTER TABLE
The `ALTER TABLE` statement adds a new column to the table. You can use this command when you want to add columns to a table.

```sql
ALTER TABLE table_name ADD COLUMN column_name TEXT;
```

`ALTER TABLE` is a clause that lets you make the specified changes.

`table_name` is the name of the table that's being changed.

`ADD COLUMN` is a clause that lets you add a new column to a table.

`column_name` is the name of the new column being added.

`TEXT` is the data type for the new column. 

### DELETE FROM
The `DELETE FROM` statement deletes one or more rows from a table. You can use the statement when you want to delete existing records.

```sql
DELETE FROM table_name WHERE column_name IS NULL;
```

`DELETE FROM` is a clause that lets you delete rows from a table.

`table_name` is the name of the table we want to delete rows from. 

`WHERE` is a clause that lets you select which rows you want to delete.

`IS NULL` is a condition that returns true when the value is NULL, and false otherwise.

## ACID
ACID stands for Atomicity, Consistency, Isolation, Durability. A sequence of database operations that satisfies ACID compliance is a transaction.

PostgreSQL is ACID compliant by default.

MySQL has multiple different storage engines, but only InnoDB is ACID compliant.

**Atomicity:** Each transaction is all-or-nothing. If one part of the transaction fails, then the entire transaction fails, and the database state is left unchanged.

**Consistency:** Any transaction will bring the database from one valid state to another. Any data written to the database must be valid according to defined rules.

**Isolation:** The concurrent execution of transactions results in a system state that would be obtained if transactions were executed sequentially.

**Durability:** Once a transaction has been committed, it will remain even in the event of a power loss, crash, or error.

### Transactions
Transactions are bundles of operations in a single all-or-nothing operation.

By default, PostgreSQL treats every SQL statement as a transaction. However, you can wrap your statements with the `BEGIN;` and `COMMIT;` keywords to define a transaction block.

MySQL, by default, runs in autocommit mode. This means that every statement is written to disk individually. To implicitly disable autocommit, you must wrap your statements with `START TRANSACTION;` and `COMMIT;`. `BEGIN` is an alias for `START TRANSACTION`.

To abort your transaction, use the `ROLLBACK` keyword (can only be used if you did not already `COMMIT`).

### Comparison Operators
Comparison operators create a condition that can be true or false. Common operators used with the `WHERE` clause are:

 - `=`  equals
 - `!=` not equals
 - `>`  greater than
 - `<`  less than
 - `>=` greater than or equal to
 - `<=` less than or equal to

### Mathematical Operators
 - `+`   addition
 - `-`   subtraction
 - `*`   multiplication
 - `/`   division
 - `%`   modulo (remainder)
 - `^`   exponentiation
 - `|/`  square root
 - `||/` cube root
 - `!`   factorial (suffix)
 - `!!`  factorial (prefix)
 - `@`   absolute value

### LIKE
`LIKE` can be a useful operator when you want to compare similar values.

```sql
SELECT * FROM table_name WHERE column_name LIKE 'value';
```

`LIKE` is a special operator used with the `WHERE` clause to search for a specific pattern in a column. 

`column_name LIKE 'value'` is a condition evaluating the `column_name` column for a specific pattern.

### Wildcard Characters
Wildcard characters are used with the `LIKE` operator. They are used to substitute for any other characters in a string. 

 - `%` is a substitute for zero or more characters.
 - `_` is a substitute for a single character.
 - `[charlist]` sets or ranges of characters to match.

### IN
The `IN` operator is used to filter the result set within a set of values.

```sql
SELECT * FROM table_name WHERE column_name IN (value1, value2, value3);
```

### BETWEEN
The `BETWEEN` operator is used to filter the result set within a certain range. The values can be numbers, text, or dates.

```sql
SELECT * FROM table_name WHERE column_name BETWEEN 'value' AND 'value';
```

### AND
The `AND` operator combines multiple conditions in a `WHERE` clause to make the result set more specific.

### OR
The `OR` operator can also be used to combine multiple conditions in a `WHERE` clause. 

### ORDER BY
You can sort the results of your query using `ORDER BY`. 

The `DESC` keyword will sort the results in descending order; the `ASC` keyword will sort the results in ascending order.

```sql
SELECT * FROM table_name ORDER BY column_name DESC;
```

### LIMIT
`LIMIT` is a clause that lets you specify the maximum number of rows of the result set. When using `LIMIT`, it is important to also use `ORDER BY` to constrain the rows to a unique order.

### GROUP BY
`GROUP BY` is a clause in SQL that is only used with aggregate functions. It is used in collaboration with the `SELECT` statement to arrange identical data into groups. 

### HAVING
`HAVING` filters rows created by `GROUP BY`.

This differs from `WHERE`, which filters rows BEFORE being created by `GROUP BY`.

### OFFSET
`OFFSET` tells the database server to skip a specified number of rows before beginning to return rows.

### COUNT()
The `COUNT()` function is the fastest way to calculate the number of rows in a table. `COUNT()` takes the name of a column as an argument or `*` for all rows in a table. 

### LENGTH()
Returns the number of characters in a string.

### Changing Text Case
`UPPER()` changes text to uppercase.

`LOWER()` changes text to lowercase.

### SUBSTR()
`SUBSTR()` is a function that takes the name of a column, the starting position, and the length as arguments and returns a substring.

### SUM()
`SUM()` is a function that takes the name of a column as an argument and returns the sum of all values in that column.

### MAX()
`MAX()` is a function that takes the name of a column as an argument and returns the largest value in that column.

### MIN()
`MIN()` is a function that takes the name of a column as an argument and returns the smallest value in that column.

### AVG()
`AVG()` is a function that takes a column as an argument and returns the average value of that column. 

### ROUND()
`ROUND()` is a function that takes a column name and an integer as an argument. It rounds the values in the column to the decimal place specified by the integer.

### Cross Join
One way to query multiple tables is to write a `SELECT` statement with multiple table names separated by a comma. When querying multiple tables, column names need to be specified using dot notation.

```sql
SELECT albums.name, artists.name FROM albums, artists;
```

### Inner Join
The most common type of join is an inner join, which combines rows from different tables if the join condition is true.

```sql
SELECT * FROM albums INNER JOIN artists ON albums.artist_id = artists.id;
```

`SELECT` specifies the columns our result set will have.

`FROM albums` specifies the first table we are querying.

`INNER JOIN artists ON` specifies the type of join we are going to use as well as the name of the second table.

`albums.artist_id = artists.id` is the join condition that describes how the two tables are related to each other.

### Outer Join
Outer joins combine rows from two or more columns, but they do not require the join condition to be true. Instead, every row in the left table is returned in the result set, and if the join condition is false, `NULL` values are used to fill in the columns on the right table. 

There are three types of outer joins: left, right, and full.

### AS
`AS` is a keyword that allows you to rename a column or table using an alias. The new name must be wrapped in single quotes (double quotes for PostgreSQL).

```sql
SELECT albums.name AS 'Album', artists.name AS 'Artist'
FROM albums
JOIN artists ON albums.artist_id = artists.id;
```

### Non-correlated Subquery
A non-correlated subquery is a subquery that can be run independently of the outer query and used to complete a multi-step transformation. 

We first create an inner query, or subquery, that finds the airports with elevation greater than 2000 from the airports table:

```sql
SELECT code
  FROM airports
  WHERE elevation > 2000;
```

Next, we take the result set of the inner query and use it to filter on the flights table, to find the flight detail that meets the elevation criteria:

```sql
SELECT * 
FROM flights 
WHERE origin IN (
  SELECT code 
  FROM airports 
  WHERE elevation > 2000);
```

You can also use a subquery in a `NOT IN` clause.

### Correlated Subquery
In a correlated subquery, the subquery can not be run independently of the outer query. The order of operations is important in a correlated subquery:

 1. A row is processed in the outer query. 
 2. Then for that particular row in the outer query, the subquery is executed.

```sql
SELECT id
FROM flights AS f
WHERE distance > (
  SELECT AVG(distance)
  FROM flights
  WHERE carrier = f.carrier);
```

### UNION
`UNION` allows you to utilize information from multiple tables in your queries. In a join, you are merging rows; in a union, you are merging columns.

Unions combine the results of two or more `SELECT` statements. Each `SELECT` statement within the union must have the same number of columns with similar data types. The columns in each `SELECT` statement must be in the same order.

To allow duplicate values, use `UNION ALL`.

```sql
SELECT column_name FROM table1
UNION
SELECT column_name FROM table2;
```

### INTERSECT
`INTERSECT` is used to combine two `SELECT` statements, but returns rows only from the first statement that are indentical to a row in the second statement. This means that it only returns common rows returns by the two statements. 

```sql
SELECT column_name FROM table1
INTERSECT
SELECT column_name FROM table2;
```

### EXCEPT
`EXCEPT` is used to return distinct rows from the first `SELECT` statement that aren't output by the second statement.

```sql
SELECT column_name FROM table2
EXCEPT
SELECT column_name FROM table1;
```

### REPLACE()
`REPLACE(column_name,from_string,to_string)` returns the string with all occurences of the string `from_string` replaced by the string `to_string`.

For example:

```sql
SELECT * FROM addresses WHERE REPLACE(state, 'California', 'CA');
```

Returns all results where the state was entered as either `California` or `CA`.

```sql
SELECT street, city, REPLACE(state, 'California', 'CA') AS "state", zip
FROM addresses
WHERE REPLACE(state, 'California', 'CA') = 'CA';
```

Returns the same results as the previous query, but with the state names changed to `CA`.

### Conditional Aggregate Functions
Conditional aggregates are functions that compute a result set based on a given set of conditions.

### IS NULL
Use the `IS NULL` and `IS NOT NULL` keywords in the `WHERE` clause to test whether a value is null or not.

### CASE
`CASE` is used to represent conditional (if/elseif/else) logic in SQL.

```sql
SELECT
    CASE
        WHEN elevation < 500 THEN 'Low'
        WHEN elevation BETWEEN 500 AND 1999 THEN 'Medium'
        WHEN elevation >= 2000 THEN 'High'
        ELSE 'Unknown'
    END AS elevation_tier
    , COUNT(*)
FROM airports
GROUP BY 1;
```

### Dates
Dates are often written in the following format:

 1. Date: YYYY-MM-DD
 2. Timestamp: YYYY-MM-DD hh:mm:ss

### DATETIME
`DATETIME` returns the date and time of the column specified. This can be modified to return only the date or  only the time.

### DATE()
The `DATE()` function returns the date half of a timestamp.

### TIME()
The `TIME()` function returns the time half of a timestamp.

### String Concatenation
The double-pipe `||` operator is used to concatenate strings in PostgreSQL. The `CONCAT()` function is used in MySQL (and can also be used in PostgreSQL).

When adding a space in between words, you must use single-quotes in PostgreSQL; otherwise, PostgreSQL will look for a " " column.
