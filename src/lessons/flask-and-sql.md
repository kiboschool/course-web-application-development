# Flask and SQL
Building web applications often requires storing and retrieving data, such as user profiles, posts, or product details. Flask, combined with SQL, makes it very easy to integrate this database functionality into web applications.

Let's explore how to do it.

### Setting Up

Before diving in, ensure you have Flask installed and a project structure ready. For database operations, we'll use the SQLite database through Python's built-in `sqlite3` library.

### Integrating SQLite with Flask

1. Create a brand new Flask app.

2. **Setting up the Database**:
    Create a new file called `db.py` in the *root folder of your app* and paste this code.

    ```python
    import sqlite3

    def init_db():
        db = sqlite3.connect('app.db')
        cursor = db.cursor()
            
        # Create table
        cursor.execute('''
            CREATE TABLE IF NOT EXISTS users (
                id INTEGER PRIMARY KEY,
                username TEXT,
                email TEXT
        )''')
        db.commit()

        print("DB successfully created")

    init_db()
    ```

Now go to your terminal and execute this python file:

```
python db.py
```


As you can see, we are creating a table called users and populating it with 3 fields: id, username and email.

This database is stored in a new filed called `app.db` that is also stored in your root folder. Don't touch this file.

3. Seeding the first data

Now create a new file called `seed.py` in the *root folder of your project* with the following content:

```python
import sqlite3

DATABASE = 'app.db'

def seed_db():
    conn = sqlite3.connect(DATABASE)
    cursor = conn.cursor()
    
    # Sample data
    users = [
        ("Alice", "alice@example.com"),
        ("Bob", "bob@example.com"),
        ("Charlie", "charlie@example.com"),
        ("David", "david@example.com"),
        ("Eva", "eva@example.com")
    ]

    cursor.executemany('INSERT INTO users (username, email) VALUES (?, ?)', users)
    conn.commit()
    conn.close()

    print("Database seeded successfully!")

seed_db()
```

Now run the seed file from your terminal with:

```sh
python seed.py
```

After running the script, your `app.db` will have 5 users. Remember, this script will insert these users every time it's run.

4. **Database Connection from Flask**:
   Open `app.py` and paste the following lines in the beginning:
   
   Establish a connection to the SQLite database when needed:

   ```python
    import sqlite3

    def get_db():
       db = sqlite3.connect('app.db')
       return db
   ```

As you can see, we are creating a new function that will allow us to call the db whenever we need it (most of the time this will be done inside of a route)

5. Fetching Data:

Go to `app.py` again and create a new route with the following code: (don't forget to import render_template)

```python
@app.route('/users')
def users():
    db = get_db()
    cursor = db.cursor()
    cursor.execute('SELECT * FROM users')
    users_list = cursor.fetchall()

    return render_template('users.html', users=users_list)
```

6. Visualization:

Create a template file called`users.html` with the following content:

```html
<ul>
{% for user in users %}
    <li>{{ user[1] }} ({{ user[2] }})</li>
{% endfor %}
</ul>
```

After this step, run your Flask app. You should be able to go to `http://localhost:5000/users` in your browser and see a list of users in your app.