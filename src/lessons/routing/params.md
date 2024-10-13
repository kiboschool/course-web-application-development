# Route params

Routes aren't always an exact match. Sometimes, the same handler function should
respond to any route that fits a _pattern_. 

For instance, on dev.to, all articles display in a similar page layout, but the
urls are different:
[https://dev.to/sm0ke/flask-a-list-of-useful-how-to-s-42m7](https://dev.to/sm0ke/flask-a-list-of-useful-how-to-s-42m7) and [https://dev.to/lucianopereira86/python-flask-part-2-http-methods-15hm](https://dev.to/lucianopereira86/python-flask-part-2-http-methods-15hm) are both handled in the same way, but they have different urls.

**Route params** are a way to set up a handler function that can handle all the
paths that match a given pattern. That way, you don't need to add a new handler
function for each article on the site!

## Wildcards

A 'wildcard' is a way to allow a route to accept paths that match a pattern. In
Flask, you mark variable sections with `<angle_brackets>`.

```python
@app.get('/<author>/<title>')
def show_article(author, title):
  # ...
```

The matching part of the path will be passed to the function. For the path 
`/sm0ke/flask-a-list-of-useful-how-to-s-42m7`, the `author` would be `sm0ke`
and the `title` would be `flask-a-list-of-useful-how-to-s-42m7`.

### Converting path variables

Often, you'll want a route to allow particular types of values, but not others.

For instance, you might allow int ids, but not string ids: `/pets/7` is okay, but
`/pets/bumblebee` should not match.

As you can see in the [Flask variable rules docs](https://flask.palletsprojects.com/en/2.2.x/quickstart/#variable-rules),
you can specify the _type_ of a path variable. Flask will check and convert the
variable before it calls your route handler function.

```python
@app.get('/pets/<int:id>')
def show_pet(id):
  # ... id will be an int
```

>Video: Routing Demonstration

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe width="716" height="403" src="https://www.youtube.com/embed/hvd-_DvjpN0" title="WD-JAN-23-Routing demonstration" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></div>



## Query Parameters

As you saw in [last week's lessons](/lessons/web-apps/urls.md), URLs can have parameters. As a reminder: they show up towards the end of a URL, after a `?`, and come in key/value pairs, like

```
https://www.youtube.com/watch?v=yNjn_c_ovIY`
```

The parameters part of the URL is `?v=yNjn_c_ovIY`. The one parameter in this
string has the key `v` and the value `jyNjn_c_ovIY`.

In Flask, you can't match a route based the URL parameters, but you can access
the values in your function.

```python
@app.get('/watch')
def show_video():
  video_id = request.args.get('v')
```

The user may or may not pass in the query parameter you want. You need to
handle this situation! 

One way is to specify a default value as the second argument to
`request.args.get`:

```python
default_video_id = '1234abcd'
request.args.get('v', default_video_id)
```

Depending on the behavior you want, you might use a default, or you might use a
conditional statement to handle the situation differently when the parameter is
missing, such as showing a warning message.

### Note: additional imports from flask

In order to have the `request` available in your function, you need to include
it in your import from Flask, like this:

```
from flask import Flask, request
```

There are several other imports from the `flask` library that you'll end up
using as you learn more features of the framework. In a larger Flask app, you
might have many imports from `flask`.

## Check your understanding

1. Write a route handler with a decorator that matches all of these paths: 
   `/tags/programming`, `/tags/sports`, and `tags/life-lessons`.
2. Write a function that uses the url parameter `name` to greet someone (a
   'Hello, world' in Flask). Remember to include a fallback if no parameter is
   passed in!
3. Write a route handler and decorator that multiply two numbers in the path. It
   should check that the variables are ints and convert them, using Flask's
   variable rules syntax.
4. Write a decorator for an alternative version of the YouTube video route that
   uses a wildcard instead of a URL parameter.

## Tip: Flask CLI

When you install flask, it comes with a command line tool (`flask`) that you can
use for common tasks. You use it to start the development server (`flask run`). 

It has another helpful built-in tool that shows all the routes that are
configured for your application:

```sh
$ flask routes
Endpoint          Methods  Rule
----------------  -------  -----------------------
pets              GET      /pets
index             GET      /
delete_pet        POST     /pets/delete/<id>
```
