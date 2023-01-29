# Foreign Keys and JOINS

So far, we've been focused on databases with just one table. In most web applications, there are many tables, with complicated relationships between the items in the tables.

Foreign keys and JOINs are the basic SQL tools for creating and using relationships between tables.

## Video: Linking Tables with Keys

This video illustrates linking the Primary key of one table with the Foreign key of another table:

<div class="embed"><iframe src="https://www.youtube.com/embed/B5r8CcTUs5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></div>

## FOREIGN KEY

**Foreign keys** are a way of linking data in two different tables in a relational database. They are used to establish a relationship between two tables, where the values in one table depend on the values in another table.

A foreign key is a column or set of columns in one table that refer to the primary key of another table. The purpose of a foreign key is to ensure data integrity, which means that the data in the database is consistent and accurate.

For example, consider a database that has two tables: a `customers` table and an `orders` table. The `customers` table contains information about customers, including a unique identifier for each customer, which is the primary key. The `orders` table contains information about the orders placed by each customer, including the customer's identifier. 

```sql
CREATE TABLE customers (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  email TEXT NOT NULL UNIQUE
);

CREATE TABLE orders (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  customer_id INTEGER NOT NULL,
  product TEXT NOT NULL,
  quantity INTEGER NOT NULL,
  FOREIGN KEY (customer_id) REFERENCES customers (id)
);
```

The `customer_id` column in the `orders` table is a foreign key. It refers to the primary key of the customers table. It tells us which customer the order belongs to.

The `FOREIGN KEY` statement is a _database constraint_. It creates a relationship between the two tables, where each order in the orders table must correspond to a customer in the customers table. If you try to insert an order into the orders table with a customer_id that doesn't exist in the customers table, you'll get an error.

## JOIN

The SQL `JOIN` statement is used to combine rows from two or more tables based on a related column between them.

Here's an example of a JOIN statement: 

```sql
SELECT customers.name, orders.product
FROM customers
JOIN orders
ON customers.id = orders.customer_id;
```

The `JOIN` statement combines the rows from the `customers` and `orders` tables based on the `customer_id` column. The result of this query contains the name from the customers table and product from the orders table, with each row representing a customer and their corresponding order.

If a customer has multiple orders, each order will appear as a separate row in the results.

## Practice: Writing JOINs

Practice JOINs on SQLBolt

[SQL Lesson 6: Multi-table queries with JOINs](https://sqlbolt.com/lesson/select_queries_with_joins)

### Other kinds of JOIN

The most common kind of `JOIN` is the `INNER JOIN`. If you don't specify another kind of join, it will treated as an `INNER JOIN`.

There are several types of JOIN statements in SQL, each of which returns different subsets of the data from the joined tables.

- `INNER JOIN`
- `LEFT JOIN`
- `RIGHT JOIN`
- `FULL OUTER JOIN`

The names correspond to the portions of a Venn diagram of the tables:

![SQL joins diagram](https://learnsql.com/blog/learn-and-practice-sql-joins/2.png)

An `INNER JOIN` returns only the rows that have matching values in both tables.

The other three joins are all 'outer' joins in some sense, since they include 'outer' values (not just inner ones).

A `LEFT JOIN` returns all the rows from the left table and the matching rows from the right table. If there is no matching row in the right table, the result will contain `NULL` values for the columns from the right table.

A `RIGHT JOIN` is similar to a `LEFT JOIN`, but it returns all the rows from the right table and the matching rows from the left table.

A `FULL JOIN` returns all the rows from both tables, including the rows that have no matching values in either table.

You'll almost exclusively use the `INNER JOIN` (or just `JOIN`), but occasionally a LEFT or RIGHT JOIN will be helpful. `FULL JOIN` is pretty rare, so you'll probably only see it in tutorials.

## Practice: Outer joins

Practice OUTER JOINs on SQLBolt:

[SQL Lesson 7: OUTER JOINs](https://sqlbolt.com/lesson/select_queries_with_outer_joins)
