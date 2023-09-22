# CRUD Operations with Prisma

In the previous article, we've set up an Express application integrated with Prisma. We've also created a basic `User` model and seeded our database with some sample users. Now, let's extend our application to perform more CRUD (Create, Read, Update, Delete) operations and explore various relationships between data models.

## Extending the Data Model

Before diving into CRUD operations, let's introduce more complexity to our data model by adding one-to-one, one-to-many, and many-to-many relationships.

### 1. One-to-One Relationship: `Profile`

Each `User` can have one `Profile`. This represents a one-to-one relationship.

Update your `schema.prisma`:

```prisma
model User {
  id      Int     @id @default(autoincrement())
  name    String
  email   String  @unique
  profile Profile?
}

model Profile {
  id     Int    @id @default(autoincrement())
  bio    String
  userId Int    @unique
  user   User   @relation(fields: [userId], references: [id])
}
```

### 2. One-to-Many Relationship: `Posts`

A `User` can have multiple `Posts`, but each `Post` belongs to one `User`. This represents a one-to-many relationship.

Extend your `schema.prisma`:

```prisma
model User {
  // ... existing fields ...
  posts  Post[]
}

model Post {
  id       Int    @id @default(autoincrement())
  title    String
  content  String?
  authorId Int
  author   User   @relation(fields: [authorId], references: [id])
}
```

### 3. Many-to-Many Relationship: `Categories`

A `Post` can belong to multiple `Categories`, and each `Category` can have multiple `Posts`. This represents a many-to-many relationship.

Further extend your `schema.prisma`:

```prisma
model Post {
  // ... existing fields ...
  categories CategoryOnPost[]
}

model Category {
  id    Int            @id @default(autoincrement())
  name  String         @unique
  posts CategoryOnPost[]
}

model CategoryOnPost {
  postId     Int
  categoryId Int
  post       Post     @relation(fields: [postId], references: [id])
  category   Category @relation(fields: [categoryId], references: [id])

  @@id([postId, categoryId])
}
```

After you've updated your `schema.prisma` don't forget to run the migration command to update your actual database with the new schema:

```bash
npx prisma migrate
```

With our relationships defined, let's explore CRUD operations in plain JavaScript

## CRUD Operations

### 1. Create:

To create a new user:

```javascript
const newUser = await prisma.user.create({
  data: {
    name: "Alice",
    email: "alice@example.com",
  },
});
```

### 2. Read:

Fetch all users:

```javascript
const users = await prisma.user.findMany();
```

### 3. Update:

Update a user's name:

```javascript
const updatedUser = await prisma.user.update({
  where: { email: "alice@example.com" },
  data: { name: "Alicia" },
});
```

### 4. Delete:

Delete a user:

```javascript
const deletedUser = await prisma.user.delete({
  where: { email: "alice@example.com" },
});
```

## Complex CRUD operations

### 1. All posts of a user

```javascript
const posts = await prisma.user.findUnique({
  where: { id: Number(id) },
  select: {
    posts: true,
  },
});
```

### 2. Get all the categories of a post:
```javascript
// Fetch categories for all posts
prisma.post.findMany({
  select: {
    title: true,
    categories: {
      select: {
        category: {
          select: {
            name: true,
          },
        },
      },
    },
  },
});
```

### 3. Fetching Users with Their Latest Post:

```javascript
const usersWithLatestPost = await prisma.user.findMany({
  select: {
    name: true,
    email: true,
    posts: {
      take: 1,
      orderBy: {
        createdAt: 'desc'
      }
    }
  }
});
```

### 4. Count of Posts for Each User:

```javascript
const usersPostCount = await prisma.user.findMany({
  select: {
    name: true,
    email: true,
    _count: {
      select: { posts: true }
    }
  }
});
```

### 5. Users Who Have Written More Than 5 Posts:
To filter users based on the number of posts they've written:

```javascript
const activeUsers = await prisma.user.findMany({
  where: {
    posts: {
      _count: {
        gt: 5
      }
    }
  },
  select: {
    name: true,
    email: true
  }
});
```

### 5. Fetch Posts with Specific Categories:
Let's say you want to fetch all posts that are categorized under "Technology":

```javascript
const techPosts = await prisma.post.findMany({
  where: {
    categories: {
      some: {
        category: {
          name: 'Technology'
        }
      }
    }
  },
  select: {
    title: true,
    content: true
  }
});
```

### 6. Posts Without Any Categories:
Fetching posts that haven't been categorized:

```javascript
const uncategorizedPosts = await prisma.post.findMany({
  where: {
    categories: {
      NONE: {}
    }
  },
  select: {
    title: true,
    content: true
  }
});
```

### 7. Sorting Users by the Number of Posts:

```javascript
const usersByPostCount = await prisma.user.findMany({
  select: {
    name: true,
    email: true,
    _count: {
      select: { posts: true }
    }
  },
  orderBy: {
    _count: {
      posts: 'desc'
    }
  }
});
```

These are just a few examples of what you can achieve with Prisma. The ability to chain conditions, filter based on relationships, and perform aggregations makes Prisma a powerful tool for complex queries.

## Setting Up API Routes in Express.js

Now that we've explored how to write the queries in plain javascript, let's do it with Express.

Extend your `index.js` to handle these basic operations:

```javascript
// Create a new user
app.post("/user", async (req, res) => {
  const { name, email } = req.body;
  const user = await prisma.user.create({
    data: { name, email },
  });
  res.json(user);
});

// Fetch all users
app.get("/users", async (req, res) => {
  const users = await prisma.user.findMany();
  res.json(users);
});

// Update a user
app.put("/user/:id", async (req, res) => {
  const { id } = req.params;
  const { name } = req.body;
  const user = await prisma.user.update({
    where: { id: Number(id) },
    data: { name },
  });
  res.json(user);
});

// Delete a user
app.delete("/user/:id", async (req, res) => {
  const { id } = req.params;
  const user = await prisma.user.delete({
    where: { id: Number(id) },
  });
  res.json(user);
});
```

And of course you can explore:

Try adding more endpoinds with more complex queries as detailed before!