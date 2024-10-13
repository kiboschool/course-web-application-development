# Accessibility

Accessible websites are ones that everyone can use. They are understandable (even if you can't see, or see in color), they are navigable (using either the keyboard or mouse), and they try to make things as clear as possible for the user -- especially when they ask the user to input data.

This [guide from the Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/fundamentals/accessibility-intro/) introduces accessibility. 

## Accessible forms guidelines

Forms are a particularly important thing to design well. While many pages on a site can have design issues, no issues are as painful to users as form design issues.

Here are the core rules for designing accessible forms:

- Use the appropriate HTML elements (especially for form inputs)
- Label form inputs
- Show meaningful error messages, near the inputs
- Allow tab navigation
- Highlight the inputs on focus
- Break long forms into labeled sections
- Lay out form inputs vertically, not horizontally
- Enable copy, paste and autofill

### Use appropriate elements

It is possible, with 'clever' JavaScript, to make any element _sort of_ act like a form element.

This is bad:

```html
<div class="button">Submit</div>
```

While it is possible to make a div look button-like and do something when clicked, it's hard to give it all of the behaviors that 'real' buttons normally have, like tab-selection, focus, keyboard commands, and access via a screen reader.

Always use the appropriate element for the job: an `<input>` when you want an input, a `<button>` if you want a button, or an `<a>` when you want a link.

### Include labels for form inputs

Users don't know what to type into a form without a label.

```html
<label for="email">Email:</label>
<input id="email" type="text" name="email"></input>
```

The `for` attribute of the label connects the label, based on the `id` of the input.

> Note: Only use placeholders for additional info. A placeholder may be helpful, but it isn't a label! See [this from MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/::placeholder) or [this article from Smashing Magazine](https://www.smashingmagazine.com/2018/06/placeholder-attribute/)

### Provide helpful error messages

When the user enters invalid data, you have to tell them what went wrong!

- the error should be near the invalid input
- the error should explain what the user can do to fix the problem
- the message can use contrasting color (but should not use _only_ color) to indicate what went wrong

See these guides on error messages:
- [Providing Helpful Error Messages](https://accessibility.huit.harvard.edu/provide-helpful-error-messages)
- [WAI: Form Notifications](https://www.w3.org/WAI/tutorials/forms/notifications/)

### Focus management and tab control 

By default, it's possible to navigate through a form using the keyboard, mostly by using the Tab key to advance.

Some web developers accidentally disable this navigation through some combination of CSS and JavaScript. That takes away the default accessibility of the browser. Don't do it!

Similarly, focused elements are usually surrounded by a 'ring' to visually highlight them. If a developer disables that highlight, it's difficult for the user to tell which element is focused.

### Ordering and grouping elements

Logical ordering and grouping of related inputs makes forms easier to fill out. The `<fieldset>` and `<legend>` tags create a grouping of related elements.

See the page [WAI: Grouping Controls](https://www.w3.org/WAI/tutorials/forms/grouping/) for more about grouping elements.

Typically, it's easier to fill out forms from top to bottom, instead of having many elements arrayed horizontally.

### Enable copy, paste, and autofill

Copy, paste, and autofill help users enter information easily. They are enabled for most elements by default. Don't disable them!

If you use appropriate input types and labels, the browser can also help users to autofill details like emails, names, addresses, and credit cards.

By using the right labels, you can make your forms easier for everyone to use.

## Further Reading: Accessible Forms

There are a lot of articles and resources online explaining top accessiblity tips, especially for forms.

- [UX Design blog: 10 tips for designing accessible forms](https://uxdesign.cc/10-tips-for-designing-accessible-forms-a016dae8e9aa)
- [A11y Project: How to write accessible forms](https://www.a11yproject.com/posts/how-to-write-accessible-forms/)
- [Logrocket: A Practical Guide to Accessiblity for forms](https://blog.logrocket.com/a-practical-guide-to-accessibility-for-forms/)
- [Formspree: Accessible forms](https://formspree.io/blog/accessible-forms/)

MDN and the W3 Web Accessibility Initiative (WAI) also have tons of great resources on accessible design:

- [WAI: Accessiblity Principles](https://www.w3.org/WAI/fundamentals/accessibility-principles/)
  - [WAI: Tips for writing](https://www.w3.org/WAI/tips/writing/)
  - [WAI: Tips for designing](https://www.w3.org/WAI/tips/designing/)
  - [WAI: Tips for developing](https://www.w3.org/WAI/tips/developing/)
- [MDN: Accessibility](https://developer.mozilla.org/en-US/docs/Web/Accessibility)
