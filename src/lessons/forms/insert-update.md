# INSERT, UPDATE, and DELETE

So far, the only thing we've done with data submitted from forms is to show it back to the user.

But, usually, that's not all we want to do! Other things we might want to do with form data:

* Log the user into the site
* Make an HTTP request to another service with the data
* Compute some logic based on the data

Or, what we're going to focus on now:

* Store the data in a database

First, let's focus on the SQL syntax for creating, updating, and deleting rows. Then, we'll focus on how to connect that to our form submission for an end-to-end example.

## Saving new data with INSERT

If you made it further in the SQL practice, you've probably seen hints of the INSERT statement. It's how you add a new row to a SQL table.
The syntax for a SQL INSERT statement is as follows:

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

* `INSERT INTO` is used to indicate that you're inserting data into a table.
* `table_name` is the name of the table where the data will be inserted.
* `(column1, column2, column3, ...)` is a list of the columns in the table where the data will be inserted. This is optional and only necessary if you want to specify which columns the data should be inserted into.
* `VALUES` is used to indicate the values that will be inserted into the table.
* `(value1, value2, value3, ...)` is a list of the values that will be inserted into the table, in the same order as the columns specified.

For example, if you have a table called "employees" with columns "id", "name", and "salary", you could insert a new employee into the table with the following SQL statement:

```sql
INSERT INTO employees (id, name, salary)
VALUES (16, 'Oluwaseun Oyebola', 50000);
```

This would insert a new employee with an id of 16, a name of "Oluwaseun Oyebola", and a salary of 50000 into the "employees" table.

### Video: Inserting Data

Here's a pair of videos on inserting data into a SQLite database. The first shows how to run an INSERT statement, and the second provides more details about inserting and placeholders with the Python sqlite module.

- [How to insert into a SQLite database in Python](https://www.youtube.com/watch?v=NPWA5AkGuaM)
- [Python SQLite Tutorial (Youtube)](https://www.youtube.com/watch?v=pd-0G0MigUA)

## Updating data with UPDATE

To change an existing row in a table, you use the UPDATE statement.

The syntax for a SQL UPDATE statement is as follows:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE some_column = some_value;
```

* `UPDATE` is used to indicate that you're updating data in a table.
* `table_name` is the name of the table where the data will be updated.
* `SET` is used to indicate the new values that will be set for the columns in the table.
* `column1 = value1, column2 = value2, ...` is a list of the columns and their new values that will be set.
* `WHERE some_column = some_value` is used to specify which rows in the table will be updated.

**Important**: Do not forget the WHERE clause in an UPDATE statement! If you don't include a WHERE, you will update _all rows_.

For example, if you have a table called "employees" with columns "id", "name", and "salary" and you want to update the salary of the employee with id 16 to 100000, you could use the following SQL statement:

```sql
UPDATE employees
SET salary=100000
WHERE id = 16;
```

This would update the salary of the employee with id 16 to 100000 in the "employees" table.

Here's a quick video on updating and deleting data in SQL: [Updating/Deleting Data (YouTube)](https://www.youtube.com/watch?v=bhnrIforc7s)

## Deleting Data with DELETE

To remove a row from a table, you use the DELETE statement.

The syntax for a SQL DELETE statement is as follows:

```sql
DELETE FROM table_name
WHERE some_column = some_value;
```

* `DELETE FROM` is used to indicate that you're deleting data from a table.
* `table_name` is the name of the table where the data will be deleted.
* `WHERE some_column = some_value` is used to specify which rows in the table will be deleted.
 
For example, if you have a table called "employees" with columns "id", "name", "salary" and you want to delete the employee with id=1 you could use the following SQL statement:

```sql
DELETE FROM employees
WHERE id = 1;
```

This would delete the row with id=1 from the "employees" table.

It is important to note that DELETE statements without a WHERE clause will delete all rows from the table! Always include a condition to specify which rows should be deleted.

### Practice: SQLBolt Insert, Update, and DELETE

Practice the syntax for INSERT, UPDATE, and DELETE with SQLBolt:

- [SQL Lesson 13: Inserting rows](https://sqlbolt.com/lesson/inserting_rows)
- [SQL Lesson 14: Updating rows](https://sqlbolt.com/lesson/updating_rows)
- [SQL Lesson 15: Deleting rows](https://sqlbolt.com/lesson/deleting_rows)

## Inserting form data into the database in Flask

Now we have all the tools we need to save form data submitted to the server to the database.

We'll need:
- a route to serve the html form
- the form itself, with inputs, action, and method
- a route to handle the form submission
- logic to insert the data into the database

```python
from flask import Flask, request, render_template
import sqlite3

app = Flask(__name__)

def connect_db():
    return sqlite3.connect('employees.db')

@app.get('/new_employee')
def new_employee_form():
    return render_template('new_employee.html')

@app.post('/create_employee')
def create_employee():
  name = request.form['name']
  salary = request.form['salary']
  conn = connect_db()
  c = conn.cursor()
  c.execute("INSERT INTO employees (name, salary) VALUES (?,?)", (name, salary))
  conn.commit()
  conn.close()
  return 'Employee added.'
```

```html
<!-- new_employee.html -->
<form method="post" action="/create_employee">
  Name: <input type="text" name="name"><br>
  Salary: <input type="number" name="salary"><br>
  <input type="submit" value="Add Employee"><br>
</form>
```

In this example, we have a route `/new_employee` that serves the HTML form. The form has inputs for the name and salary. The `action` and `method` attributes tell the browser where and how to submit the form data.

When a user clicks the "Add Employee" button, the browser submits the form with a POST request to the `/create_employee` route. The request is handled by the `create_employee` function. The form data is accessed using `request.form`. Then, we open a connection to the database and insert the form data into the "employees" table, using an `INSERT` statement.

## Preview: Validation and SQL Injection

In this example, there is no validation for the name or salary submitted in the form. The user could enter _anything_! That means that the data going into the database could end up being nonsense, like a blank name or a salary less than 0.

The _good_ thing about this example is that it does not allow SQL injection. The sqlite `execute` method lets you add _placeholders_ in the query and pass in arguments to fill them in:

```python
c.execute("INSERT INTO employees (name, salary) VALUES (?,?)", (name, salary))
```

The `execute` method replaces the `?` placeholders with the values `name` and `salary` _safely_. It makes sure that the values won't get mixed up with the SQL code, so that the query is safe to execute.

When querying the database, **never use string concatenation to build the query yourself**. 

In the next lessons, you'll learn more about validation and SQL injection. 

## Preview: SQLAlchemy and ORMs

You've been learning to write SQL queries by hand, so that you understand what's happening under the hood. In many large web applications, developers use libraries that manage the database connection, send queries, and turn the response from the database into Python objects. Libraries that do this are called _ORMs_, for Object-Relational Mappers.

A very popular Python ORM is called SQLAlchemy. By using it, you can write queries like

```python
User.query.filter_by(id=15).first()
```

instead of using the SQLite library to write a query like:

```python
conn.execute("SELECT * FROM users WHERE id = ?;", 15).fetchone()
```

The same (or very similar) SQL will be generated by the ORM, and the same result is returned from the database. Especially for more complicated queries, an ORM can be easier than writing SQL statements by hand.

Here's a video on [using Flask-SQLAlchemy to insert, update, and delete data](https://www.youtube.com/watch?v=FEyNt9iFPGc).
