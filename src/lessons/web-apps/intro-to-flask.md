# Intro to flask

# Introduction to Flask within the Context of Web Applications

As we learned in the previous lesson, web applications are software applications that run on the web and are accessed through a web browser. Web applications work by sending and receiving data over the internet using the Hypertext Transfer Protocol (HTTP), which defines how requests and responses are formatted. We also learned that web servers are software that serves web content, listening on a port for incoming requests and returning a response containing the requested resource.

When it comes to building web applications, developers need a tool that simplifies the tasks associated with creating and maintaining a web server, handling HTTP requests and responses, and managing other web-related functionalities. That's where Flask comes in.

## What is Flask?

Flask is a micro web framework for **Python** that helps developers create web applications with minimal effort. It's considered a "micro" framework because it provides the essential tools to build web applications while leaving much of the application's functionality up to the developer's discretion. Despite its simplicity, Flask is powerful and flexible, enabling developers to create everything from small single-page applications to complex web services.

## Why Use Flask to create web applications?

When building a web application, developers need to handle a variety of tasks, including setting up a web server, managing HTTP requests and responses (HTML, JSON, XML, etc), routing incoming requests to the appropriate resource, serving static and dynamic content, and more. Flask makes all these tasks easier and more straightforward, providing developers with built-in features and extensions like the following:

1. **Web Server Management:** Flask comes with a built-in web server, allowing developers to quickly start serving their web applications without the need for external web server software.

2. **HTTP Requests and Responses:** Flask provides an intuitive way to handle incoming HTTP requests and send back appropriate HTTP responses. Developers can easily define URL patterns, specify the type of request (e.g., GET or POST) and responses (HTML, JSON, XML, etc)

3. **Routing and Resource Management:** Flask enables developers to define routes that map URL patterns to specific Python functions. These functions, called "view functions," handle incoming requests, process data, and generate responses, allowing developers to serve dynamic content based on the specific request.

## Appendix: Getting Started with Flask

Here, we will guide you through the process of installing Flask and creating a simple "Hello, World!" web application.

### Installing Flask

To install Flask, you'll need to have Python installed on your computer. Flask is compatible with Python versions 3.6 and newer. You can install Flask using pip, which is the package installer for Python. Open your terminal or command prompt and type the following command:

```bash
pip install Flask
```

### Creating a Simple "Hello, World!" Web Application

Open your terminal and:

1. Create a new folder and  go inside this folder:
```bash
mkdir my_app
cd my_app
```

2. **Create a new Python file:** Create a new Python file named `app.py` and open it in your preferred text editor.

3. Paste the following code:
```python
# Import the Flask class from the flask module
from flask import Flask

# Create an instance of the Flask class, which will be our web application
app = Flask(__name__)

# Define a route for the root URL ("/") and the associated view function
@app.route('/')
def hello():
    # This view function returns the text "Hello, World!" when accessed
    return "Hello, World!"

# Define a route for the URL "/json" and the associated view function
@app.route('/json')
def json():
    # This view function returns a JSON object with two key-value pairs
    # "my_message" with value "cool", and "value" with value 10
    return {"my_message": "cool", "value": 10}

# Define a route for the URL "/html" and the associated view function
@app.route('/html')
def html():
    # This view function returns an HTML string that displays a header with the text "You can also return HTML"
    return "<h1>You can also return HTML</h1>"

# This block of code is executed if the file is run as a script (not imported as a module)
if __name__ == '__main__':
    # Run the Flask web server with debugging mode turned on
    app.run(debug=True)

```

4. **Run the application:** Save the `app.py` file and go back to your terminal or command prompt. Navigate to the directory where the file is located and run the following command:

```bash
python app.py
```

You should see a message indicating that your server is running on `http://127.0.0.1:5000/`.

5. **Access the web application:** Open your web browser and visit `http://127.0.0.1:5000/`. You should see the message "Hello, World!" displayed in your browser. If you visit `/json` and `/html` routes, you will discover that the response is different.

Congratulations! You've successfully installed Flask and created your first "Hello, World!" web application. You can now continue to explore Flask's features and build more complex web applications.

### Check your understanding

1. What is Flask and why is it referred to as a "micro" web framework?
2. What language is Flask written in?
3. List some of the tasks that developers need to handle when building a web application. How does Flask make these tasks easier?
4. Explain what a view function is in Flask and how it is related to routes.
5. What are the steps to install Flask and create a simple "Hello, World!" web application using Flask?