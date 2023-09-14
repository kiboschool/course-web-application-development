# Static file serving

So far, we've focused on _dynamic routes_. Dynamic routes have custom logic -
the code in your route handler functions.

_Static_ routes are simpler, and super common. Send the file that was requested!

In apps that you build, static files will include images, stylesheets, 
javascript, and documents. There are also frequently HTML pages that are part 
of your website that don't require any logic, like a home page or terms and 
conditions.

For files like that, you don't need to set up a custom route. In Flask, any files 
in the `/static` directory will be served as-is.

If you have a link to a stylesheet like `<link href="/static/style.css"
rel="stylesheet">` in your HTML template, when the browser sees that link, it
will make a request for the path `/static/style.css`. Flask will look in the
`/static` directory and serve the `style.css` file if it finds it there.

## Further Reading

- [Flask docs on static files](https://flask.palletsprojects.com/en/2.2.x/quickstart/?highlight=static#static-files)
- [Flask tutorial on static files](https://flask.palletsprojects.com/en/2.2.x/tutorial/static/)

## Check your understanding

1. Add a `style.css` file to the static folder, and add a link to it from an
   HTML template. Add some CSS style rules and confirm that they are applied.
   Check in the network tab of the browser to see the request that the browser
   is making for the `style.css` file.
2. Add a favicon to the static folder and a link to it from your HTML. Reload 
   the page, and see the request in the server logs for your favicon.
3. Add another file inside a subfolder within static, like `static/images` or
   `static/files`. Enter the path to the file your browser as a URL, like
   `localhost:3000/static/files/test.pdf`, and check that the browser shows the
   file.

## Preview: Static files in Deployment

Right now, we're focused on the basics of web apps. We won't focus on deployment
until later in the course. However, it's worth noting now that static files
often get handled differently when you run your app in a production environment.

Instead of asking Flask for the static files, often there is an application layer 
between the user and Flask that knows how to handle static files. Sometimes,
this involves a Content Delivery Network (CDN). Since serving static files does
not require application logic, a server close to the client can store and serve
the files, instead of sending the request all the way to the Flask server. CDNs
are designed to be very fast at serving static files, from close to the client,
anywhere in the world.

When you learn about deployment, you'll see more about CDNs and how to handle
static files in production.
