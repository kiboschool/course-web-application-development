# Setting up a SQLite database

### SQLite

SQLite is a convenient database that we'll use throughout the course:
- it stores data in a file, which is convenient for seeing, sharing, and
    understanding databases
- it's a real database. It supports a full version of SQL, and it's the most 
  widely deployed SQL database.
- Python includes an sqlite3 library, so there's less to install or configure

### SQLite from the Terminal

Check that SQLite is installed:

```
sqlite3 --version
```

If it is not installed, you can install it using your package manager (scoop or
brew).

You can run `sqlite3 [name-of-db-file]` to connect to a file-backed database and 
using the SQLite CLI interface.

Download the [countries dataset](https://www.kaggle.com/datasets/robbcobb/countries)
from Kaggle so you have some interesting data to explore. (You may need to
create an account).

Unzip and move the file to a directory, then run it with `sqlite3`:

```
❯ sqlite3 countries_database.sqlite
SQLite version 3.37.0 2021-12-09 01:34:53
Enter ".help" for usage hints.
sqlite>
```

If you enter `.help` you can see a full listing of the _sqlite commands_ that
can change settings or show you meta information.

Now that you have the database open, you are ready to start executing SQL
commands! 

```
sqlite> SELECT * FROM countries;
```

If you run this, you should see a bunch of country data.

See the next few pages on querying and filtering for more about SQL syntax and
what you can do with queries.

### SQLite from Python

To connect a Python program to your SQLite database, you need to
- import the `sqlite3` library
- connect to the database (often by specifying a file)
- execute queries

Here's what that looks like in Python:

```python
import sqlite3

DATABASE_FILE = 'countries_database.sqlite'

db = sqlite3.connect(DATABASE_FILE)
cursor = db.execute('SELECT * FROM countries')
print(cursor.fetchone())
```

You'll learn more about how to use SQLite from Python over the next few lessons.

A few quick tips:
- `db.execute` takes in a query and returns a _cursor_ object (not the results).
    You have to call `.fetchone` or `.fetchall` to get results
- `fetchone` returns a _tuple_ with all of the data for the first row. Calling
    `fetchone` again returns the next row.
- `fetchall` returns all of the rows, as a _list of tuples_.

### Further reading: When to use SQLite - or not

SQLite's documentation includes a page explaining appropriate uses. 

See the page [Appropriate Uses for SQLite](https://www.sqlite.org/whentouse.html)
to learn more about when SQLite is and is not the right choice of database.
