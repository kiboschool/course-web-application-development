# Intro to express

Express.js, often referred to simply as "Express," is a minimalistic web framework for Node.js. It provides a robust set of features for web applications.

### Key Features of Express.js

1. **Minimalistic and Flexible:** Express is unopinionated, meaning it doesn't force any particular way of organizing your application. This gives developers the freedom to choose libraries, structure their code, and define their workflow as they see fit.
2. **Middleware Support:** Middleware are functions that have access to the request object, the response object, and the next function in the application’s request-response cycle. They form the backbone of an Express application, allowing developers to augment requests, handle errors, and more.
3. **Routing System:** Express provides a sophisticated routing system, allowing developers to define routes based on HTTP methods, paths, and parameters.
4. **Performance:** Being built on Node.js, Express benefits from its non-blocking, event-driven architecture, resulting in high performance and scalability.
5. **Vast Ecosystem:** Express, being a part of the Node ecosystem, has access to the vast npm registry, which is filled with countless modules and packages to assist in your development process.

### Hello World with Express.js

Setting up a basic Express application is straightforward. Here's a simple "Hello World" example to get you started:

1. **Setting Up:**
   Begin by initializing a new Node.js project and installing Express:

```bash
mkdir express-demo
cd express-demo
npm init -y
npm install express
```

2. **Creating the Application:**
   In your project directory, create a file named `app.js`. Add the following code:

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Hello World!');
});

const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});
```

3. **Running the Application:**
   In your terminal, run the application:

```bash
node app.js
```

Now, if you navigate to `http://localhost:3000` in your web browser, you'll be greeted with the message "Hello World!"