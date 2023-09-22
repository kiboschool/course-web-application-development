# Authorization

The first part of 'auth' (Authentication) is all about proving that a user is who they say they are. We solve with with a JWT token.

The next part, Authorization, is about giving users the right access, based on who they are.

## User-specific data

When a user visits the home page, they expect to see their own data - not someone else's.

One key, but subtle, component of Authorization is fetching data based on the current user. Often, web frameworks (like express) will provide a helper to get the current user from the session, which can then be used to look up data for that user.

```javascript
return {
  posts: currentUser().posts()
}
```

Usually, Authorization refers to checking that a user has access to particular data. If you fetch data related to the user, the assumption is that they have access to that data.

## Basics of Authorization

At it's core, authorization is about if statements. If the user has permission, then continue. If they don't, raise an exception and show a Forbidden response instead of continuing.

Authorization in many apps uses if statements like this, spread throughout the application.

> [This post from Oso](https://www.osohq.com/post/why-authorization-is-hard) runs through some of the reasons why authorization tends to get complicated.

Let's continue the flow we implemented in last session and add protected endpoints. (endpoints that only authenticated users can use). Like geting posts (`/posts`)

This is the code:

```javascript
const express = require('express');
const jwt = require('jsonwebtoken');

const app = express();

app.use(express.json());

// Dummy data representing user posts
const userPosts = {
  "john@email.com": ["Post 1", "Post 2"],
  "jane@email.com": ["Post A", "Post B"]
};

// Endpoint to fetch user posts
app.get('/posts', (req, res) => {
  // Extract the token from the request header
  const token = req.headers['authorization'];

  // If no token is provided, deny access
  if (!token) {
    return res.status(403).send('Access denied. No token provided.');
  }

  try {
    // Verify and decode the token
    const decoded = jwt.verify(token, 'YOUR_SECRET_KEY');
    req.user = decoded; // Store decoded payload for subsequent use
  } catch (error) {
    // If token verification fails, deny access
    res.status(400).send('Invalid token.');
  }
  // Extract user email from the decoded token payload
  const userEmail = req.user.email;

  // Fetch posts for the authenticated user
  const posts = userPosts[userEmail];

  // If there are no posts for the user, send an empty array
  if (!posts) {
    return res.json([]);
  }

  // Send the fetched posts as the response
  res.json(posts);
});
```

As you can see, this endpoint provides a simplified demonstration of how JWT can be used to protect an endpoint and ensure that only authenticated users can access specific resources.

1. **Dummy Data Creation**: A constant `userPosts` is initialized with dummy data to simulate user posts. Each key in this object is an email, and the corresponding value is an array of posts associated with that email.

2. **Define Endpoint**: An endpoint `/posts` is defined to handle GET requests. This endpoint fetches posts for authenticated users.

3. **Token Extraction**: Inside the endpoint, the code attempts to extract a JWT token from the `authorization` header of the incoming request.

4. **Token Verification**: If a token is provided, the code tries to verify and decode it using the `jwt.verify` method. If the token is valid, the decoded payload is attached to the request object for subsequent use.

5. **Error Handling**: 
    - If no token is provided in the request, the server sends a `403 Forbidden` response with a message "Access denied. No token provided."
    - If the token verification fails (maybe because it's expired or tampered with), the server sends a `400 Bad Request` response with a message "Invalid token."

6. **Fetch User Posts**: After verifying the token, the code extracts the user's email from the decoded payload. It then uses this email to fetch the associated posts from the `userPosts` dummy data.

7. **Send Response**: 
    - If there are no posts associated with the user's email, the server sends an empty array as the response.
    - Otherwise, the server sends the fetched posts in JSON format as the response.

