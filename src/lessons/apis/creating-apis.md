# Creating APIs

An API is not so different from the other web applications you've been working with.

* Instead of returning HTML templates, they return JSON
* They pay even more attention to the names and HTTP verbs of the routes
* They publish documentation describing how the API works

All the rest of what you've learned still applies. APIs still use HTTP, routes, templates, and databases.

## Rendering JSON from Flask

Flask will automatically convert strings, ints, lists, and dicts into JSON.

```python
@app.get("/users/<id>")
def show_user(id):
  user = db.get_user(id)
  return { "name": user.name, "id": user.id }
```

If you have another datatype (not a dict, list, string, or int), then you may have some work to do to turn it into JSON. You can either make a dict with the values that you want, or you can write code that will _serialize_ your data into JSON.

There are some libraries that will do this for you. For the small apps in this class, you can usually write the dictionary or list version of your response more easily than configure a library to do the work.

## Rendering JSON from express

In Express, you can render a JSON response using `res.json`.

```javascript
app.get("/user/:id", (req, res) => {
  const user = db.get_user(req.params.id)
  res.json(user);
});
```

## Boom! It's an API

Well... routing requests and rendering JSON is the easy part.

The hard part is designing an API that other developers want to use. That means:

- making an API that does something that is valuable to them
- designing the API so they can understand it
- writing documentation (and sharing the API) so that they can learn how to use it

## Practice: Rendering JSON

Create a small Flask app with no database. Return a string, int, list, and dict from different routes. Run the app and check your routes in the browser to confirm that they show up as JSON.

Rebuild the same app using Express for practice. Check that your routes render JSON in the browser.

## Other considerations

There are some API-specific features that don't show up as often in HTML web applications, or are treated differently.

- **Errors**: in an HTML site, you want to steer users away from errors as much as possible. In an API, errors are almost inevitable, so it's more important to give clear error messages that can help the developer know what they got wrong in their request.
- **Rate limiting**: If users use your site too much, it might go down. To prevent that, you might rate-limit users so that they can only view 1000 pages per minute, or some other limit. APIs may be expected to support much higher rate limits, since Python can make requests much faster than a user can click!
- **Caching**: Browsers will sometimes cache images or other static resources, so they don't have to fetch them again when reloading a page. When designing an API, you will likely have a different caching strategy than when you design an HTML page.
- **Availability**: APIs and web pages have different expectations for performance and availability. It's bad if a user can't access a webpage. If no one can use PayPal's API, then that's many thousands of webpages that end up broken!
- **Authentication**: Many websites have concepts of Users who can log in, and only access certain resources. APIs frequently have more complicated notions of users. For instance, you can sign in with a provider, who can then modify resources on your behalf.

We haven't discussed auth yet, but it is a frequent concern in APIs. This week you'll see how to authenticate to an API, and next week you'll learn a bit about building authentication in your apps.
