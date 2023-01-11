# Templates

Python f-strings are a convenient way to set up a string _template_.

```python
f"{name} will attend {school} this October"
```

You can change the variables `name` and `school`, while leaving the rest of the
string the same.

Templates in a web server are much the same. You write the template once,
leaving slots for values to be inserted. To serve the template, you pass in the
values, and it uses them to fill in the slots.

## Flask Templates

Flask templates are stored in the `templates` directory. Files in that folder
can use a template syntax similar to f-strings to insert values into the rest of
the content.

To use a template, you use the `render_template` function. This function needs 
to be imported from Flask. The function takes in the variables to be inserted
into the template as named arguments.

Here's a minimal example:

```python
# app.py
from flask import Flask, request, render_template

@app.get('/hello')
def say_hello():
  name = request.args.get('name', 'world') # default to 'world'
  render_template('hello.html', name=name)
```

```html
<!-- templates/hello.html -->
<h1>Hello, {{name}}</h1>
```

## Jinja2 syntax

As you saw in the example, the template syntax is a little different than
f-strings. Flask uses a library called [Jinja](https://jinja.palletsprojects.com/en/3.1.x/)
for rendering templates. 

> _(From the [Jinja template docs](https://jinja.palletsprojects.com/en/3.1.x/templates/))_
>
> Below is a minimal template that illustrates a few basics using the default Jinja configuration.
> 
> ```
> <!DOCTYPE html>
> <html lang="en">
> <head>
>     <title>My Webpage</title>
> </head>
> <body>
>    <ul id="navigation">
>    {% for item in navigation %}
>        <li><a href="{{ item.href }}">{{ item.caption }}</a></li>
>    {% endfor %}
>    </ul>
>
>    <h1>My Webpage</h1>
>    {{ a_variable }}
>
>    {# a comment #}
> </body>
> </html>
>```
> 
> There are a few kinds of delimiters. The default Jinja delimiters are configured as follows:
> 
> - `{% ... %}` for Statements
> - `{{ ... }}` for Expressions to print to the template output
> - `{# ... #}` for Comments not included in the template output
>

**Statements** are things like loops and conditions. In the example, there's a loop:

```
{% for item in navigation %}
...
{% endfor %}
```

Jinja also supports conditions:

```
{% if item > 50 %}
...
{% endif %}
```

Statements look a lot like regular Python, except:

- They are surrounded by `{% %}`
- They don't have the `:`
- There's an `endfor` or `endif` to close the block.

Indentation is significant in Python, but it doesn't have the same
meaning in other kinds of files, so Jinja can't use indent/dedent to guess when
a loop or a conditional statement starts and ends.

**Expressions** are for showing values ibn the template.

```html
<li><a href="{{ item.href }}">{{ item.caption }}</a></li>
```

You can evaluate small pieces of Python code inside of double-curly braces, and
the result will show up in the output.

Expressions are often used to show the value of variables passed into your
template, like

```
Hello, {{ name }}
```

But you can run other python code too. Usually, this is to help with things like
formatting, or showing different pieces of some object, like `item.caption`.


## Check your understanding

1. Create and render a template from a flask app, passing in a random integer to
   display on the page.
2. Explore the Jinja template syntax. Create a list in your Python code, pass
   the list to the template, and render each item in the list.
3. Templates don't have to be HTML! Try rendering a custom CSS template that
   uses Jinja syntax to set a custom color from Flask.

## Further Reading: Templates

- [Flask template docs](https://flask.palletsprojects.com/en/2.2.x/quickstart/#rendering-templates)
- [Flask template tutorial](https://flask.palletsprojects.com/en/2.2.x/tutorial/templates/)
- [Jinja template syntax docs](https://jinja.palletsprojects.com/en/3.1.x/templates/)
