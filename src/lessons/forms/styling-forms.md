# Styling Forms

As you've seen in these lessons, forms are complicated! That's even more true when it comes to styling. 

A big reason for the complexity is that forms are made of so many interacting pieces with specific behavior. They've also evolved over time, adding new features and more complexity.

For a history on the form specification and how browser-native forms have grown, see this [article from Smashing Magazine](https://www.smashingmagazine.com/2020/11/standardizing-select-native-html-form-controls/).

## Game: User Inyerface

Sometimes the best way to get a sense for what makes a _good_ form is to see a very bad one.

Check out [User Inyerface](https://userinyerface.com/game.html), a game. 


## Learning Path: MDN Form Styling

MDN has a series of posts about styling forms.

1. Start with the [forms guide within the CSS Building Blocks Tutorial](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Images_media_form_elements#form_elements)
2. Next, read [Styling web forms](https://developer.mozilla.org/en-US/docs/Learn/Forms/Styling_web_forms) for a comprehensive overview.
3. Next up is a [guide to styling based on the state inputs with pseudo-classes](https://developer.mozilla.org/en-US/docs/Learn/Forms/UI_pseudo-classes)
4. Last is the [Advanced Form styling guide](https://developer.mozilla.org/en-US/docs/Learn/Forms/Advanced_form_styling)

## Styling forms

Forms and inputs are still subject to the basic CSS rules you've learned: typography, colors, the box model, and layout.

Since they have lots of nested and interacting elements, it's worth practicing styling them. There are also some kinds of inputs (like the browser-native file picker) that can't be styled normally.

The principles of design for input elements are all about _clarity_ and _usability_.

You have to make it clear what the user is supposed to do with an input, and you have to make that thing easy to do.

Two important rules for achieving those goals are: **labels** and **size**.

- Inputs need to be clearly labeled.

- Inputs need to be big enough to see, click, and enter text.

## Using a library

Forms are a great case to use a CSS library for styles. Writing consistent CSS styles yourself can be very challenging!

For a long time, Bootstrap has been a popular choice for open-source styles. Check out the [Bootstrap page on styling forms](https://getbootstrap.com/docs/5.0/forms/overview/) for a sense of what using the library looks like.
