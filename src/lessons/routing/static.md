# Static file serving

So far, we've only worked with Python files, files that dictates the business logic of our app. This files are served backend only and never sent to the final user (in the front end). But there are files that will be sent to the user. Static files (CSS, JS, images, etc)

### Serving Static Files in Flask

In a Flask application, static files are usually placed in a directory named `static`. Flask is smart enough to recognize this convention, making it easier to serve these files.

Here's a simple directory structure:

```
/myapp
    /static
        /css
            style.css
        /js
            script.js
        /images
            logo.png
    /templates
        index.html
    app.py
```

#### CSS Implementation in Flask:

To link a CSS file in your Flask template, you would use the `url_for` function:

```html
<!-- templates/index.html -->
<link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">
```

Here, `url_for` generates the URL for the `style.css` inside the `static/css` directory.

#### JS Implementation in Flask:

Similarly, to link a JavaScript file:

```html
<!-- templates/index.html -->
<script src="{{ url_for('static', filename='js/script.js') }}"></script>
```

#### Displaying Images in Flask:

To display an image:

```html
<!-- templates/index.html -->
<img src="{{ url_for('static', filename='images/logo.png') }}" alt="App Logo">
```