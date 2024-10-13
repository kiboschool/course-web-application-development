# Relational DBs

## What are Relational DBs?

A relational database is an application that organizes data into one or more tables (or "relations") of rows and columns, with a unique key identifying each row. The tables are typically related to each other through the use of foreign keys, which allow data to be linked across tables. This structure allows for data to be queried and manipulated in a flexible and efficient manner. 

The most popular type of relational database is SQL (Structured Query Language) databases, such as SQLite (which we'll use in class), MySQL, SQL Server, Oracle, and PostgreSQL. These databases are widely used in many types of applications, from small personal projects to large enterprise systems.

See these videos for further explanation of relational databases.

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.youtube.com/embed/OqjJjpjDRLc" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.youtube.com/embed/V4gbPVdUOpw" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

### Key ideas

- A database is a program that stores data
- Databases persist to _disk_ instead of just in your program's memory
- They make it efficient to organize and manipulate data
- Structured as typed columns and rows of items

## What does a relational DB look like?

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.youtube.com/embed/e8zSXnyskro" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.youtube.com/embed/PhvA7DCgtpw" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

A table is made of _rows_ and _columns_.

A **row** is a set of data that corresponds to one item or object in the real 
world, such as a customer, an order, or a product. Each row has a unique 
identifier, called a _primary key_, that allows it to be easily accessed and 
distinguished from other rows in the table.

A **column**, also known as a field, represents a specific attribute or piece 
of data within a row. For example, in a table of customers, a column could 
represent the customer's name, address, or phone number. Each column has a 
specific data type (e.g. text, integer, date) and often has certain constraints 
applied to it (e.g. not null, unique).

## Consistency: Preventing Data Errors

Databases are designed to help prevent _inconsistencies_ in data. They ensure,
for instance, that every row has the same fields, and that the fields have
exactly the right types. A customer's birthdate should be a date (and not text
or a url or a number).

As you'll see, databases have many other ways that they help keep data
consistent.

## Try it: Explore an example database

> Explore this visual database in Airtable: https://airtable.com/shr5RgFWwaFQ46VXd

Ask yourself:
- What are the columns?
- What are the _types_ of the columns?
- What does one row represent?
- What kinds of operations would you want to do with this data?

If you need to, [sign up for Airtable here](https://support.airtable.com/docs/student-plan-extended-trial)
