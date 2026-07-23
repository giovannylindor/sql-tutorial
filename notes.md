# Data and Databases

* Unstructured Data: data that has info w/o any structure
    - Storing data this way may work if you only have a small amount, but once it grows it becomes too wild 

* Structured Data: data thats formatted in a structured format (rows/cols)
    - This allows people to find data easily and manage it better
    - Data be sorted and modified 
    - An example of structured data is in a _Relational Database_


**_What is a database?_**

_A structured set of data held in a computer._ 

Examples of databases:
- Spreadsheets
- Tables


* Relational Database: Database organized according to a relational model of data
    - The relational model defines a set of relationships between data to determine how data stored can interact
    - It's represented in a 2d table 
    - Relational Databsed helps cut down on complicated data 

* Relational Database Management System (RDBMS): An application for managing databases 
    - Allows users/applications to interact w/ a DB by using syntax that conforms to a set of standards 
    - Examples:
        - SQLite
        - MS SQL
        - PostgreSQL
        - MySQL 
    - Some are lightweight and easy, others are robust and scalable and complex to install. 
    - They all use SQL 


- A relational model isn't the only model used by DBs. These are typically labeled _NoSQL_
     - MongoDB uses document-oriented storage


# SQL 

* SQL stands for _Strutured Query Language_ and is used to comminicate w/ a relational database
    - Its a language that uses simple english languages which allow you to: 
         - Select (Find)
         - Insert (Add)
         - Update (Change)
         - Delete (Remove)
    - SQL is a _declarative language_ in which you write an SQL statement to describe what needs to be done, but not _how_ to do it. 
    - SQL is relational &rarr; you define relationships between records using _foreign keys_ 
    - SQL shows you the entities and values your app exepcts
    - SQL _isn't_ good w/ dealing w/ dynamic data
    - Having a **Database Schema** (_Blueprint that defines how data is stored, orginized and related_) means you can validate data

* Primary Key: A specific column that uniquely identifies each record in a table
    - Links to another table in a DB 
    - No primary key value is null 
    - ![ ](/primary-key.webp)

* NoSQL: Databases that aren't non-relational and are used as document stores, graph DBs, key-value stores, and wide-column stores
    - "No" doesn't mean No SQL &rarr; it means _Not Only SQL_. 
        - You can find SQL in NoSQL DBs 
    - They sacrifce robustness to gain speed and scale
    - There are 4 broad categories of a NoSQL database:
        - 1. Document Stores
            - Looks like SQL but has no schema and normalization 
            - Ex: MongoDB, Firebase
        - 2. Graph DBs
            - Niche NoSQL DB
            - Common case: "People you may know" 
            - Ex: Neo4j, ArangoDB, CosmosDB
        - 3. Key-Value Stores
            - Holds key value pairs
            - Used for caching and storing sessions data
            - Ex: Redis, Memcached, CosmosDB
        - 4. Wide-column data stores
            - Looks like key-value, but a key holds access to columns 
            - Scalable and holds billions of columns and can be dynamic
            - Used financial data marketing, IoT data, Graph Data
            - Ex: CosmosDB, Bigtable, Cassandra, HBase


**How do I choose between SQL and NoSQL?**

- SQL is a good all-around choice
- For Specialized work NoSQL may be better
- If youre looking for fast & scale, use NoSQL


A good knowledge of SQL will help when using an ORM (Obect-Relational Mapper) and when making complicated DB queries 


# Breakdown

- SQL is the language to talk to relational databases
    - These DB use many Tables to store different types of data

* Tables: lists like spreadsheets where each row is a different record and each column is one of that records attributes 
    - The one column thats in all tables is the `ID` column
        - Which gives you unique row numbers and called the records _Primary Key_ 

- You can link Tables together by making one of the columns in one table point to the ID of another table 

**Setting Up Database**

* The first category of cmds are for setting up the database
    - `CREATE DATABASE`: Setup DB
    - `CREATE TABLE`: Creates Individual Table 

* The setup information is stored in a file called the Schema, and is updated when you make changes to the structure of your DB 

* You can tell your DB to only allow unique values in a column or index for faster searching using `CREATE INDEX` 

* SQL uses semicolons at the end of lines and single quotes instead of double 


**Messing with Data**

Once your DB is setup and you have tables to work with, use SQL statements to populate it

* The Main Actions are CRUD (Create, Read, Update, Delete)
    - Most actions will fall under READ

* Every CRUD-like cmd in SQL has the Action, The Table, and the Conditions
    - If you do an action w/o specifying the conditions it will apply to the whole table 

* For DELETING Queries, the mistake is smth like `DELETE FROM users` which remotes all users from a table
    - You prob need to delete just 1 user
    - You would specify based on either `name` or `id` as your condition
    - So the correct syntax would be `DELETE FROM users WHERE users.id = 1`


* You can do comparisons like `>, <, <=`, etc
- You can do logicals like `AND, OR, NOT`, etc 

To chain clauses tg: 
`DELETE FROM users WHERE id > 12 AND name = 'foo';`
* This deletes every user with an id greater than 12 and has the name "Foo" 


* CREATING queries use `INSERT INTO`  
    - You need to specify the columnns to insert values into, followed by values
    - `INSERT INTO users (name, email) VALUES ('foobar', 'foo@bar.com');` 


* UPDATE queries use `UPDATE` and you need to tell it what data to `SET` it to using key=value pairs, and which rows to do those updates for 
    - Be careful! if your `WHERE` finds multiple rows, they'll all get updated!

```SQL
    UPDATE users
       SET name='barfoo', email='bar@foo.com'
       WHERE email='foo@bar.com';`
```


* READ queries use `SELECT` and are the most common
    - `SELECT * FROM users`
        - `*` means all columns 
        - Specify a column using the table name and the column name
            - You can get away w/ just the column name if its a query from 1 table, but if its more than 1, specify col name and table name!
    - If you wanna select unique vals from a col, use `SELECT DISTINCT`
        - Ex: Different names of users w/o duplicates
            - `SELECT DISTINCT users.name FROM users`


**Mashing Tables `JOIN`** 

* Joining is the clause that combines rows from 2+ tables based on a related column
    - Typically by linking a foreign key in one table to the primary key of another
    - There are 4 types of joins 

Example 

Table A 

| id | name | 
| --- | ---- |
| 1  | _pirate_ |
| 2  | monkey |
| 3  | _ninja_ |


Table B

| id | name | 
| --- | ---- |
| 1  | _pirate_ |
| 2  | _ninja_ |
| 3  | sleeping |


**Inner Join** 
- Only Produces sets of records that match in Table A and Table B

```SQL
SELECT * FROM TableA
INNER JOIN TableB
ON TableA.name = TableB.name
```

Returns 

| id | name |
| --- | --- | 
| 1  |  pirate |
| 3 | ninja |


| id | name | 
| --- | --- | 
| 1  | pirate | 
| 2 | ninja |

**FULL OUTER JOIN**
- Produces set of all records from Table A and Table B w/ matching records from both sides if available
    - if no match, missing side == null

```SQL
SELECT * FROM TableA
FULL OUTER JOIN TableB
ON TableA.name = TableB.name
```
RETURNS 
id    name       id    name
--    ----       --    ----
1     Pirate     2     Pirate
2     Monkey     null  null
3     Ninja      4     Ninja
4     Spaghetti  null  null
null  null       1     Rutabaga
null  null       3     Darth Vader

To produce set unique to A and B, perform the same full outer join 
Exclude records via where clause

```SQL
SELECT * FROM TableA
FULL OUTER JOIN TableB
ON TableA.name = TableB.name
WHERE TableA.id IS null
OR TableB.id IS null
```

Returns 
id    name       id    name
--    ----       --    ----
2     Monkey     null  null
4     Spaghetti  null  null
null  null       1     Rutabaga
null  null       3     Darth Vader

**Left/Right Outer Join**
- Producses set of all records from Table A w/ matching records from both sides
    - If no match, the RIGHT side returns null


```SQL
SELECT * FROM TableA
LEFT OUTER JOIN TableB
ON TableA.name = TableB.name 
```

Returns
id  name       id    name
--  ----       --    ----
1   Pirate     2     Pirate
2   Monkey     null  null
3   Ninja      4     Ninja
4   Spaghetti  null  null

* To produce records from A but not B
    - Do same left outer join 
        - Exclude records you dont want via `WHERE`

```SQL 
SELECT * FROM TableA
LEFT OUTER JOIN TableB
ON TableA.name = TableB.name
WHERE TableB.id IS null
```

id  name       id     name
--  ----       --     ----
2   Monkey     null   null
4   Spaghetti  null   null


**Cross Join**
- JOINS everything-to-everything

```SQL
SELECT * FROM TableA
CROSS JOIN TableB
```


**Using Functions to Aggregate Data** 

Aggregate Functions offered by SQL help to return a single relavent value 

Some of these Functions Are:
-  `SUM`
- `MIN`
- `MAX`

These would be apart of the `SELECT` statement 
Ex: `SELECT MAX(users.age) FROM users`

* the funcs will operate on single column unless you include `*` which includes all rows 

* `AS` is often used as an alias to rename columns or aggregate functions to be called later 
    - Ex: `SELECT MAX(users.age) AS highest_age FROM users` will return a col named `highest_age` w/ the maximum age



Primary Key = A specific column that uniquely identifies each record in a table