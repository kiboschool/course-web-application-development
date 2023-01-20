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

```sql
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

```sh
sqlite3 countries_database.sqlite
```

### SELECT

The SELECT statement lets us pick out data from the database.

First, lets try selecting all the data:

```sql
sqlite> SELECT * FROM countries;
Afghanistan |ASIA (EX. NEAR EAST)         |31056997|647500|48,0|0,00|23,06|163,07|700|36,0|3,2|12,13|0,22|87,65|1|46,6|20,34|0,38|0,24|0,38
Albania |EASTERN EUROPE                     |3581655|28748|124,6|1,26|-4,93|21,52|4500|86,5|71,2|21,09|4,42|74,49|3|15,11|5,22|0,232|0,188|0,579
(..224 rows)
Zimbabwe |SUB-SAHARAN AFRICA                 |12236805|390580|31,3|0,00|0|67,69|1900|90,7|26,8|8,32|0,34|91,34|2|28,01|21,84|0,179|0,243|0,579
```

That's more data than we wanted!

Let's turn on some sqlite settings to make the data easier to read:

```sql
sqlite> .headers on
sqlite> .mode columns
```

Instead of selecting everything, lets just select the country and population. 

```sql
sqlite> SELECT country, population FROM countries;
Country                            Population
---------------------------------  ----------
Afghanistan                        31056997
Albania                            3581655
...
Zimbabwe                           12236805
```

SELECT lets us get data from the database. There are a lot more ways to use
SELECT, but it's better to practice hands-on than to just read!

## Practice: SQL Select in SQLBolt

SQL takes a lot of practice!

Read the introduction and first lesson on [SQLBolt](https://sqlbolt.com/). 

Complete the interactive exercises to practice writing queries.
