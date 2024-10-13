# Shared templates
### What are Shared Templates?

Shared templates are foundational templates that *encapsulate a common structure or layout for a website*. They typically include elements like headers, footers, navigation bars, or any other component that remains consistent across multiple pages. 

By using shared templates, developers can avoid the redundancy of rewriting the same HTML structures in every single template. Instead, shared templates can be extended, allowing for a consistent look and feel across pages, while minimizing code repetition.

### Normal Templates vs Shared Templates

Before diving into shared templates, let's recall what a normal template in Flask looks like:

```html
<!-- normal_template.html -->
<h1>Hello, {{ name }}!</h1>
```

This simple template is designed to display a greeting, with `{{ name }}` being a placeholder replaced by actual data during runtime. 

On the other hand, a shared template provides a foundational structure that can be reused across multiple templates:

```html
<!-- shared_template.html -->
<html>
<head>
    <title>{% block title %}Default Title{% endblock %}</title>
</head>
<body>
    <nav>
        <!-- Navigation links -->
    </nav>
    <div id="content">{% block content %}{% endblock %}</div>
    <footer>
        <!-- Footer content -->
    </footer>
</body>
</html>
```

In this shared template, `{% block title %}` and `{% block content %}` are defined areas that can be overridden or extended by other templates.

### Using Shared Templates with Normal Templates

Here's how you can use a shared template in conjunction with a normal template in Flask:

```html
<!-- normal_template.html -->
{% extends "shared_template.html" %}

{% block title %}
    Greeting Page
{% endblock %}

{% block content %}
    <h1>Hello, {{ name }}!</h1>
{% endblock %}
```

The `extends` keyword indicates that this template is derived from the `shared_template.html`. The defined `block` sections in the shared template can be overridden in the normal template, allowing customization while preserving the overarching layout.

### Why Do We Need Shared Templates?

1. **Consistency**: Shared templates ensure that all pages on the web application have a uniform appearance. This creates a cohesive user experience.

2. **Efficiency**: By centralizing the common elements of web pages into one shared template, changes can be made in one location rather than updating multiple individual templates.

3. **Maintainability**: It simplifies the process of updating and maintaining the web application. When you need to modify a common element, you do it in one place rather than searching through multiple files.

4. **Modularity**: Shared templates promote modular design. Developers can focus on designing individual page content without getting bogged down by the overall layout.