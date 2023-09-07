# HTML Forms

HTML forms are used to collect user input. They typically consist of a set of form elements, such as text fields, checkboxes, and submit buttons, enclosed within `<form>` tags.

When the user submits the form, it sends an HTTP request to the server with the data entered into the inputs.

## Forms Intro Video

Check out this quick overview video covering the basics of HTML forms and input elements.

<div class="embed"><iframe src="https://www.youtube.com/embed/2O8pkybH6po" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></div>

> Note the use of the `<label>` tag to label the forms.

#### Highlights
## Form elements

The `<form>` tag defines a form.

Form elements, such as text fields, checkboxes, and submit buttons, can be created using the `<input>` element, with different types:

- `<input type="text">` is a text box
- `<input type="checkbox">` is a checkbox
- `<input type="radio">` is a radio button
- `<input type="submit">` is a submit button. When clicked, it will submit the form.

The `<label>` tag is used to provide a text description for form elements.

The `<select>` and `<option>` tags are used to create a drop-down list.

The `<textarea>` tag is used to create a multi-line text input field.

The `<fieldset>` and `<legend>` tags are used to group related form elements together.

## Form tag attributes

The `<form>` tag defines the form. It goes on the outside of the input elements.

* All the inputs inside the form get included when it is submitted
* The `action` attribute specifies where the form data will be sent when the form is submitted.
* The `method` attribute specifies what HTTP method to use to submit the data. 

Forms method attribute can only be set to `"get"` or `"post"`. Other HTTP methods aren't allowed, and will send a `"GET"` request.

"get" sends the form data as part of the URL, while "post" sends the form data in the body of the HTTP request.

The action attribute specifies the route on the server to send the form data.

## Form Examples

### A login form

```html
<form action="/login" method="post">
    <label for="username">Username:</label>
    <input type="text" id="username" name="username">
    <label for="password">Password:</label>
    <input type="password" id="password" name="password">
    <input type="submit" value="Login">
</form>
```

This form contains two text fields for the username and password, and a submit button to send the form data to the server for processing. It submits a POST request to the `/login` route.

### A contact form

```html
<form action="/send_message" method="post">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name">
    <label for="email">Email:</label>
    <input type="email" id="email" name="email">
    <label for="message">Message:</label>
    <textarea id="message" name="message"></textarea>
    <input type="submit" value="Send">
</form>
```

This form contains text fields for the user's name and email address, a textarea for a message, and a submit button to send the form data. It sends a POST request to the `/send_message` endpoint on the server.

### A survey form

```html
<form action="/color_survey" method="get">
    <fieldset>
        <legend>What is your favorite color?</legend>
        <input type="radio" id="red" name="color" value="red">
        <label for="red">Red</label>
        <input type="radio" id="blue" name="color" value="blue">
        <label for="blue">Blue</label>
        <input type="radio" id="green" name="color" value="green">
        <label for="green">Green</label>
    </fieldset>
    <input type="submit" value="Submit">
</form>
```

This form contains radio buttons for different color options, and a submit button. It submits a GET request to the `/color_survey` route when the submit button is clicked.

In all above examples, the form data is sent to the server when the form is submitted. The server can use the data from the form to perform various actions such as logging in a user, sending an email, or storing data in a database.

## Further Reading: Forms and Form Elements

HTML forms are complicated! There are a ton of different kinds of elements with many options to control their behavior.

MDN has a [learning track about forms](https://developer.mozilla.org/en-US/docs/Learn/Forms)

We recommend that you read these pages to learn about forms:

- [Your first form](https://developer.mozilla.org/en-US/docs/Learn/Forms/Your_first_form)
- [How to structure a web form](https://developer.mozilla.org/en-US/docs/Learn/Forms/How_to_structure_a_web_form)
- [Basic native form controls](https://developer.mozilla.org/en-US/docs/Learn/Forms/Basic_native_form_controls)
- [HTML5 Input Types](https://developer.mozilla.org/en-US/docs/Learn/Forms/HTML5_input_types)
- [Other form controls](https://developer.mozilla.org/en-US/docs/Learn/Forms/Other_form_controls)

There is also a [reference page for the `<form>` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form).

## Check your understanding: HTML Forms

Answer these questions to check what you know about HTML forms. 

1. How do you create a text input field in an HTML form?

2. What attribute determines the HTTP method used when submitting a form?

3. How do you create a drop-down list in an HTML form?

4. How do you create a submit button in an HTML form?

5. What is the purpose of the `<label>` tag in an HTML form?

6. How do you create a multi-line text input field in an HTML form?

7. What is the role of the `action` and `method` attributes in form?

> If you write your answers in a publicly-accessible doc, you can submit the link to your work in the **[practice log form](https://forms.gle/z8GVWpkbPAtsu4b98)**.

## Practice: Create a form

Create an HTML form with input fields for a theme park survey.

Your form should include:

1. Text inputs for the user's name and email
2. Radio buttons for providing an overall rating of the park, 1-5.
3. Checkboxes for selecting their favorite attractions. 
4. A select field for entering the age range, with the ranges `"<17"`, `"18-24"`, `"25-34"`, `"35-44"`, `"45-55"`, `"55+"`
5. Labels for each of the form fields.
6. Set the form to submit to the "/park-survey" route, using a "POST" request.
7. Include a Submit button that says "Submit your survey".

> If you create a public Codepen or Replit, you can submit a link to your work in the **[practice log form](https://forms.gle/z8GVWpkbPAtsu4b98)**.
