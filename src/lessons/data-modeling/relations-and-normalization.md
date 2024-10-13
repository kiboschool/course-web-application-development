#  Tables Normalization

While designing databases, sometimes we need some guidance or best practices to ensure an optimal database design, table normalization is one of them.

Table normalization is a systematic approach used in designing relational database tables to minimize data redundancy and ensure data integrity. It involves organizing the columns (attributes) and tables (relations) of a database to ensure that their dependencies are maintained properly.

## Video: Learn the process of table normalization

This video walks through all of the different kinds of data consistency errors and the normal forms that can make those inconsistencies impossible.

<div class="embed"><iframe src="https://www.youtube.com/embed/GFQaEYEc8_8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></div>

## Anomalies and Inconsistencies

When designing a schema, you want to make sure the data is correct, consistent, and easy to work with.

Here's a poorly-designed _orders_ table that also stores information about the _product_ and _customer_.

```sql
CREATE TABLE orders (
  order_id INTEGER PRIMARY KEY AUTOINCREMENT,
  customer_id INTEGER,
  customer_name TEXT,
  address TEXT,
  product_id TEXT,
  product_name TEXT,
  quantity INTEGER,
  price DECIMAL(10, 2)
);
```

| order_id | customer_id | customer_name | product_id | product_name | quantity | price |
|---|---|---|---|---|---|---|
| 0 | 2 | Mary | 1 | leg warmers | 3 | 23 |
| 1 | 2 | Mary | 4 | shoes | 10 | 21 |
| 2 | 2 | Mary | 6 | towel | 3 | 40 |
| 3 | 4 | Chukwuemeka | 1 | leg warmers | 9 | 32 |
| 4 | 1 | Simon | 1 | leg warmers | 5 | 33 |
| 5 | 1 | Simon | 5 | chocolate | 10 | 45 |
| 6 | 1 | Simon | 4 | shoes | 8 | 46 |

This schema can lead to all kinds of problems!

* **Update anomalies**: If you update the name for a customer, you could update it for _all_ of that customer, or just some. After running `UPDATE orders SET customer_name = "Gideon" WHERE order_id = 2;`, what is the name of the customer with `id = 2`? It could be either Mary or Gideon. The database is inconsistent!

* **Insert anomalies**: With this schema, if a customer has not placed any orders, there's no good way to add them to the database.

* **Delete anomalies**: A delete anomaly occurs when deleting data from one part of a database leads to unintended consequences. For example, if Chukwuemeka cancels order number 3 for leg warmers, then that whole customer is deleted too!

* **Data redundancy**: Data redundancy is when the same data is stored in multiple places, leading to data storage inefficiencies and an increased risk of inconsistencies. Since the same customer information is repeated in multiple rows for different orders, it takes up more space in the database (and can lead to the issues noted above). 

## Why do we need table normalization?

Table Normalization prevents the anomalies above. In short, it requires that you create different tables for the different "things" in your system.

To normalize the orders, customers, and products from the example and prevent inconsistencies, you would need to separate the data into separate tables and establish relationships between them.

```sql
CREATE TABLE customers (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT,
  address TEXT
);

CREATE TABLE products (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT,
  price DECIMAL(10, 2)
);

CREATE TABLE orders (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  customer_id INT NOT NULL,
  product_id INT NOT NULL,
  quantity INT,
  FOREIGN KEY (customer_id) REFERENCES customers(id),
  FOREIGN KEY (product_id) REFERENCES products(id)
);
```

In this example, the customers table stores customer information, the products table stores product information, and the orders table stores order information. 

With this design, changing customer information will only affect the customers table, and deleting an order will only delete the order information, not the related customer information.

Notice also the use of constraints to ensure the data stays consistent. You've seen the PRIMARY KEY and NOT NULL constraints already, which ensure that those columns are present and, for primary keys, unique. The orders table also has _foreign key constraints_ that reference the primary keys of the customers and products tables, establishing relationships between the data.

## Rules of Normalization

These aren't all of the normalization rules, but if you keep these in mind, you'll end up with better database designs.

1. Store data in separate tables. Each kind of item should be stored in its own table, rather than all data being stored in a single table.

2. Avoid repeating data. Data should not be repeated in multiple places, and instead should be stored in one location and referenced from other tables as needed.

3. Columns should only contain single values. Don't put a list in a single column!

4. Minimize data dependencies. If updating one field or row would mean that you need to update another row in order to stay consistent, there might be a better way to design the schema so that it's impossible to "forget to update" part of the data.
