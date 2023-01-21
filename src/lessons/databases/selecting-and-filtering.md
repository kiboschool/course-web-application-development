# Selecting and filtering

In SQL, you can filter records by using the `WHERE` clause in a `SELECT`, `UPDATE`, or `DELETE` statement. The `WHERE` clause specifies a condition that must be true for a row to be included in the result set or affected by the statement. The syntax for a basic WHERE clause is as follows:

```sql
SELECT column1, column2, ... FROM table_name WHERE condition;
```

For example, you can use the following query to retrieve all customers whose last name is "Smith" from the customers table:

```sql
SELECT first_name, last_name FROM customers WHERE last_name = 'Smith';
```

## Multiple conditions with AND, OR, and NOT

You can also use multiple conditions in the WHERE clause to filter records using the AND, OR and NOT operators.

```sql
SELECT column1, column2, ... FROM table_name WHERE condition1 AND/OR/NOT condition2;
```

For example, you can use the following query to retrieve all customers whose last name is "Smith" and live in the city "New York":

```sql
SELECT first_name, last_name, city FROM customers WHERE last_name = 'Smith' AND city = 'New York';
```

## Other operators: BETWEEN, LIKE, IN, IS NULL

Additionally, you can use the BETWEEN operator to filter records based on a range of values. For example, you can use the following query to retrieve all customers whose age is between 25 and 40:

```sql
SELECT first_name, last_name, age FROM customers WHERE age BETWEEN 25 AND 40;
```

You can also use the LIKE operator to filter records based on a pattern. For example, you can use the following query to retrieve all customers whose first name starts with the letter "J":

```sql
SELECT first_name, last_name FROM customers WHERE first_name LIKE 'J%';
```

You can also use the IN operator to filter records based on a list of values. For example, you can use the following query to retrieve all customers whose city is either "New York" or "Los Angeles":

```sql
SELECT first_name, last_name, city FROM customers WHERE city IN ('New York', 'Los Angeles');
```

You can also use the IS NULL operator to filter records where a specific column contain null value. For example, you can use the following query to retrieve all customers whose phone number is null:

```sql
SELECT first_name, last_name, phone FROM customers WHERE phone IS NULL;
```

These are just a few examples of how you can filter records in SQL, and there are many other ways to filter data depending on the specific needs of your query.

## Practice: Constraints and Filtering in SQLBolt

Read the SQLBolt lessons on constraints and filtering:

- [SQL Lesson 2: Queries with constraints (Pt. 1)](https://sqlbolt.com/lesson/select_queries_with_constraints)
- [SQL Lesson 3: Queries with constraints (Pt. 2)](https://sqlbolt.com/lesson/select_queries_with_constraints_pt_2)

Practice with the interactive exercises to solidify your SQL syntax.
