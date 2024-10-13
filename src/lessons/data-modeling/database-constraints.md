# Database Constraints

You got a preview of database constraints when discussing form data validation last week.

Now, let's take a slightly deeper look at what kinds of constraints you can add to a database.

## Types of Data

One fundamental way that databases enforce valid data is through the types of the columns.

Each database has different types that it supports. SQLite supports [just 5 types](https://www.sqlite.org/datatype3.html): NULL, INTEGER, REAL, TEXT, and BLOB. (Many more 'spellings' of types are allowed in CREATE TABLE statements, but SQLite turns them into one of these types.) Postgres supports [many datatypes](https://www.postgresql.org/docs/9.4/datatype.html) and even more through [extensions](https://www.postgresql.org/download/products/6-postgresql-extensions/) like [PostGIS](https://www.postgis.net/). 

If you try to INSERT or UPDATE a column with a value that does not match the data type of the column, the database will reject your query. 

```sql
sqlite> INSERT INTO students (id) VALUES ("albert");
Error: stepping, datatype mismatch (20)
```

> Well... at least it should. [SQLite is a bit flexible with the types](https://sqlite.org/flextypegood.html) of the columns, so you don't get as much protection as other databases. You can enable [STRICT](https://sqlite.org/stricttables.html) for a table if desired.

## What are database constraints?

Your database will raise an error instead of inserting a string into an integer column. That protects your data - you won't accidentally enter a string for a numeric rating, or any similar error.

Database constraints are rules or conditions that must be met by the data in a database. They are used to enforce the integrity and consistency of data within the database. Constraints are specified when creating or modifying a database table and are enforced by the database management system.

That way, more invalid situations will raise errors - like if you forget to include the 'name' for a student, if that column is marked as NOT NULL. 

More errors means more protection from invalid data.

## Types of constraints

There are several types of database constraints:

- `NOT NULL`: Specifies that a column cannot contain a null value.
- `UNIQUE`: Specifies that a column or a set of columns must have unique values.
- `PRIMARY KEY`: Specifies a unique identifier for each row in a table and cannot contain null values. There can only be one primary key for any table.
- `FOREIGN KEY`: Specifies a relationship between two tables by referencing the primary key of one table in another table. It will fail if the value in the FOREIGN KEY column does not exist in the other table.
- `CHECK`: Specifies a custom condition that must be met by the data in a column. `CHECK` constraints allow you to bring your own constraint to a column.

There are two other specifiers you'll see for columns, which aren't _quite_ constraints in the same way:

- `DEFAULT`: Specifies a default value for a column. If no value is provided, the default value is used.
- `AUTOINCREMENT`: Automatically fills in the value with the next incremental value. 

These don't raise errors for invalid data the way other constraints do, but they can help ensure data integrity.

## NOT NULL

As the name suggests, the NOT NULL constraint prevents NULL values from being added in that column. This is useful in situations where you need to have that data for the application to make sense. For instance - many applications will not work if a user does not have an email. Setting NOT NULL on the email field will prevent the database from storing users without emails.

If the constraint is specified:
```sql
  assignment_id INTEGER NOT NULL,
```

Then the error might be:

```sql
sqlite> INSERT INTO assignment_scores (student_id, assignment_id, score) VALUES (1, NULL, 100);
Error: stepping, NOT NULL constraint failed: assignment_scores.assignment_id (19)
```

## UNIQUE

The UNIQUE constraint is used when you want to ensure that a particular column or set of columns contains unique values. 

For example, you might use the UNIQUE constraint on the email column of a customers table to ensure that each customer has a unique email address. This constraint is also often used to enforce unique identifiers, such as product codes or order numbers.

If the constraint is specified:
```sql
  email TEXT UNIQUE,
```

Then the error might be:

```sql
sqlite> INSERT INTO users (email) VALUES ("oye@example.com");
sqlite> INSERT INTO users (email) VALUES ("oye@example.com");
Error: stepping, UNIQUE constraint failed: users.email (19)
```

> How would you specify a unique constraint on multiple columns in the same table? 
> Write the constraint statement that would ensure that the pair (post_id, tag_id) is unique for a post_tags table.

## PRIMARY KEY

A primary key is both UNIQUE and NOT NULL, and there can only be one for any table. 

The primary key is special because it can be used in a FOREIGN KEY constraint on another table.

## FOREIGN KEY

The FOREIGN KEY constraint ensures that the related data exists when inserting a row that references another table.

> Note: SQLite will allow you to specify FOREIGN KEY constraints, but it will not check them unless you enable them by executing `PRAGMA foreign_keys = ON;`

with the foreign key constraint specified this way on the `assignment_scores` table:

```sql
FOREIGN KEY (student_id) REFERENCES students (id)
```

This is the error when inserting a student that does not exist:
```sql
sqlite> INSERT INTO assignment_scores (student_id, assignment_id, score) VALUES (5000000, 1, 100);
Error: stepping, FOREIGN KEY constraint failed (19)
```

## CHECK

The check constraint allows you to define your own expression to check that the data is valid. It's _very_ powerful; it can execute SQL expressions. Here are some examples.

Check that the price is more than 0:

```sql
price INTEGER CHECK (price > 0),
```

Check that the phone number is longer than 10 characters:

```sql
phone TEXT NOT NULL CHECK (length(phone) >= 10),
```

CHECK constraints can also apply to a whole table, like checking that the start date is before the end date:

```sql
CREATE TABLE terms (
  start_date INTEGER NOT NULL,
  end_date INTEGER NOT NULL,
  CHECK (start_date < end_date)
);
```

Attempting to insert invalid data into any of these tables would result in an error.

```sql
sqlite> INSERT INTO term VALUES (date('now'), date('now', '-1 day'));
Error: stepping, CHECK constraint failed: start_date < end_date (19)
```

## Practice: SQL Expressions

CHECK constraints rely on SQL expressions. Like the rest of SQL, expressions take practice.

Complete [SQL Lesson 9: Queries with expressions](https://sqlbolt.com/lesson/select_queries_with_expressions) on SQLBolt.

## ON CONFLICT

When encountering a conflict with a constraint, you can have the database take an action other than fail.

For instance, when inserting data that _might_ conflict with an existing row, you can update that data if it exists.

Here's an example. 

A process will be looking at emails and scores, and inserting them into the database. 
If an email appears more than once, the _total score_ should be reflected in the database.

```sql
CREATE TABLE email_scores (
  email TEXT NOT NULL UNIQUE,
  score INTEGER NOT NULL,
);
```

```python
for (email, score) in data:
  conn.execute('INSERT INTO email_scores (email, score) VALUES (?, ?) ON CONFLICT DO UPDATE SET score = score + ?;', (email, score, score))
conn.commit()
```

> Note: don't worry about memorizing the ON CONFLICT syntax. It's enough to remember that you are allowed to take an action other than error when a constraint is violated.
