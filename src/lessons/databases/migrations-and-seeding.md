# Bonus: Migrations and Seeding

Migrations and Seeds are two tools that teams of developers use to keep their
database schemas in sync with each other.

## Migrations

Your application expects the schema to have a particular shape. When you change
the schema, you often change the code too.

Using Git, it's easy (well, at least possible) to share your code changes. How
do you share your schema changes?

The answer is _migrations_.

Database migrations are a way to change the structure of a database schema over time, in a controlled and organized manner. They are often used in software development to evolve the database schema as the application code changes.

Database migrations typically involve applying a series of incremental changes to the database schema, called migration scripts. Each migration script represents a specific change to the schema, such as adding a new table or column, modifying an existing column, or removing a table. The scripts are executed in a specific order to bring the database schema from one version to another.

The process of applying migration scripts is typically automated by a migration tool, which keeps track of which scripts have been executed and in what order. The tool is able to compare the current schema version with the desired version and execute the necessary scripts to bring the database up to date. This ensures that the database schema is always in a known, consistent state, and that any changes made to the schema are tracked and can be easily rolled back if necessary.

Database migrations are important because they enable teams to make changes to the database schema without affecting the data stored in the database, and without having to manually make changes to the database. They also provide a way to version and rollback the database schema, which helps to ensure the integrity of the data.

## Example: Customers database migrations over time

Migrations are often created in response to changing needs. This small story
illustrates how migrations might help evolve a "customers" database over time.

1. We need to track customers!

First, the business recognizes that it needs to track customers. It creates a
migration for creating the customers table:

```sql
-- 001_create_customers_table.sql
CREATE TABLE customers (
  id INT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) UNIQUE NOT NULL,
  address VARCHAR(255),
  created_at TIMESTAMP DEFAULT NOW()
);
```

Every developer can run this sql on their system to bring their local database
schema up to date. The primary database server also runs this migration, and the
application begins tracking customers.

2. Customer support needs phone numbers!

The customer support team has asked that we track a phone number for every 
customer in the database.

Here's the migration for adding phone numbers to the customer table:

```sql
-- 002_add_phone_number_to_customer.sql
ALTER TABLE customers ADD phone_number VARCHAR(20);
```

Now we can track the phone numbers.

3. Missing addresses

The shipping team has complained that they have to call customers because they
don't have an address on file. They have painstakingly collected and updated the
address for every customer, so there are no more NULLs in the table. Now, you
want to change the table so that no more NULLs can be added.

Here's the sql:
```sql
-- 003_make_customer_address_non_null.sql
ALTER TABLE customers MODIFY address VARCHAR(255) NOT NULL;
```

4. Adding a foreign key constraint for a orders table

Business is growing, and you're now encountering different kinds of bugs. Here's
the latest one: Shipping has complained that some orders are missing customers!

You can fix it by adding a _referential integrity constraint_. The database will
ensure that every order has a customer_id, and that the customer_id refers to an
actual customer in the database. Here's the sql:

```sql
-- 004_order_customer_id_referential_integrity.sql
ALTER TABLE orders
ADD CONSTRAINT fk_orders_customers
FOREIGN KEY (customer_id) REFERENCES customers(id);
```

5. Getting rid of the phone numbers

The customer support team has shifted to exclusively using email for support
(phone calls took too much time). Now they want to get rid of the phone numbers
for all the customers:

```sql
-- 005_remove_customer_phone_number.sql
ALTER TABLE customers DROP COLUMN phone_number;
```

6. Becoming a services business

It's been decided that instead of selling products to _customers_, the company
will now sell consulting services to _clients_. Now you are renaming the table.

```sql
-- 006_rename_customers_to_clients.sql
RENAME TABLE customers TO clients;
```

Each time a new migration is introduced, all of the developers can keep their
databases in sync by running the migrations in order. The migrations help the
team track and manage the changes to the database schema, in response to
business needs.

For databases in real organizations, there are often hundreds of migrations, to
represent all of the changes to the database over time!

## Seeding

Seeding a database refers to the process of inserting default or initial data into a database. This data is typically used to populate the database with a set of known data, which is required for the application to function correctly. The data can be inserted directly into the database using SQL statements, or it can be done through a script or application code.

Seeding a database can be useful in various scenarios, for example:

- When a new database is created, it can be seeded with data that is needed for the application to function correctly.
- When an application is being developed, it's often useful to have a set of test data that can be used for debugging and testing the application.
- When an application is deployed to a production environment, it can be seeded with data that is required for the application to function correctly.

The data that is used for seeding a database can be stored in a variety of formats, such as CSV, JSON, or XML, and it can be read into the database using a variety of tools, such as SQL scripts, ORM libraries or other database management libraries.

## Further reading: Seeding

For more on seeding, check out the [Prisma docs on seeding](https://www.prisma.io/docs/guides/database/seed-database)
