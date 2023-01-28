# Server side validation

Client side validation is great for user experience, but it cannot prevent malformed data from reaching your application. 

For one, you could have a bug in your client-side validation, allowing the user to submit invalid data.

Perhaps more concerningly, you can't control the client! An attacker is allowed to send _any HTTP_ to your application, including requests that don't pass the client-side validation, no matter how good.

You _must_ validate data on the server.

First, we'll look at manually validating data. Since validating data is so common, we'll also look at using a libary to handle common validation tasks.

## Manually validating data

The basic idea of validation is to check the form data against a series of validation rules.

For example, check that a required field is not empty, that a field's length is within a certain range, or that a field's value is within a set of allowed values.

If the form data is not valid, the handler should return an error message to the user and render the form again.

If the form data is valid, it can go ahead and insert or update the data in the database, or use the data however it was intended.

Here's an example of validating a form that has a "name" and "age" fields, where "name" is a required field and "age" should be between 18 and 99:

```python
from flask import Flask, request, render_template
app = Flask(__name__)

@app.get("/form")
def show_form():
  return render_template("form.html")

@app.post("/form")
def handle_submit():
  # Get the form data
  name = request.form["name"]
  age = request.form["age"]

  # Validate the form data
  errors = {}
  if not name:
      errors["name"] = "Name is a required field"
  if age:
      age = int(age)
      if age < 18 or age > 99:
          errors["age"] = "Age should be between 18 and 99"
  if errors:
      # Return the form with errors
      return render_template("form.html", errors=errors)

  # Insert the data into the database
  #..

  # Redirect the user to a confirmation page
  return redirect("/success")
```

In this example, we are using `request.form` to access the form data, checking if the name is not empty, and checking if the age is between 18 and 99. 

If there's an error, we store it in a dictionary, and then pass the dictionary to the template to show the errors to the user. 

If the form data is valid, the app redirects the user to a success page.

## Server-side validation using libraries

Converting values to the correct types and checking their formatting often go hand in hand. For almost every backend framework, there are a number of parsing and validation libraries that you can use. Sometimes, these are built into the framework itself. Other times (especially with lightweight frameworks like Flask) they are separate packages to install and use.

There are a _lot_ of [data validation libraries in Python](https://github.com/mahmoudimus/awesome-validation-python). We'll focus on showing examples with just one library, and suggest some others to read more about.

[webargs](https://webargs.readthedocs.io/en/latest/) is a library that provides powerful validation without having to learn _too much_ new syntax.

Webargs is designed to validate HTTP Requests. Under the hood, it uses a validation library called Marshmallow for the actual data parsing and validation.

Here is a simple example using webargs to perform the same validation as the manual example above:

```python
from flask import Flask, redirect
from webargs import fields
from webargs.flaskparser import use_args

app = Flask(__name__)

@app.post("/form")
@use_args({
    "name": fields.Str(required=True),
    "age": fields.Int(validate=[validate.Range(min=18, max=99))
  }, location="form")
def handle_submit(args):
    return redirect("/success")
```

This will validate that the name field is present `(required=True)` as form data (`location="form"`).

It will also validate that the age field is between 18 and 99.

Using a library means learning how the library works, but it results in code that is more concise and easier to reason about, once you understand what the library does.

### More about webargs

- Here is a [larger example from webargs repository](https://github.com/marshmallow-code/webargs/blob/dev/examples/flask_example.py)
- See the [Quickstart guide](https://webargs.readthedocs.io/en/latest/quickstart.html) for more details about using the library
- See the [marshmallow.fields docs](https://marshmallow.readthedocs.io/en/latest/marshmallow.fields.html#module-marshmallow.fields) for a list of all of the different types of data that webargs can validate.

### Further reading: more validation libraries

Since data validation is common to many applications, validation libraries typically have a general validation core, and another library connects them to Flask.

Validation libraries we suggest looking at are:

- [Marshmallow](https://github.com/marshmallow-code/marshmallow) with  [Flask Marshmallow](https://flask-marshmallow.readthedocs.io/en/latest/)
- [Pydantic](https://github.com/pydantic/pydantic) with [flask-pydantic](https://github.com/bauerji/flask-pydantic)
- [WTForms](https://wtforms.readthedocs.io/en/3.0.x/) and [FlaskWTF](https://flask-wtf.readthedocs.io/en/1.0.x/)
