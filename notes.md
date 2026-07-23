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