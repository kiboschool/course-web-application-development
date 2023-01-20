# Database Management

So far, we've focused on reading the data in the database. There are also
another set of commands that focus on managing the database itself. This
includes creating and connecting to databases and managing the database
_schema_.

Managing the schema of a database involves creating and modifying the _structure 
of the database_, including the tables, fields, and relationships between them. 

This includes tasks such as 
- creating new tables
- altering the structure of existing tables
- adding or modifying indexes to improve performance. 

## The Schema

A database schema is the blueprint that defines the structure of a database, including the tables, fields, and relationships between them. It describes the organization of data and the rules that govern it, including constraints, defaults, and null values.

The schema is defined using a set of SQL statements that create the tables, fields, and relationships between them. These statements are typically executed when the database is first created, or when the schema needs to be modified.

To see the schema of an existing table in SQLite, you can use the `.schema` command from the terminal:

```
❯ sqlite3 countries_database.sqlite
sqlite> .schema
CREATE TABLE IF NOT EXISTS "countries" (`Country`, `Region`, `Population`, `Area (sq. mi.)`, `Pop. Density (per sq. mi.)`, `Coastline (coast/area ratio)`, `Net migration`, `Infant mortality (per 1000 births)`, `GDP ($ per capita)`, `Literacy (%)`, `Phones (per 1000)`, `Arable (%)`, `Crops (%)`, `Other (%)`, `Climate`, `Birthrate`, `Deathrate`, `Agriculture`, `Industry`, `Service`);
```

This provides the schema in the form of a `CREATE TABLE` statement. This one
says to create a table named "countries" (if there is not one already), with the
fields listed (country, region, population, etc).

## Creating a table

A `CREATE TABLE` statement in SQL is used to create a new table in a database. 
The basic syntax for creating a table is as follows:

```sql
CREATE TABLE table_name (
    column1_name data_type constraint,
    column2_name data_type constraint,
    ...
    constraint
);
```

- `table_name` is the name of the table being created.
- `column_name` is the name of a column in the table.
- `data_type` is the type of data that the column will store (e.g. INT, VARCHAR, DATE, etc.).
- `constraint` is an optional clause that specifies additional properties for the column such as primary key, not null, check etc.

For example, the following SQL statement creates a table named "employees" with three columns: "id", "name", and "salary":

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    salary DECIMAL(10,2)
);
```

This creates a table named 'employees' with three columns 'id','name','salary' where 
- 'id' is a primary key
- 'name' cannot be null
- 'salary' is decimal with 10 digits and 2 digits after the decimal.

It's worth noting that different database management systems (DBMS) have slightly 
different syntax for creating tables, so the exact syntax may vary depending on 
the specific DBMS you are using.

### Practice: Creating a table

Read the SQLBolt lesson on creating tables:

[SQL Lesson 16: Creating tables](https://sqlbolt.com/lesson/creating_tables)

Practice writing a CREATE TABLE statement.

## Altering and Dropping tables

The ALTER TABLE statement in SQL is used to add, modify, or delete columns in an existing table, or to change the table's constraints. The basic syntax for the ALTER TABLE statement is as follows:

```sql
ALTER TABLE table_name
    [ADD | DROP | MODIFY] column_name data_type constraint;
```
- ADD is used to add a new column to the table.
- MODIFY is used to change the definition of an existing column.
- DROP is used to delete a column from the table.

For example, the following SQL statement adds a new column named "email" to the "employees" table:

```sql
ALTER TABLE employees ADD email VARCHAR(255);
```

The following SQL statement modifies the data type of 'salary' column in "employees" table:

```sql
ALTER TABLE employees MODIFY salary DECIMAL(12,2);
```

The DROP TABLE statement in SQL is used to delete a table from the database. The basic syntax for the DROP TABLE statement is as follows:

```sql
DROP TABLE table_name;
```

For example:

```sql
DROP TABLE employees;
```

This will delete the table named 'employees' and all the data inside it permanently.

It's worth noting that dropping a table will also delete all the data stored in the table, so you should be careful when using this statement, and make sure you have a backup of the data before you drop a table.

## Practice: Altering and Dropping tables

Read the SQLBolt lessons on Altering and Dropping tables:
- [SQL Lesson 17: Altering tables](https://sqlbolt.com/lesson/altering_tables)
- [SQL Lesson 18: Dropping tables](https://sqlbolt.com/lesson/dropping_tables)

Practice the exercises to work on your database management skills.

## Migrations

Your application expects the schema to have a particular shape. When you change
the schema, you often change the code too.

Using Git, it's easy (well, at least possible) to share your code changes. How
do you share your schema changes?

The answer is _migrations_.


## Seeding

