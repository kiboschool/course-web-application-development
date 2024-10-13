# Routing Basics

Servers send different responses based on the path of the request. Most web
frameworks allow developers to specify which functions should handle which
paths.

## Routing in Flask

In Flask, routes are configured using a [decorator](https://peps.python.org/pep-0318/) method on the `app` object.

```python
@app.route('/')
def index():
  return render_template('index.html')
```

The `route` function tells Flask that this function should handle requests to
that path.

It's common for a function to handle particular HTTP methods for a given
path. Instead of handling all requests to `/pets/15`, a function might only
respond to GET requests. Flask has two ways to achieve this.

Using the `route` function with the `methods` parameter:
```python
@app.route('/pets', methods=['GET'])
def show_pets():
  return render_template('pets.html')
```

Or, using a dedicated named method like `app.get` or `app.post`:
```python
@app.get('/pets'):
def show_pets():
  return render_template('pets.html')
```

Both do the same thing.

See the [Flask docs on Routing](https://flask.palletsprojects.com/en/2.2.x/quickstart/#routing) for more.

### Check your understanding

Write the decorator for the following routes:

- GET requests to the path `'/home'`
- POST requests to the path `'/add_friend'`
- DELETE requests to the path `'/enemies'`
- PUT _and_ PATCH requests to the path `'/profile'`

### Further reading: Python decorators

Check out the [Python docs on
decorators](https://docs.python.org/3/reference/compound_stmts.html#function).
It might help to search for other explanations on Google, or check out this
[explanation on YouTube](https://www.youtube.com/watch?v=r7Dtus7N4pI)

Do you think you understand decorators? Try explaining them in writing or in a
recording of your own. You could also try writing a decorator.

<!--
## Bonus: Routing in Express

-->

