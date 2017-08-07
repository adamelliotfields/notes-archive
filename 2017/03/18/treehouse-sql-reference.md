# Treehouse SQL Reference

### Find All Columns and Rows in a Table

```sql
SELECT * FROM <table name>;
```

The asterisk or star symbol (`*`) means all columns.

The semi-colon (`;`) terminates the statement like a period in sentence or question mark in a question.

Examples:

```sql
SELECT * FROM books;
SELECT * FROM products;
SELECT * FROM users;
SELECT * FROM countries;
```

### Retrieving Specific Columns of Information
Retrieving a single column:

```sql
SELECT <column name> FROM <table name>; 
```

Examples:

```sql
SELECT email FROM users;
SELECT first_name FROM users;
SELECT name FROM products;
SELECT zip_code FROM addresses;
```

Retrieving multiple columns:

```sql
SELECT <column name 1>, <column name 2>, ... FROM <table name>;
```

Examples:

```sql
SELECT first_name, last_name FROM customers;
SELECT name, description, price FROM products;
SELECT title, author, isbn, year_released FROM books;
SELECT name, species, legs FROM pets;
```

### Aliasing Column Names

```sql
SELECT <column name> AS <alias> FROM <table name>;
SELECT <column name> <alias> FROM <table name>;
```

Examples:

```sql
SELECT username AS Username, first_name AS "First Name" FROM users;
SELECT title AS Title, year AS "Year Released" FROM movies;
SELECT name AS Name, description AS Description, price AS "Current Price" FROM products;
SELECT name Name, description Description, price "Current Price" FROM products;
```
 
### Finding the Data You Want

```sql
SELECT <columns> FROM <table> WHERE <condition>;
```

### Equality Operator
Find all rows that a given value matches a column's value.

```sql
SELECT <columns> FROM <table> WHERE <column name> = <value>;
```

Examples:

```sql
SELECT * FROM contacts WHERE first_name = "Andrew";
SELECT first_name, email FROM users WHERE last_name = "Chalkley";
SELECT name AS "Product Name" FROM products WHERE stock_count = 0;
SELECT title "Book Title" FROM books WHERE year_published = 1999;
```

### Inequality Operator
Find all rows that a given value doesn't match a column's value.

```sql
SELECT <columns> FROM <table> WHERE <column name> != <value>;
SELECT <columns> FROM <table> WHERE <column name> <> <value>;
```

The not equal to or inequality operator can be written in two ways `!=` and `<>`. The latter is *less* common.

Examples:

```sql
SELECT * FROM contacts WHERE first_name != "Kenneth";
SELECT first_name, email FROM users WHERE last_name != "L:one";
SELECT name AS "Product Name" FROM products WHERE stock_count != 0;
SELECT title "Book Title" FROM books WHERE year_published != 2015;
```

### Relational Operators
There are several relational operators you can use:

 - `<` less than
 - `<=` less than or equal to
 - `>` greater than
 - `>=` greater than or equal to

These are primarily used to compare *numeric* and *date/time* types.

```sql
SELECT <columns> FROM <table> WHERE <column name> < <value>;
SELECT <columns> FROM <table> WHERE <column name> <= <value>;
SELECT <columns> FROM <table> WHERE <column name> > <value>;
SELECT <columns> FROM <table> WHERE <column name> >= <value>;
```

Examples:

```sql
SELECT first_name, last_name FROM users WHERE date_of_birth < '1998-12-01';
SELECT title AS "Book Title", author AS Author FROM books WHERE year_released <= 2015;
SELECT name, description FROM products WHERE price > 9.99;
SELECT title FROM movies WHERE release_year >= 2000;
```

### More Than One Condition
You can compare multiple values in a `WHERE` condition. If you want to test that *both* conditions are true use the `AND` keyword, or *either* conditions are true use the `OR` keyword.

```sql
SELECT <columns> FROM <table> WHERE <condition 1> AND <condition 2> ...;
SELECT <columns> FROM <table> WHERE <condition 1> OR <condition 2> ...;
```

Examples:

```sql
SELECT username FROM users WHERE last_name = "Chalkley" AND first_name = "Andrew";
SELECT * FROM products WHERE category = "Games Consoles" AND price < 400;
SELECT * FROM movies WHERE title = "The Matrix" OR title = "The Matrix Reloaded" OR title = "The Matrix Revolutions";
SELECT country FROM countries WHERE population < 1000000 OR population > 100000000;
```

### Searching in a Set of Values

```sql
SELECT <columns> FROM <table> WHERE <column> IN (<value 1>, <value 2>, ...);
```

Examples:

```sql
SELECT name FROM islands WHERE id IN (4, 8, 15, 16, 23, 42);
SELECT * FROM products WHERE category IN ("eBooks", "Books", "Comics");
SELECT title FROM courses WHERE topic IN ("JavaScript", "Databases", "CSS");
SELECT * FROM campaigns WHERE medium IN ("email", "blog", "ppc");
```

To find all rows that are not in the set of values you can use `NOT IN`.

```sql
SELECT <columns> FROM <table> WHERE <column>  NOT IN (<value 1>, <value 2>, ...);
```
Examples:

```sql
SELECT answer FROM answers WHERE id IN (7, 42);
SELECT * FROM products WHERE category NOT IN ("Electronics");
SELECT title FROM courses WHERE topic NOT IN ("SQL", "NoSQL");
```

### Searching within a Range of Values

```sql
SELECT <columns> FROM <table> WHERE <column> BETWEEN <lesser value> AND <greater value>;
```

Examples:

```sql
SELECT * FROM movies WHERE release_year BETWEEN 2000 AND 2010;
SELECT name, description FROM products WHERE price BETWEEN 9.99 AND 19.99;
SELECT name, appointment_date FROM appointments WHERE appointment_date BETWEEN "2015-01-01" AND "2015-01-07";
```

### Pattern Matching
Placing the percent symbol (`%`) any where in a string in conjunction with the `LIKE` keyword will operate as a wildcard. Meaning it can be substituted by any number of characters, including zero!

```sql
SELECT <columns> FROM <table> WHERE <column> LIKE <pattern>;
```

Examples:

```sql
SELECT title FROM books WHERE title LIKE "Harry Potter%Fire";
SELECT title FROM movies WHERE title LIKE "Alien%";
SELECT * FROM contacts WHERE first_name LIKE "%drew";
SELECT * FROM books WHERE title LIKE "%Brief History%";
```

### PostgreSQL Specific Keywords
`LIKE` in PostgreSQL is case-sensitive. To do case-insensitive searches use `ILIKE`.

```sql
SELECT * FROM contacts WHERE first_name ILIKE "%drew";
```

### Missing Values

```sql
SELECT * FROM <table> WHERE <column> IS NULL;
```

Examples:

```sql
SELECT * FROM people WHERE last_name IS NULL;
SELECT * FROM vhs_rentals WHERE returned_on IS NULL;
SELECT * FROM car_rentals WHERE returned_on IS NULL AND location = "PDX";
```

To filter out missing values you can use `IS NOT NULL`.

```sql
SELECT * FROM <table> WHERE <column> IS NOT NULL;
```

Examples

```sql
SELECT * FROM people WHERE email IS NOT NULL;
SELECT * FROM addresses WHERE zip_code IS NOT NULL;
```

### Adding a Row to a Table
Inserting a single row:

```sql
INSERT INTO <table> VALUES (<value 1>, <value 2>, ...);
```

This will insert values in the order of the columns prescribed in the schema.

Examples:

```sql
INSERT INTO users VALUES  (1, "chalkers", "Andrew", "Chalkley");
INSERT INTO users VALUES  (2, "ScRiPtKiDdIe", "Kenneth", "Love");

INSERT INTO movies VALUES (3, "Starman", "Science Fiction", 1984);
INSERT INTO movies VALUES (4, "Moulin Rouge!", "Musical", 2001);
```

Inserting a single row with values in any order:

```sql
INSERT INTO <table> (<column 1>, <column 2>) VALUES (<value 1>, <value 2>);
INSERT INTO <table> (<column 2>, <column 1>) VALUES (<value 2>, <value 1>);
```

Examples:

```sql
INSERT INTO users (username, first_name, last_name) VALUES ("chalkers", "Andrew", "Chalkley");
INSERT INTO users (first_name, last_name, username) VALUES  ("Kenneth", "Love", "ScRiPtKiDdIe");

INSERT INTO movies (title, genre, year_released) VALUES ("Starman", "Science Fiction", 1984);
INSERT INTO movies (title, year_released, genre) VALUES ("Moulin Rouge!", 2001,  "Musical");
```

### Adding Multiple Rows to a Table
Inserting multiple rows in a single statement:

```sql
INSERT INTO <table> (<column 1>, <column 2>, ...) 
             VALUES 
                    (<value 1>, <value 2>, ...),
                    (<value 1>, <value 2>, ...),
                    (<value 1>, <value 2>, ...);
```

Examples:

```sql
INSERT INTO users (username, first_name, last_name) 
    VALUES 
                  ("chalkers", "Andrew", "Chalkley"),
                  ("ScRiPtKiDdIe", "Kenneth", "Love");

INSERT INTO movies (title, genre, year_released) 
     VALUES 
                   ("Starman", "Science Fiction", 1984),
                   ("Moulin Rouge!", "Musical", 2001);
```

### Updating All Rows in a Table
An update statement for all rows:

```sql
UPDATE <table> SET <column> = <value>;
```

The `=` sign is different from an equality operator from a `WHERE` condition. It's an _assignment operator_ because you're assigning a new value to something.

Examples:

```sql
UPDATE users SET password = "thisisabadidea";
UPDATE products SET price = 2.99;
```

Update multiple columns in all rows:

```sql
UDPATE <table> SET <column 1> = <value 1>, <column 2> = <value 2>;
```

Examples:

```sql
UPDATE users SET first_name = "Anony", last_name = "Moose";
UPDATE products SET stock_count = 0, price = 0;
```

### Updating Specific Rows
An update statement for specific rows:

```sql
UPDATE <table> SET <column> = <value> WHERE <condition>;
```
Examples:

```sql
UPDATE users SET password = "thisisabadidea" WHERE id = 3;
UPDATE blog_posts SET view_count = 1923 WHERE title = "SQL is Awesome";
```

Update multiple columns for specific rows:

```sql
UDPATE <table> SET <column 1> = <value 1>, <column 2> = <value 2> WHERE <condition>;
```

Examples:

```sql
UPDATE users SET entry_url = "/home", last_login = "2016-01-05" WHERE id = 329;
UPDATE products SET status = "SOLD OUT", availability = "In 1 Week" WHERE stock_count = 0;
```

### Removing Data from All Rows in a Table
To delete all rows from a table:

```sql
DELETE FROM <table>;
```

Examples:

```sql
DELETE FROM logs;
DELETE FROM users;
DELETE FROM products;
```

### Removing Specific Rows
To delete specific rows from a table:

```sql
DELETE FROM <table> WHERE <condition>;
```

Examples:

```sql
DELETE FROM users WHERE email = "andrew@teamtreehouse.com";
DELETE FROM movies WHERE genre = "Musical";
DELETE FROM products WHERE stock_count = 0;
```

### Transactions
Switch autocommit off and begin a transaction:

```sql
BEGIN TRANSACTION;
```

Or simply:

```sql
BEGIN;
```

To save all results of the statements after the start of the transaction to disk:

```sql
COMMIT;
```

To reset the state of the database to before the begining of the transaction:

```sql
ROLLBACK;
````

### Ordering Columns
Ordering by a single column criteria:

```sql
SELECT * FROM <table name> ORDER BY <column> [ASC|DESC];
```

`ASC` is used to order results in ascending order. 

`DESC` is used to order results in descending order.

Examples:

```sql
SELECT * FROM books ORDER BY title ASC;
SELECT * FROM products WHERE name = "Sonic T-Shirt" ORDER BY stock_count DESC;
SELECT * FROM users ORDER BY signed_up_on DESC;
SELECT * FROM countries ORDER BY population DESC;
```

Ordering by multiple column criteria:

```sql
SELECT * FROM <table name> ORDER BY <column> [ASC|DESC],
                                    <column 2> [ASC|DESC],
                                    ...,
                                    <column n> [ASC|DESC];
```

Ordering is prioritized left to right.

Examples:

```sql
SELECT * FROM books ORDER BY    genre ASC, 
                                title ASC;

SELECT * FROM books ORDER BY    genre ASC,
                                year_published DESC;

SELECT * FROM users WHERE email LIKE "%@gmail.com" 
                    ORDER BY    last_name ASC,
                                first_name ASC;
```

### Limiting Results
To limit the number of results returned, use the `LIMIT` keyword.

```sql
SELECT <columns> FROM <table> LIMIT <# of rows>;
```

### Paging Through Results
To page through results you can either use the `OFFSET` keyword in conjunction with the `LIMIT` keyword or just with LIMIT alone.

```sql
SELECT <columns> FROM <table> LIMIT <# of rows> OFFSET <skipped rows>;
SELECT <columns> FROM <table> LIMIT <skipped rows>, <# of rows>; 
```

### Syntax definitions
 - **Keywords**: Commands issued to a database. The data presented in queries is unaltered.
 - **Operators**: Performs comparisons and simple manipulation
 - **Functions**: Presents data differently through more complex manipulation
 - **Arguments** or **Parameters**: Values passed in to functions.

A function looks like:

```sql
<function name>(<value or column>)
```

Examples:

```sql
SELECT UPPER("Andrew Chalkley");
SELECT UPPER(name) FROM passport_holders;
```

### Concatenating Strings
Use the concatenation operator `||`.

```sql
SELECT <value or column> || <value or column> || <value or column>  FROM <table>;  
```

Use the `CONCAT()` function.

```sql
SELECT CONCAT(<value or column>, <value or column>, <value or column>) FROM <table>;
```

### Finding Length of Strings
To obtain the length of a value or column use the `LENGTH()` function.

```sql
SELECT LENGTH(<value or column>) FROM <tables>;
```

### Changing the Case of Strings
Use the `UPPER()` function to uppercase text.

```sql
SELECT UPPER(<value or column>) FROM <table>;
```

Use the `LOWER()` function to lowercase text.

```sql
SELECT LOWER(<value or column>) FROM <table>;
```

### Create Excerpts with Substring
To create smaller strings from larger piece of text you can use the `SUBSTR()` funciton or the substring function.'

```sql
SELECT SUBSTR(<value or column>, <start>, <finish>) FROM <table>;
```

### Replacing Portions of Text
To replace piece of strings of text in a larger body of  text you can use the `REPLACE()` function.

```sql
SELECT REPLACE(<original value or column>, <target string>, <replacement string>) FROM <table>;
```

### Counting Results
To count rows you can use the `COUNT()` function.

```sql
SELECT COUNT(*) FROM <table>;
```

To count unique entries use the `DISTINCT` keyword too:

```sql
SELECT COUNT(DISTINCT <column>) FROM <table>;
```

To count aggregated rows with common values use the `GROUP BY` keywords:

```sql
SELECT COUNT(<column>) FROM <table> GROUP BY <column with common value>;
```

### Obtaining Totals
To total up numeric columns use the `SUM()` function.

```sql
SELECT SUM(<numeric column) FROM <table>;
SELECT SUM(<numeric column) AS <alias> FROM <table>
                                       GROUP BY <another column>
                                       HAVING <alias> <operator> <value>;
```

### Calculating Averages
To get the average value of a numeric column use the `AVG()` function.

```sql
SELECT AVG(<numeric column>) FROM <table>;
SELECT AVG(<numeric column>) FROM <table> GROUP BY <other column>;
```

### Finding the Maximum and Minimum Values
To get the maximum value of a numeric column use the `MAX()` function.

```sql
SELECT MAX(<numeric column>) FROM <table>;
SELECT MAX(<numeric column>) FROM <table> GROUP BY <other column>;
```

To get the minimum value of a numeric column use the `MIN()` function.

```sql
SELECT MIN(<numeric column>) FROM <table>;
SELECT MIN(<numeric column>) FROM <table> GROUP BY <other column>;
```

### Mathematical Operators
 - `*` Multiply
 - `/` Divide
 - `+` Add
 - `-` Subtract

```sql
SELECT <numeric column> <mathematical operator> <numeric value> FROM <table>;
```

### Up-to-the-Minute Dates and Times
*PostgreSQL:*

To get the current date use: `CURRENT_DATE`

To get the current time use: `CURRENT_TIME`

To get the current date time: `CURRENT_TIMESTAMP`

*MySQL:*

To get the current date use: `CURDATE()`

To get the current time use: `CURTIME()`

To get the current date time: `NOW()`

### Calculating Dates
See documentation sites:

 - [PostgreSQL](http://www.postgresql.org/docs/9.1/static/functions-datetime.html)
 - [MySQL](https://dev.mysql.com/doc/refman/5.5/en/date-and-time-functions.html)

### Formatting Dates
See documentation sites:

 - [PostgreSQL](http://www.postgresql.org/docs/9.1/static/functions-datetime.html) 
 - [MySQL](https://dev.mysql.com/doc/refman/5.5/en/date-and-time-functions.html)

### SQL JOINs
JOINs merge related data from multiple tables together in to result set.

The two most common types of joins are:
 - INNER JOIN
 - OUTER JOIN

### INNER JOINs
INNER JOINs return rows that match from both tables.

```sql
SELECT <columns> FROM <table 1> 
    INNER JOIN <table 2> ON <table 1>.<column> = <table 2>.<column>;


SELECT <columns> FROM <table 1> AS <table 1 alias> 
    INNER JOIN <table 2> AS <table 2 alias> ON <table 1 alias>.<column> = <table 2 alias>.<column>;
```

Examples:

```sql
SELECT product_name, category FROM products
    INNER JOIN product_categories ON products.category_id = product_categories.id;
SELECT products.product_name, product_categories.category FROM products
    INNER JOIN product_categories ON products.category_id = product_categories.id;
SELECT p.product_name, c.category FROM products AS p
    INNER JOIN product_categories AS c ON p.category_id = c.id;        
```

INNER JOINing multiple tables:

```sql
SELECT <columns> FROM <table 1> 
    INNER JOIN <table 2> ON <table 1>.<column> = <table 2>.<column>
    INNER JOIN <table 3> ON <table 1>.<column> = <table 3>.<column>;
```

Examples:

```sql
SELECT users.full_name, sales.amount, products.name FROM sales 
        INNER JOIN users ON users.id = sales.user_id
        INNER JOIN products ON products.id = sales.product_id;
```

### OUTER JOINs
There are 3 types of OUTER JOINs:

 - LEFT OUTER JOIN - JOINs all matching data and all non-matching rows from the _left_ table in the query
 - RIGHT OUTER JOIN - JOINs all matching data and all non-matching rows from the _right_ table in the query
 - FULL OUTER JOIN - JOINs all matching data and then all non-matching rows from both tables.

```sql
SELECT <columns> FROM <left table> 
    LEFT OUTER JOIN <right right> ON <left table>.<column> = <right table>.<column>;


SELECT <columns> FROM <left table> AS <left alias> 
    LEFT OUTER JOIN <right table> AS <right alias> 
        ON <left alias>.<column> = <right alias>.<column>;

```

Example:

If you wanted to get the product count for every category, even categories without products, an `OUTER JOIN` is the best solution.

```sql
SELECT categories.name, COUNT(products.id) AS "Product Count" FROM categories
    LEFT OUTER JOIN products ON categories.id = products.category_id;

SELECT categories.name, COUNT(products.id) AS "Products Count" FROM products
    RIGHT OUTER JOIN categories ON categories.id = products.category_id;
```

### Set Operations
Set operations merge data in to one set based on column definitions and the data contained within each column.

The four set operations are:
 - UNION
 - UNION ALL
 - INTERSECT
 - EXCEPT

The number of columns need to match. If number of columns don't match it'll result in an error.

```sql
<query 1> <set operation> <query 2>
SELECT <column> FROM <table 1> <set operation> SELECT <column> FROM <table 2>;
SELECT <column>, <column> FROM <table 1> <set operation> SELECT <column>, <column> FROM <table 2>;
```

### UNION
Unions return all distinct values from both data sets with no duplicates.

Get a list of unique restaurants from both north and south malls.

```sql
SELECT store FROM mall_south WHERE type = "restaurant"
    UNION 
SELECT store FROM mall_north WHERE type = "restaurant";
```

Get a list of unique classes taught in two schools. Order them by their class name.

```sql
SELECT evening_class FROM school_1 UNION SELECT evening_class FROM school_2
    ORDER BY evening_class ASC;
```

### UNION ALL
Union all returns all values from both data sets – with duplicates.

Get a list of all names for boys and girls and order them by name.

```sql
SELECT boy_name AS name FROM boy_baby_names 
    UNION ALL 
SELECT girl_name AS name FROM girl_baby_names
    ORDER by name;
```

### INTERSECT
Returns only values that are in both data sets.

Get list of classes offered in both schools.

```sql
SELECT evening_class FROM school_1 INTERSECT SELECT evening_class FROM school_2
    ORDER BY evening_class ASC;
```

Get list of restaurants at both mall locations.

```sql
SELECT store FROM mall_south WHERE type = "restaurant"
    INTERSECT 
SELECT store FROM mall_north WHERE type = "restaurant";
```

### EXCEPT
Returns data from the first data set that's not in the second.

Get a list of local stores in a mall.

```sql
SELECT store FROM mall
    EXCEPT
SELECT store FROM all_stores WHERE type = "national"
```

### Subqueries
Subqueries are queries within queries. A subquery can also be called an _inner_ query with the "parent" query being called the _outer_ query.

There are two main ways to use a subquery:

 1. In an `IN` condition
 2. As a derived or temporary table

A subquery in an `IN` condition must only have one column.

```sql
SELECT <columns> FROM <table 1> WHERE <table 1>.<column> IN (<subquery>);
SELECT <columns> FROM <table 1> 
    WHERE <table 1>.<column> IN (SELECT <a single column> FROM <table 2> WHERE <condition>);
```

Examples:

Get a list of user's names and emails for users who have spent over 100 dollars in a single transaction.

```sql
SELECT name, email FROM users 
    WHERE id IN (SELECT DISTINCT(user_id) FROM sales WHERE saleAmount > 100);

// OR

SELECT name, email FROM users
    INNER JOIN (SELECT DISTINCT(user_id) FROM sales WHERE saleAmount > 100) AS best_customers
    ON best_customers.user_id = users.id
```

Get a list of user's names and emails for users who have spent over 1000 dollars in total.

```sql
SELECT name, email FROM users WHERE id IN (SELECT user_id FROM sales WHERE SUM(saleAmount) > 1000 GROUP BY user_id);

// OR

SELECT name, email, total FROM users 
    INNER JOIN (SELECT user_id, SUM(saleAmount) AS total FROM sales WHERE total > 1000 GROUP BY user_id) AS ultimate_customers
    ON ultimate_customers.user_id = users.id;
```
