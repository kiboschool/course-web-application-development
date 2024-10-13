# Query VS URL params

Params allows you to capture user input in your application.

![Parts of a url](/images/mdn-url-parts.png)
*Query params are represented in blue, URL params are represented in yellow*

## What are URL Parameters?

URL parameters, also known as path parameters or path variables, are values embedded in the URL path of a request. They are typically used to capture values that define a specific resource. For example, in the URL `https://example.com/users/123`, `123` is a URL parameter that probably represents a user ID.

## What are Query Parameters?

Query parameters, on the other hand, are usually used to provide non-hierarchical data that doesn't fit into the path structure. They appear after the `?` symbol in a URL and are separated by the `&` symbol.

For example, in the URL `https://example.com/search?query=python&sort=asc`, there are two query parameters:
1. `query` with the value `python`
2. `sort` with the value `asc`

## Using URL Parameters and Query Parameters in Flask

### URL Parameters

In Flask, you can define URL parameters in your route by using angle brackets `< >`.

Here's an example that shows how to use a URL parameter to display a user profile:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/users/<username>')
def user_profile(username):
    return f"Welcome to the profile page of {username}."
```

When a user accesses the URL `https://example.com/users/john`, the view function `user_profile()` is called with `john` as the argument for the `username` parameter, and it returns the string "Welcome to the profile page of john."

### Query Parameters

In Flask, you can access query parameters using the `request` object. The `request` object is imported from the `flask` module and contains all the data sent by the client during the HTTP request.

Here's an example that demonstrates how to use query parameters in Flask:

```python
from flask import Flask, request
app = Flask(__name__)

@app.route('/search')
def search():
    query = request.args.get('query')
    sort_order = request.args.get('sort')
    return f"Searching for: {query}, sorted in {sort_order} order."
```

When a user accesses the URL `https://example.com/search?query=python&sort=asc`, the view function `search()` is called, and it returns the string "Searching for: python, sorted in asc order."

## Why Use URL Parameters and Query Parameters?

1. **URL Parameters**: They are often used to identify a specific resource or a set of resources. They are part of the URL path and are suitable for data that is hierarchical in nature.

2. **Query Parameters**: They are useful for sending additional data that is not part of the resource identifier. They are often used for filtering, sorting, and pagination.

### Check your understanding
1. What is the main purpose of using params in a web application?
2. What are URL parameters, and where are they located in a URL?
3. How do URL parameters differ from query parameters in terms of their position within a URL?
4. Can you give an example of a URL with a URL parameter and explain what it represents?
5. What are query parameters, and how are they represented in a URL?
6. Can you give an example of a URL with query parameters and explain what they represent?
7. In Flask, how can you define URL parameters in your route?
8. Using the provided Flask example for URL parameters, what would the output be if a user accesses the URL `https://example.com/users/john`?
9. How can you access query parameters in Flask? What is the `request` object used for?
10. Using the provided Flask example for query parameters, what would the output be if a user accesses the URL `https://example.com/search?query=python&sort=asc`?
11. What are the typical use cases for URL parameters and query parameters?