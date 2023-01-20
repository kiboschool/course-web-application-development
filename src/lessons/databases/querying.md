# Querying

## What is a query?

A SQL (Structured Query Language) query is a command used to communicate with a 
relational database to retrieve or manipulate data. SQL is the standard language 
used to interact with relational databases, and it allows you to perform a wide 
range of operations on the data stored in them.

A SQL query is a statement written in SQL that is used to retrieve or manipulate 
data in a database. Queries can be used to select specific data from one or more 
tables, insert new data into a table, update existing data, or delete data from 
a table.

For example, a SELECT statement is used to retrieve data from a table, and it 
may look like this:

```sql
SELECT first_name, last_name FROM customers WHERE city = 'New York';
```

This query retrieves the first and last names of customers who live in the city 
of New York.

Another example, an INSERT statement is used to insert new data into a table, it 
may look like this:

```
INSERT INTO customers (first_name, last_name, email) VALUES ('John', 'Doe', 'johndoe@example.com');
```

This query inserts a new customer with first name "John", last name "Doe" and 
email "johndoe@example.com" into the table 'customers'.

There are many other types of SQL statements, each with its own specific syntax 
and use cases. A good understanding of SQL is essential for working with 
relational databases and building efficient and effective database-driven 
applications.

## Querying from SQLite in the Terminal

If you followed the SQLite Terminal setup steps, you're ready to start making
some queries.

Let's see some examples of queries on the countries database.

## Practice: SQL Select in SQLBolt

SQL takes a lot of practice!

Read the introduction and first lesson on [SQLBolt](https://sqlbolt.com/). 

Complete the interactive exercises to practice writing queries.


## Querying from Python


