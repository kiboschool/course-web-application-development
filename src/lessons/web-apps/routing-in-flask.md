# Routing in Flask

Flask, makes it easy for developers to define routes, handle various request types, and serve different response formats. This article provides a comprehensive guide to setting up routes with different request types (GET, POST) and different response types (JSON, HTML).

## Setting Routes
In Flask, routes are defined using the `@app.route()` decorator, which maps a URL pattern to a Python function. This function, known as a view function, handles incoming requests, processes data, and generates responses.

Here's a simple example:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Welcome to my web app!"
```

> In this example, the route `"/"` is mapped to the `home()` view function. When a user accesses the root URL of the application, the `home()` function is called and returns the text "Welcome to my web app!".

## Handling Different Request Types

HTTP defines several request methods (GET, POST, DELETE, etc). Flask allows developers to specify which request methods a route should handle by using the `methods` parameter of the `@app.route()` decorator. Check out the following example

```python
from flask import request

@app.route('/submit', methods=['POST'])
def submit():
    name = request.form['name']
    return f"Hello, {name}!"
```

> In this example, the route `"/submit"` handles POST requests. The view function retrieves the `name` field from the submitted form data and returns a personalized greeting.

## Serving Different Response Types

Flask allows developers to serve various response types, including JSON and HTML. The `jsonify` function and the `render_template` function make it easy to serve JSON and HTML responses, respectively.

### JSON Responses

To serve a JSON response, you can use the `jsonify` function from the Flask module. This function converts a Python dictionary into a JSON-formatted response.

Here's an example:

```python
from flask import jsonify

@app.route('/api/data', methods=['GET'])
def api_data():
    data = {'name': 'John', 'age': 30}
    return jsonify(data)
```

> In this example, the route `POST "/api/data"` serves a JSON response containing the specified data.

### HTML Responses

To serve an HTML response, you can just render the HTML as text. Flask will be smart enough to recognize it and show a HTML response

Here's an example:

```python
from flask import render_template

@app.route('/about', methods=['GET'])
def about():
    return "<h1>Hello</h1>"
```

> In this example, the route `GET "/about"` serves an HTML response.
