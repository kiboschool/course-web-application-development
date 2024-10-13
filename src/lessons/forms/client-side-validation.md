# Client side validation

## HTML input elements

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

## Input element attributes

You can use specific attributes to provide further validation and feedback to the user:

- `required`: This attribute indicates that the input field must be filled out before the form can be submitted. If a user attempts to submit the form without filling out a required field, the browser will display an error message.
- `pattern`: This attribute can be used to specify a regular expression that the input's value must match. If the input's value does not match the pattern, the browser will display an error message.
- `min` and `max`: These attributes can be used to specify a minimum and maximum value for an input field. If the input's value is less than the minimum or greater than the maximum, the browser will display an error message.
- `step`: This attribute can be used to specify the increment or decrement of the input's value.
- `minlength` and `maxlength`: These attributes can be used to specify a minimum and maximum number of characters that can be entered into the input field.

You can read more about [HTML constraint validation on MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Constraint_validation)

## Validation using JavaScript

Particularly for more complicated constraints, another approach is to validate the form using JavaScript.

Client-side form validation using JavaScript involves checking the form inputs in the browser before they are sent to the server. This can improve user experience by providing immediate feedback to the user if they have entered invalid data.

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

## Further Reading: Client-side validation

[MDN's page on form validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation) explains the principles of client-side validation, with examples.
