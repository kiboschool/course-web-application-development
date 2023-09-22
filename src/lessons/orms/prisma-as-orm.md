# Prisma as ORM

So let's set up a simple app with prisma and Javascript.

By the way, Prisma can also be used in python with Flask.  However, this week we will use Express and JavaScript.

## Setting Up Prisma with Express.js

### 1. Installation:

Create the folder app and navigate into it
```bash
mkdir prisma-test
cd prisma-test
```

Start by initializing a new Node.js project if you haven't already:

```bash
npm init -y
```

Install all required dependences

```bash
npm install prisma @prisma/client express
```

Now, set up Prisma for your project:

```bash
npx prisma init --datasource-provider sqlite --url file:./dev.db
```

This command generates a `prisma` directory with 3 files:
- `schema.prisma`. You define all your tables information (also known as models)
- `dev.db`. Contains the database itself. Never touch this file

As well, in the root folder you will have a `.env` file (for environment variables like the DB url).

### 2. Defining Models:

Inside `schema.prisma`, you can define your data models. It's like tables in the SQL universe. 

Here's a basic example with a `User` table (model):

```prisma
model User {
  id    Int     @id @default(autoincrement())
  name  String
  email String  @unique
}
```

The above definition creates a `User` with an `id`, `name`, and `email` fields, with `email` being unique.

Copy this code in your `schema.prisma` file

### 3. Integration with Express.js:

In your `root folder` create a file `index.js`.

```bash
touch index.js
```

Now, in your main server file (e.g., `index.js`), set up a basic Express.js application connected to Prisma.

```javascript
const express = require('express');
const { PrismaClient } = require('@prisma/client');

const prisma = new PrismaClient();
const app = express();

app.use(express.json());

// Sample route to fetch all users
app.get('/users', async (req, res) => {
    const users = await prisma.user.findMany();
    res.json(users);
});

const PORT = 8000;
app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});
```

This sets up a basic Express server with a single route to fetch all users from the database.


### 4. Seeding the Database:

To seed the database (add some test users into DB) with Prisma, we'll add a seeding script.

Create a new file called `seed.js` in the prisma folder of your project (`prisma/seed.js`). In this file, you'll add the logic to insert sample users into the database:

```javascript
const { PrismaClient } = require('@prisma/client');

const prisma = new PrismaClient();

async function main() {
    await prisma.user.create({
        data: {
            name: 'John Doe',
            email: 'john.doe@example.com',
        },
    });

    await prisma.user.create({
        data: {
            name: 'Jane Smith',
            email: 'jane.smith@example.com',
        },
    });

    // You can add more users or other data as needed
}

main()
    .catch(e => {
        console.error(e);
        process.exit(1);
    })
    .finally(async () => {
        await prisma.$disconnect();
    });
```

### 5. Migrating the Database:

So far you only created the "mould of your information". But the database is empty, you need to create the tables and run the seed file to populate this tables. This process is called migration:

In your terminal run:

```bash
npx prisma migrate dev --name init
```

### 6. Run your app

Finally run:

```bash
node index.js
```

This command will run the Express server in port 8000 (`http://localhost:8000`) and navigate to the `http://localhost:8000/users` endpoint, you'll see the seeded users in the response. 

