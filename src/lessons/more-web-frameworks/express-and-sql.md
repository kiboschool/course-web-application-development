# Express and SQL

As we covered before, it's often necessary to store and retrieve data, and this is where databases come into play. SQLite, known for its lightweight and serverless nature, is a popular choice for various applications.

We'll guide you through integrating SQLite with an Express application.

#### Setting Up SQLite with Express.js

To integrate SQLite with Express, we'll make use of the `sqlite3` module available on npm.

1. **Installation**:

```bash
npm install sqlite3
```

2. **Setting up the Database Connection**:
```javascript
const express = require('express');
const sqlite3 = require('sqlite3').verbose();

const app = express();
const PORT = 3000;

// Middleware for parsing POST request bodies
app.use(express.json());

// Connect to SQLite database
const db = new sqlite3.Database('./database.db', (err) => {
    if (err) {
        console.error("Error connecting to database:", err);
    } else {
        console.log('Connected to SQLite database.');
    }
});

// Create the "users" table if it doesn't exist
const createTableQuery = `
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL
)`;

// execute query
db.run(createTableQuery, (err) => {
    if (err) {
        console.error("Error creating table:", err);
    }
});

// Route to register a new user
app.post('/register', (req, res) => {
    const { username, email } = req.body;
    const insertQuery = "INSERT INTO users (username, email) VALUES (?, ?)";

    db.run(insertQuery, [username, email], function(err) {
        if (err) {
            return res.status(400).json({ error: err.message });
        }
        // `this` refers to the statement object, and `lastID` contains the ID of the last inserted row.
        res.json({ id: this.lastID, message: "User registered successfully!" });
    });
});

// Route to fetch a user by their ID
app.get('/user/:id', (req, res) => {
    const userId = req.params.id;
    const fetchQuery = "SELECT * FROM users WHERE id = ?";

    db.get(fetchQuery, [userId], (err, row) => {
        if (err) {
            return res.status(400).json({ error: err.message });
        }
        res.json(row);
    });
});

// Start the Express server
app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});

// Handle exiting the application
process.on('exit', () => {
    db.close((err) => {
        if (err) {
            console.error(err.message);
        }
        console.log('Closed the SQLite database connection.');
    });
});
```

As you can see the app is doing:

1. **Initialization**:
    - Necessary modules (`express`, and `sqlite3`) are imported.
    - An Express application instance (`app`) is created.

2. **Middleware Configuration**:
    - The `express.json()` middleware is added to the Express application. This enables the app to parse incoming POST request bodies, which is essential when handling form data submissions.

3. **Database Connection and Setup**:
    - A connection to an SQLite database (`database.db`) is established.
    - If the database doesn't exist, SQLite will create a new file named `database.db`.
    - A table named `users` is created if it doesn't already exist. This table is designed to store user information, with columns for `id`, `username`, and `email`.

4. **Routes**:
    - **Registration Route (`/register`)**: 
        - It's a POST route designed to register a new user.
        - The submitted `username` and `email` are extracted from the request body.
        - The data is then inserted into the `users` table in the SQLite database.
        - A JSON response is sent back, containing the ID of the newly registered user and a success message.
    - **User Retrieval Route (`/user/:id`)**:
        - It's a GET route to retrieve a user's details based on their ID.
        - The user ID is extracted from the route parameter (`:id`).
        - A database query fetches the corresponding user's details and returns them as a JSON response.

5. **Server Start**:
    - The Express server is set to listen on port `3000`.
    - A console log confirms when the server starts and provides the URL to access the app.

6. **Shutdown**:
    - An event listener is added to handle the `exit` event of the application process.
    - When the application is about to exit, the SQLite database connection is closed gracefully.
    - A message confirming the closure of the database connection is logged to the console.
