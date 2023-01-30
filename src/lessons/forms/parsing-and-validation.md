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

On the **client side**, you can use HTML elements and attributes to provide basic validation, and add JavaScript for more advanced or custom validation. This can include simple validation checks such as ensuring that a required field has been filled out, that an email address is in the correct format, or that a password meets certain requirements. Client side validation improves user experience by providing instant feedback, but it should not be the only source of validation: it can be easily bypassed.

On the **server side**, parsing and validating inputs can include more complex validation checks such as ensuring that a username is unique, that a phone number is valid, or that a date is in the correct format. Server-side validation is more secure because it cannot be easily bypassed by attackers, or by accident, if there is a bug in the client application.

In the **database**, you can use _constraints_ to specify rules that prevent invalid data. These aren't always easy to construct or as flexible as your application code, but they provide the most robust protection against invalid data in your application.

Both client-side and server-side validation should be used together, so that users have clear feedback, and your application is secure from attackers and invalid data.
