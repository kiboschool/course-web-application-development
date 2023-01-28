# Parsing and Validation

As you've probably seen when creating CLI programs, users cannot be trusted to enter the right information into your program.

A big job for most applications is _validating user input_. That means:

- parsing data into the appropriate types (e.g. from a string into a float)
- checking that the data makes sense for the application (e.g. the name should not be blank, the password should have 8 characters)
- showing helpful information to the user, so that they can enter the information correctly

Parsing and validating form inputs is an important step in ensuring that the data submitted by the user is _accurate_ and can be _safely_ processed by the application.

## Parsing data types

Input to your application need to be converted to the appropriate data type before they can be used.

Even if an `input` element has a specific type like number or date, the form-encoded data will come into your request handler as a string.

You'll need to convert it to the correct type in order to store it in the database or use it for some other computation.

Here's a basic example parsing string data:

```python
@app.post('/submit')
def submit():
    # Get form data as strings
    name = request.form['name']
    age = request.form['age']
    salary = request.form['salary']

    # Parse age and salary
    age = int(age)
    salary = float(salary)

    # Do something with the parsed data, e.g. insert into a database
    # ...

    return 'Form data parsed and converted successfully'
```

<details><summary>What would happen if age or salary was not able to be parsed as an int or float?</summary>

Python raises a `ValueError` when it cannot convert a string into the right type.

Flask will handle the error, so instead of crashing your program, it will return a 500 error page to the client.

Instead of a 500 error, you could check the values before you convert them: _Validation_. Then, you could return a meaningful error to the client, instead of a 500. That way, the user can correct their submission.

</details>

## Client, Server, and Database Validation

In the web applications we've seen, there are three places code runs, so three places where you can validate input:

- On the client
- On the server
- In the database

On the client side, you can use HTML elements and attributes to provide basic validation, and add JavaScript for more advanced or custom validation. This can include simple validation checks such as ensuring that a required field has been filled out, that an email address is in the correct format, or that a password meets certain requirements. Client side validation improves user experience by providing instant feedback, but it should not be the only source of validation: it can be easily bypassed.

On the server side, parsing and validating inputs can include more complex validation checks such as ensuring that a username is unique, that a phone number is valid, or that a date is in the correct format. Server-side validation is more secure because it cannot be easily bypassed by attackers, or by accident, if there is a bug in the client application.

In the database, you can use _constraints_ to specify rules that prevent invalid data. These aren't always easy to construct or as flexible as your application code, but they provide the most robust protection against invalid data in your application.

Both client-side and server-side validation should be used together, so that users have clear feedback, and your application is secure from attackers and invalid data.

## Client side validation

### HTML input elements

First, it's helpful to ask the user to input the right types of data! The browser will enable basic validation (as well as autofill) if you use the right type of input.

- `<input type="email">` for email
- `<input type="search">` for search
- `<input type="phone">` for phone numbers
- `<input type="url">` for urls
- `<input type="number">` for numbers
- `<input type="range">` for a range slider
- various input types (`time`, `week`, `month`, `datetime-local`) for dates and times

The browser will only let the user enter the right type of data, and it will make it easier for the user to enter the data. Compare typing a date vs. picking from a calendar.

See the list of [HTML input types](https://developer.mozilla.org/en-US/docs/Learn/Forms/HTML5_input_types) for more.

### input element attributes

You can use specific attributes to provide further validation and feedback to the user:

- `required`: This attribute indicates that the input field must be filled out before the form can be submitted. If a user attempts to submit the form without filling out a required field, the browser will display an error message.
- `pattern`: This attribute can be used to specify a regular expression that the input's value must match. If the input's value does not match the pattern, the browser will display an error message.
- `min` and `max`: These attributes can be used to specify a minimum and maximum value for an input field. If the input's value is less than the minimum or greater than the maximum, the browser will display an error message.
- `step`: This attribute can be used to specify the increment or decrement of the input's value.
- `minlength` and `maxlength`: These attributes can be used to specify a minimum and maximum number of characters that can be entered into the input field.

You can read more about [HTML constraint validation on MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Constraint_validation)

### Validation using JavaScript

Particularly for more complicated constraints, another approach is to validate the form using JavaScript.

Client-side form validation using JavaScript involves checking the form inputs on in the browser before they are sent to the server. This can improve user experience by providing immediate feedback to the user if they have entered invalid data.

Form validation using JavaScript typically involves the following steps:

1. Attach an event listener to the form, typically to the submit event, so that the validation code runs when the user attempts to submit the form.
2. In the event listener callback function, access the form input elements and check their values.
3. If the input values are invalid, display an error message to the user and prevent the form from being submitted by calling `event.preventDefault()`.

Here's an example: 

```javascript
// Get the form element
const form = document.querySelector("form");

// Attach an event listener to the form's submit event
form.addEventListener("submit", function(event) {
    // Get the input elements
    const name = document.querySelector("input[name='name']");
    const age = document.querySelector("input[name='age']");

    // Check if the input values are valid
    if (name.value.trim() === "" || age.value.trim() === "") {
        // Display an error message
        alert("Name and Age are required fields");
        // Prevent the form from being submitted
        event.preventDefault();
    }
});
```

This example uses an `alert` to let the user know what's wrong. A better design would be to add inline warning messages that specify what is wrong with the form.

## Further Reading: MDN on form validation

[MDN's page on form validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation) explains the principles of client and server-side validation, with examples.

## Server side validation

Client side validation is great for user experience, but it cannot prevent malformed data from reaching your application. 

For one, you could have a bug in your client-side validation, allowing the user to submit invalid data.

Perhaps more concerningly, you can't control the client! An attacker is allowed to send _any HTTP_ to your application, including requests that don't pass the client-side validation, no matter how good.

You _must_ validate data on the server.

### Manually validating data

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

### Server-side validation using libraries

Converting values to the correct types and checking their formatting often go hand in hand. For almost every backend framework, there are a number of parsing and validation libraries that you can use. Sometimes, these are built into the framework itself. Other times (especially with lightweight frameworks like Flask) they are separate packages to install and use.

There are a _lot_ of [data validation libraries in Python](https://github.com/mahmoudimus/awesome-validation-python). We'll focus on showing examples with just one library, and suggest some others to read more about.

The library we recommend for validation _right now_ is [webargs](https://webargs.readthedocs.io/en/latest/).

Webargs is designed to validate HTTP Requests. Under the hood, it uses a validation library called Marshmallow for parsing and validation.

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

#### More about webargs

- Here is a [larger example from webargs repository](https://github.com/marshmallow-code/webargs/blob/dev/examples/flask_example.py)
- See the [Quickstart guide](https://webargs.readthedocs.io/en/latest/quickstart.html) for more details about using the library
- See the [marshmallow.fields docs](https://marshmallow.readthedocs.io/en/latest/marshmallow.fields.html#module-marshmallow.fields) for a list of all of the different types of data that webargs can validate.

#### Further reading: more validation libraries

Since data validation is common to many applications, validation libraries typically have a general validation core, and another library connects them to Flask.

Validation libraries we suggest looking at are:

- [Marshmallow](https://github.com/marshmallow-code/marshmallow) with  [Flask Marshmallow](https://flask-marshmallow.readthedocs.io/en/latest/)
- [Pydantic](https://github.com/pydantic/pydantic) with [flask-pydantic](https://github.com/bauerji/flask-pydantic)
- [WTForms](https://wtforms.readthedocs.io/en/3.0.x/) and [FlaskWTF](https://flask-wtf.readthedocs.io/en/1.0.x/)

## Database validation

A key software design principle is "Defense in depth". It's commonly applied to security, but it applies equally well to data validity and ensuring that there aren't bugs.

Client-side validation can by bypassed by an attacker. Even server-side validation can still have errors.

Database validation can provide another layer of constraints that ensure that your data is valid.

While the constraints provided by a database are often less flexible than ones you can write for your server, they are critical to prevent weird bugs and situations.

For instance, your application probably is not designed to have two different users with the same email address. That would probably cause all kinds of headaches! Database constraints can prevent that kind of issue.

Read the [SQLBolt Lesson on Creating Tables](https://sqlbolt.com/lesson/creating_tables) for a taste of the types of constraints you can create, and the syntax for doing so.

<details><summary>What are some of the key ways constriants can protect the validity of your data?</summary>

- Validate the type of data
- Check the uniqueness of a field across all the rows in a table
- Make sure a field is not null
- Confirm that a foreign key exists in another table (e.g. make sure that a `user` exists before creating an `order` associated with them)

You can also create custom CHECK constraints, but we won't cover those.

</details>

Next week, we'll discuss Database constraints in more detail when we cover Data Modeling.
