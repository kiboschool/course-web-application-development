# SQL Injection

SQL injection is a type of security vulnerability that allows an attacker to insert malicious code into an SQL statement, usually through an unprotected user input in a web application. The injected code can then be executed by the database, potentially giving the attacker access to sensitive data or allowing them to make unauthorized changes to the database.

## Video: Building a SQL Injection Attack

This video shows the attacker's perspective on attacking a website. It walks through building a basic SQL injection attack, and then how to use various tools to analyze and protect vulnerabilities.

<div class="embed"><iframe src="https://www.youtube.com/embed/cx6Xs3F_1Uc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></div>

> There's a lot of extras in this video about security and networking. We're focused on SQL injection right now, so don't worry about all of the other tools and terms.

## What is SQL injection?

For example, let's say a web application has a login form that takes a username and password and checks them against a database to see if they match. 

If the application is not properly protected, an attacker could enter a malicious username and password like this:

```
username: admin
password: anything' OR '1'='1
```

This would cause the application to create an SQL statement like this:

```sql
SELECT * FROM users WHERE username = 'admin' AND password = 'anything' OR '1'='1';
```

The result is that the query will find the admin user, even without the correct password. The attacker could gain access to the system, and cause all kinds of havoc.

To prevent SQL injection, you can use _prepared statements_ or _parameterized queries_ and use libraries that to handle input validation and sanitization. Always validate input before using it in a query.

And the biggest rule of all:

> **Do not concatenate user input into SQL statements** 

## Example: vulnerable Flask code

> This is **bad** code, because an attacker could write a SQL injection. 
> Don't copy this code into a real application!

```python
from flask import Flask, request, render_template
app = Flask(__name__)

def connect_db():
    return sqlite3.connect('employees.db')

@app.get("/login")
def show_login():
  return render_template("login.html")

@app.post("/login")
def handle_login():
  username = request.form["username"]
  password = request.form["password"]
  conn = connect_db()
  user = conn.execute("SELECT * FROM users WHERE username = '" + username + "' AND password = '" + password + "';").fetchone()
  if user:
    return show_user_page()
  else:
    redirect("/login", error="User not found")
```

An attacker could submit a password like `"anything' OR '1'='1"`, and the resulting SQL would be

```sql
SELECT * FROM users WHERE username = 'admin' AND password = 'anything' OR '1'='1';
```

This would return the admin user, even without knowing the password!

> Note: this example also assumes that passwords are stored in plain text in the database. That's another bad idea! It's important to hash passwords and compare against the hashes, instead of using the database query like this. This is just example code.

## Preventing SQL injection

The reason SQL injection can happen is that some characters have a special meaning in the SQL syntax. Characters like `'` and `;` and `--` are not just values, they tell SQL where values and commands start and stop.

To prevent users from including these characters in the SQL query, the input is _sanitized_. Those characters are _escaped_, so they don't count as SQL syntax.

> Don't try to sanitize queries yourself. Don't build SQL statements by hand.

It's quite easy to mess up when sanitizing inputs. Instead, you can rely on the sqlite3 module, which automatically sanitizes parameters to the `execute` method. Here's fix for the code above that uses placeholders, and sanitizes the inputs.


```python
user = conn.execute("SELECT * FROM users WHERE username = ? AND password = ?;", (username, password)).fetchone()
```

The execute method sanitizes the password, so it doesn't contain the raw `'` character any more.
