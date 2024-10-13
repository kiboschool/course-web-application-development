# Express templates
As we covered with Flask, Web applications often require dynamic content rendering, where the same template can be used to display different data based on user actions (visit a page, click something, etc). This is where templating engines come into play.

For this lesson we will cover templates with EJS (Embedded JavaScript), but there are other template enginees like Pug or Handlebars.

#### Setting Up Templating

1. **Installation**:

   In your app folder, install the templating engine via npm:

   ```bash
   npm install ejs
   ```

2. **Configure Express to Use EJS**:

   In your main Express app file:

   ```javascript
   const express = require('express');
   const app = express();

   // Set EJS as the templating engine
   app.set('view engine', 'ejs');

   // Your routes and logic
   ```

3. **Creating Templates**:

   By default, Express expects templates to be in a directory named `views`. Create an EJS template named `index.ejs` in the `views` directory:

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Welcome</title>
   </head>
   <body>
       <h1>Welcome, <%= name %>!</h1>
   </body>
   </html>
   ```

   Here, `<%= name %>` is a placeholder that will be replaced by the actual value of `name` when the template is rendered.

4. **Rendering the Template**:

   In your Express routes:

   ```javascript
   app.get('/', (req, res) => {
       const userName = "John";
       res.render('index', { name: userName });
   });
   ```

   The `res.render()` function is used to render the EJS template. The first parameter is the name of the template file (without the `.ejs` extension), and the second parameter is an object containing the data to be passed to the template.