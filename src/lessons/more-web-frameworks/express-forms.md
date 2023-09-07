# Express forms

As we covered before, Web forms provide a mechanism for users to submit data to the server, whether it's for registration, search queries, feedback, or other purposes. Express.js, with its minimalistic and flexible nature, offers intuitive ways to handle form data. In this article, we'll delve into managing forms in Express.js, focusing on receiving and sending information using `req.query`, `req.params`, and `res.send`.

#### Setting Up Express with Body Parsing

To handle POST data (like form submissions), Express needs to use [middleware](https://stackoverflow.com/questions/2904854/what-is-middleware-exactly) to parse the incoming request body:

```javascript
const express = require('express');

// middleware is a function to be executed between request and response
app.use(express.json());

// definition of routes
```

#### Receiving Form Data

Forms can send data via GET (typically for search queries) or POST (for submitting data). For GET request, we **do not need** `express.json()` middleware.

1. **GET Data (Query Strings)**: This can be accessed using `req.query`.

   For example, for a URL like `/search?query=express`, you can access the 'query' parameter as:

   ```javascript
   app.get('/search', (req, res) => {
       let searchQuery = req.query.query;
       res.send(`You searched for ${searchQuery}`);
   });
   ```

2. **POST Data**: This can be accessed using `req.body` (thanks to the `express.json()` middleware).

   If your form looks something like this:

   ```html
   <form action="/submit" method="post">
       <input type="text" name="username">
       <input type="submit" value="Submit">
   </form>
   ```

   In Express, you'd handle it as:

   ```javascript
   app.post('/submit', (req, res) => {
       let submittedUsername = req.body.username;
       res.send(`You submitted the username: ${submittedUsername}`);
   });
   ```

3. **Route Parameters**: Accessible using `req.params`, these are useful for dynamic routes.

   For example, in a route like `/user/:username`, you can access the 'username' parameter as:

   ```javascript
   app.get('/user/:username', (req, res) => {
       let username = req.params.username;
       res.send(`You are viewing the profile of ${username}`);
   });
   ```

#### Sending Data Back to the Client

The `res` object in Express provides several methods to send responses back to the client. One of the most commonly used methods is `res.send()`.

1. **Sending a Simple Response**:

   ```javascript
   app.get('/hello', (req, res) => {
       res.send('Hello, world!');
   });
   ```

2. **Sending Form Data Back**:

   For demonstration, if a user submits their name via a form, you can send it back:

   ```javascript
   app.post('/name', (req, res) => {
       let name = req.body.name;
       res.send(`Hello, ${name}!`);
   });
   ```

3. **Sending JSON Data**:

   Express makes it easy to send JSON responses using `res.json()`:

   ```javascript
   app.get('/data', (req, res) => {
       let data = {
           name: "John",
           age: 30
       };
       res.json(data);
   });
   ```
