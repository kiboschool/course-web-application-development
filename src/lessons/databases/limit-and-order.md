# Limit and Order

In SQL, the LIMIT and ORDER BY clauses are used to retrieve a specific subset of records from a table, and to control the order in which the records are returned.

## LIMIT

The LIMIT clause is used to limit the number of rows returned in a query. The syntax for the LIMIT clause is as follows:

```sql
SELECT column1, column2, ... FROM table_name LIMIT number;
```
For example, you can use the following query to retrieve the first 10 customers from the customers table:

```sql
SELECT first_name, last_name FROM customers LIMIT 10;
```

## ORDER BY

The ORDER BY clause is used to sort the results of a query by one or more columns. The syntax for the ORDER BY clause is as follows:

```sql
SELECT column1, column2, ... FROM table_name ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...;
```

For example, you can use the following query to retrieve all customers from the customers table and sort them by last name in descending order:

```sql
SELECT first_name, last_name FROM customers ORDER BY last_name DESC;
```

## Combining LIMIT and ORDER BY

The ORDER BY clause is often used in conjunction with the LIMIT clause to retrieve a specific subset of records and sort them in a specific order. For example, you can use the following query to retrieve the first 10 customers from the customers table and sort them by last name in ascending order:

```sql
SELECT first_name, last_name FROM customers ORDER BY last_name ASC LIMIT 10;
```

You can also use multiple columns for ordering. For example, you can use the following query to retrieve all customers from the customers table and sort them by city in ascending order and last name in descending order:

```sql
SELECT first_name, last_name, city FROM customers ORDER BY city ASC, last_name DESC;
```

Keep in mind that the order of the columns in the SELECT statement doesn't affect the order of the result set, the order is defined by the ORDER BY clause.

## Practice: Limit and Order

Read the SQLBolt lesson on filtering and sorting results:

- [SQL Lesson 4: Filtering and sorting Query results](https://sqlbolt.com/lesson/filtering_sorting_query_results)

Practice the interactive exercise to improve your SQL skills.
