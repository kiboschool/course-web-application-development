# Form Data

When an HTML form is submitted, the data is sent to the server in the form of key-value pairs. For each form element, the key is the `name` attribute of the element, and the value is the user's input (the `value` attribute).

For example, let's say you have a simple form with two text fields, one for the user's name and one for their email address:

```html
<form action="/signup" method="post">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name">
    <label for="email">Email:</label>
    <input type="email" id="email" name="email">
    <input type="submit" value="Submit">
</form>
```

When the user submits the form, the data is sent to the server as key-value pairs, formatted like `"name=John"` and `"email=john@example.com"`. 

If the form's `method` is `"get"`, it is submitted with a GET request, and the data is appended to the URL as query parameters. For example, if the form action is `"/signup"` and the user input for name is "John" and email is "john@example.com", the data will be sent in the URL as:

```
/signup?name=John&email=john@example.com
```

For POST requests, the data is sent in the body of the HTTP request. The browser will form-encode the data, and include a Content-Type header `"x-www-form-urlencoded"`, which is a standard format for sending data in HTML forms. The server looks at that header and decode the data in the body.

## Data for other form elements

For form elements like radio buttons, checkboxes, and select fields, the data is also sent as key-value pairs. The key is the name attribute of the form element, and the value is the selected or entered option.

### Radio buttons

For radio buttons, the `value` attribute of the selected option is sent as the value of the key. For example, if a form has a radio button group with the name "color" and options for "red" and "blue", 

```html
<input type="radio" id="red" name="color" value="red">
<label for="red">Red</label>
<input type="radio" id="blue" name="color" value="blue">
<label for="blue">Blue</label>
```

If the user selects "blue", the data sent upon form submission would look like this:

```
color=blue
```

### Select

For select fields (usually styled as dropdown inputs), the value attribute of the selected option is sent as the value of the key. For example, if a form has a select field with the name "colors" and options for "red", "green", "blue": 

```html
<select name="color" id="color">
  <option disabled selected>Choose a color</option>
  <option value="red">Red</option>
  <option value="green">Green</option>
  <option value="blue">Blue</option>
</select>
```

and the user selects "green", the data sent upon form submission would look like this:
```
colors=green
```

### Checkboxes

For checkboxes, the value attribute of the selected option is sent as the value of the key. For example, if a form has a checkbox group with the name "fruits" and options for "apple", "banana", and "pear", and the user selects "apple" and "banana", the data sent upon form submission would look like this:

```
fruits=apple&fruits=banana
```

It's worth noting that, when multiple options are allowed in checkboxes or select fields, the data is sent as multiple key-value pairs with the same key, one for each selected option. 

In case of the select fields, it is possible to send multiple options at the same time if the select element has the attribute [`multiple`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select#attr-multiple) in the HTML form.

```html
<select name="color" id="color" multiple>
```

### Further Reading: Sending Form Data

Read [MDN's guide on submitting forms](https://developer.mozilla.org/en-US/docs/Learn/Forms/Sending_and_retrieving_form_data)

Note: we will use native form submission in this class. However, in many applications, developers submit forms using JavaScript instead of letting the browser handle the form submission. See https://developer.mozilla.org/en-US/docs/Learn/Forms/Sending_forms_through_JavaScript

## Accessing form data in Flask

In Flask, you can access the values from a submitted form in a few different ways, depending on the method used to submit the form.

For a GET request, you can access the form data as query parameters in the request object. Here is an example of a Flask route that handles a GET request with a form that has two fields, "name" and "email":

```python
from flask import Flask, request

app = Flask(__name__)

@app.get('/submit')
def handle_form_submit():
    name = request.args.get('name')
    email = request.args.get('email')
    return 'Name: {} Email: {}'.format(name, email)
```

For a POST request, you can access the form data in the request object's `form` attribute. Here is an example of a Flask route that handles a POST request with a form that has the same fields as before:

```python
from flask import Flask, request

app = Flask(__name__)

@app.post('/submit')
def handle_form_submit():
    name = request.form['name']
    email = request.form['email']
    return render_template('welcome.html', name=name, email=email)
```

## Bonus: File uploads

There are a lot of types of HTML inputs! Most behave like the ones above, with a key/value pair in the submitted data.

`<input type="file">` allows uploading a file, and it is encoded differently when submitted.

* The Content-Type header is "multipart/form-data" instead of "x-www-form-urlencoded"
* The data will be encoded differently and it will be accessible in the server side using a different method.

When a form includes a file upload field, the browser will typically submit the form using the "multipart/form-data" content type. This content type uses a different encoding method to send the form data to the server.

When the form is submitted, the browser will send the data in multiple "parts", each with its own content type and headers. Each part will contain the data for one form field, including the file data.

For example, if a form includes fields for the user's name, email address, and a file upload field, the data sent to the server might look something like this:

```text
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="name"

John Doe
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="email"

johndoe@example.com
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="file"; filename="image.jpg"
Content-Type: image/jpeg

[binary data for image file]
------WebKitFormBoundary7MA4YWxkTrZu0gW--
```

Here, the "boundary" is a string that separates the different parts of the data. Each part begins with a "Content-Disposition" header that specifies the name of the form field, and for file fields, it also contains the "filename" and "Content-Type" headers.

On the server side, the file data can be accessed by reading the raw data of the request and parsing it based on the boundary, this process is called "multipart parsing". Different languages and frameworks have their own libraries and methods to handle the multipart/form-data. 

If you'd like to handle file uploads in Flask, see the [Flask docs on file uploads](https://flask.palletsprojects.com/en/2.2.x/patterns/fileuploads/).
