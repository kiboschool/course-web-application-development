# API Basics

An Application Programming Interface (API), is a set of rules that defines how two software programs should interact with each other. It allows one program to request data or services from another program and receive a response.

## APIs on the web

When web developers say 'API', they typically mean a way of requesting data and performing actions over HTTP. Often, the JSON format is used as a standard way for programs to communicate.

Web APIs often follow a convention called REST - Representational State Transfer.

In a REST API, requests are made to a specific endpoint. The endpoint URL represents a specific resource or collection of resources, and the HTTP method (such as GET, POST, PUT, or DELETE) determines the type of action being performed on that resource.

Note: there are other popular data formats for APIs, like GraphQL, gRPC, or XML. We're going to stick to JSON for this class, but many of the ideas are similar, no matter what format an API uses.

## Communicating with an API

In your career in software, you'll write code interacting with tons of different APIs. Let's review the basics.

Developers interact with an API by making requests to the API's endpoints and receiving responses.

### Making requests in Python

In Python, the `requests` library is commonly used to make HTTP requests to an API.

Here is an example of a simple GET request to retrieve data from an API endpoint:

```python
import requests

response = requests.get("https://api.example.com/users")

if response.status_code == 200:
    data = response.json()
    print(data)
else:
    print("There was a problem fetching the data")
```

The `requests` library simplifies making HTTP requests and working with the responses.

### Making requests in JavaScript

JavaScript has a built-in method called `fetch` to make and handle HTTP requests.

Here is the same example as above, in JS:

```js
fetch("https://api.example.com/users")
  .then(response => {
    return response.json();
  })
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error("There was a problem fetching the data")
  });
```

### Handling response data

API requests and responses often use JSON as the data format. In both Python and JS, you can parse the response body from a JSON string into native objects:

`response.json()`

In the JS version, there's a little dance to actually access the data (the `.json` method actually returns a Promise, which is slightly trickier to work with).

## APIs for other kinds of services

There are APIs for all kinds of things.

- get the weather
- send an email
- process a payment or bank transfer
- add an event to someone's calendar
- start a server
- send physical mail
- drive a car

Many APIs will use HTTP, but not all.

You will follow the same kind of process to use any of them:
- read the documentation
- figure out how to do the basics (such as make an authenticated request)
- figure out how to do what you want
- brainstorm and design around edge cases

Working with APIs, like lots of web development, takes practice!

## Summary

- APIs are ways for programs to communicate with each other
- In web development, that often means REST APIs, sending JSON over HTTP
- You can make requests 

In the next few lessons, you'll see how to build your own API, learn more about REST and API design. You'll also see more about how to use external services from your application, practice reading documenation, and authenticate to an API.

## Practice: Making requests

[The Cat API](https://developers.thecatapi.com/) offers endpoints for fetching cats.

- Practice using the Python requests library to fetch images. Make a request to https://api.thecatapi.com/v1/images/search?limit=10 and print out the results.
- Practice using JS fetch to fetch the same images (you can run JS using node on the command line, or in the browser console). Make a request to the same endpoint, and log out the results.

