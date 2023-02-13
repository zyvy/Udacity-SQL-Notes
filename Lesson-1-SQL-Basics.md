## Lesson 1: Introduction to SQL

### Some Quick Vocabulary
- Structured Query Language (SQL) – Structured Query Language is a language that allows us to access information in a database. A typical query might look like this: 
```sql
SELECT account_id, standard_qty, gloss_qty 
FROM orders 
WHERE (standard_qty = 0 OR gloss_qty = 0) AND occurred_at = ‘2016-1-01’;
  ```
- NoSQL – NoSQL stands for Not Only SQL. NoSQL databases are a different type of database sometimes used to store web data. An example of a NoSQL database is MongoDB.
- Entity Relationship Diagram (ERD) – A diagrammatic representation of tables and their relationships to one another. Each box shows the name of the table and has two columns below. The first column shows whether a particular field listed to the right is a primary key (PK) or a Foreign Key (FK); the second shows a list of the attributes in the table. Each attribute has a corresponding column in the actual table. The key point here is that the ERD shows us relationships between tables. The “crows feet” arrows show us how the tables connect to one another by connecting primary keys to foreign keys. The three little prongs show that the foreign key can appear in many rows in a table. In other words, the foreign key is not unique in table.
- Primary Key (PK) – Every table has a primary key. The primary key is a unique value for each row. Now two rows can have the same primary key. The primary key is often the first column in a table.
- Foreign Key (FK) – A foreign key is a column in one table that is the primary key in a different table.
- Postgres - A popular open-source database with a very complete library of analytical functions. This is the database used in the course.

### ERD
 These diagrams help you visualize the data you are analyzing including:
- The names of the tables.
- The columns in each table.
- The way the tables work together.

### Why is SQL important?
1.	Easy to understand
2.	Can access data directly
3.	Can audit data
4.	Can replicate data
5.	Can analyze multiple tables at once
6.	Can do complex analysis
7.	Incredible flexible

### There are some major advantages to using traditional relational databases, which we interact with using SQL. The five most apparent are:

SQL is easy to understand.
Traditional databases allow us to access data directly.
Traditional databases allow us to audit and replicate our data.
SQL is a great tool for analyzing multiple tables at once.
SQL allows you to analyze more complex questions than dashboard tools like Google Analytics.

### Why do businesses like DBs? 
1.	Data integrity is ensured
2.	Data can be accessed quickly
3.	Data is easily shared

### Key points about DBs:
- Data in databases is stored in tables that can be thought of just like Excel spreadsheets. For the most part, you can think of a database as a bunch of Excel spreadsheets. Each spreadsheet has rows and columns. Where each row holds data on a transaction, a person, a company, etc., while each column holds data pertaining to a particular aspect of one of the rows you care about like a name, location, a unique id, etc.
- All the data in the same column must match in terms of data type. An entire column is considered quantitative, discrete, or as some sort of string. This means if you have one row with a string in a particular column, the entire column might change to a text data type. This can be very bad if you want to do math with this column!
- Consistent column types are one of the main reasons working with databases is fast. Often databases hold a LOT of data. So, knowing that the columns are all of the same types of data means that obtaining data from a database can still be fast.

### What are some examples of SQL DBs?
1.	MySQL
2.	Access
3.	Oracle
4.	MS SQL Server
5.	Postgres

### What is a statement in SQL?
A statement in SQL is a command that allows you to perform a certain function.  Examples include:
 - CREATE TABLE is a statement that creates a new table in a database.
 - DROP TABLE is a statement that removes a table in a database.
 - SELECT allows you to read data and display it. This is called a query.

SQL queries can be run successfully whether characters are written in upper- or lower-case. In other words, SQL queries are not case-sensitive. But it is common and best practice to capitalize all SQL commands, like SELECT and FROM, and keep everything else in your query lower case.
It is common to use underscores and avoid spaces in column names. It is a bit annoying to work with spaces in SQL. In Postgres, if you have spaces in column or table names, you need to refer to these columns/tables with double quotes around them (Ex: FROM "Table Name" as opposed to FROM table_name). In other environments, you might see this as square brackets instead (Ex: FROM [Table Name]).

### SELECT * FROM orders;
This statement is composed of clauses. Clauses always appear in the same order. Some clauses are required and others are optional. The SELECT clause tells the database which columns you want to read from the database. The * is called a wildcard. There are various types of wildcards. This one represents “all columns.” The FROM clause tells the database which table to you want to select columns from. Both SELECT and FROM are mandatory clauses in any SELECT statement. You can write statements in lower case, but traditionally, SQL commands are written all uppercase. So, “select * from orders;” works just fine, but “SELECT * FROM orders;” is more conventional. Sometimes you’ll be required to end a statement in a semicolon, but it depends on the environment. It’s a good habit to include the semicolon at the end.

### The LIMIT Clause
The LIMIT clause limits the number of rows returned from a query. For example:

```sql
SELECT *
FROM orders
LIMIT 10
```

### The ORDER BY clause
The ORDER BY clause allows you specify which column you want to use as the basis for your query results ordering and whether you would like your query results to be put in ascending order (that’s the default) or DESCending order. For example:
```sql
SELECT *
FROM orders
ORDER BY occurred_at DESC
LIMIT 10
```
Just like in Excel, you can order by multiple columns. Just list the columns you want to use as a comma separated list. For example:
```sql
SELECT *
FROM orders
ORDER BY occurred_at DESC, total_amt_usd
LIMIT 10
```
Notice that we specified that “occurred_at” should be descending order, but total_amt_usd should be in the default ascending order.
ORDER BY in a SQL query only has temporary effects, for the results of that query, unlike sorting a sheet by column in Excel or Sheets.
The ORDER BY statement always comes in a query after the SELECT and FROM statements, but before the LIMIT statement. If you are using the LIMIT statement, it will always appear last. As you learn additional commands, the order of these statements will matter more.

### The WHERE Clause
The WHERE clause goes between FROM and ORDER BY. WHERE allows you narrow your search to results where one column has a particular value or range of values. For example:
```sql
SELECT *
FROM orders
WHERE account_id >= 1000 and account_id <= 1041 and standard_qty > 150
ORDER BY occurred_at
LIMIT 1000;
```
Here, you’ll get results only for the records with account_id in the range greater than or equal to 1,000 and less than or equal to 1041 and with standard_qty greater than 150. You can use a combination of mathematical and logical operators to create complex WHERE clauses. The example above uses columns that have numerical values, but you could also use columns with text values. For example,
```sql
SELECT name, website, primary_poc
FROM accounts
WHERE name = 'Exxon Mobil';
```

### Derived Columns
A derived column is a column you create by using mathematical operations on already existing columns. For example:
```sql
SELECT id, (standard_amt_usd/total_amt_usd)*100 AS std_percent, total_amt_usd
FROM orders
LIMIT 10;
```
Here, we select the “id” column and a second derived column that we create by dividing standard_amt_usd by total_amt_usd and multiplying that by 100. We use the AS clause to name this new derived column “std_percent.” Then we add a third column – “total_amt_usd”.

### Logical Operators
Logical operators allow you to create longer more complex statements. Here’s a summary of the logical operators:
- LIKE - This allows you to perform operations similar to using WHERE and =, but for cases when you might not know exactly what you are looking for.
- IN - This allows you to perform operations similar to using WHERE and =, but for more than one condition.
- NOT - This is used with IN and LIKE to select all of the rows NOT LIKE or NOT IN a certain condition.
- AND & BETWEEN - These allow you to combine operations where all combined conditions must be true.
- OR - This allows you to combine operations where at least one of the combined conditions must be true.

### LIKE Example
```sql
SELECT *
FROM accounts
WHERE website LIKE '%google%';
```
Here we’re selecting all columns from the “accounts” table where the “website” column is like the word “google,” but preceded by 0 or more characters of any type and/or followed by 0 or more characters of any type.  Not that LIKE is always used in the WHERE clause.

### IN Example
 The IN operator is useful for working with both numeric and text columns. This operator allows you to use an =, but for more than one item of that particular column. We can check one, two, or many column values for which we want to pull data, but all within the same query.
```sql
SELECT *
FROM orders
WHERE account_id IN (1001,1021);
```
Here’s we’re selecting all columns from the “orders” table but only where the “account_id” is in the group 1001 or 1021. 

### NOT Example
You can add the NOT operator before IN or LIKE to get the inverse of the results those queries would otherwise produce. For example:
```sql
SELECT sales_rep_id, 
       name
FROM accounts
WHERE sales_rep_id NOT IN (321500,321570)
ORDER BY sales_rep_id;
```
Here, we’re getting the “sales_rep_id” and “name” columns from the “accounts” table, but only where the “sales_rep_id” is not in the group 321500 or 321570. 
Here’s another example:
```sql
 SELECT *
FROM accounts
WHERE website NOT LIKE '%com%';
```
Here, we’re getting all of the columns from the “accounts” table, but only where the “website” column does not contain a value with the string “com” within it.

### AND, BETWEEN, and OR Examples
```sql
SELECT *
FROM orders
WHERE occurred_at >= '2016-04-01' AND occurred_at <= '2016-10-01'
ORDER BY occurred_at
```
Here, we select all columns from the “orders” table, but only where the “occurred_at” column contains values greater than or equal to ‘2016-04-01’ and less than or equal to ‘2016-10-01’. Not that you must repeat the “occurred_at” column name for each arithmetic operator. The results are then ordered by “occurred_at”.
The BETWEEN operator works similarly to AND, but look like this:
```sql
SELECT *
FROM orders
WHERE occurred_at BETWEEN '2016-04-01' AND '2016-10-01'
ORDER BY occurred_at
```
Whereas the AND operator makes a statement more exclusive of some records, the OR operator makes a statement more inclusive.
```sql
SELECT *
FROM orders
WHERE standard_qty = 0 OR gloss_qty = 0 OR poster_qty = 0
```
Here, we are selecting all columns from the “orders” table, but only where the “standard_qty” is 0, or where the “gloss_qty” is 0, or where the “poster_qty” is 0. 

