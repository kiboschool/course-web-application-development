# Cookies and Sessions

HTTP is a 'stateless' protocol. The requests don't know anything about state on either side of the protocol. Requests and Responses aren't for storing data, they are for transmitting data.

But... state is so useful! It's really helpful for the browser to remember things for you, and for the server to remember things for you. When you click between pages, it's nice for the server to remember who you are and what you've done -- like the items that you've got in your ecommerce shopping cart, or (since it's the topic this week) which user you are signed in as.

That information about a user is typically stored in a **session**. There are several different ways of building sessions.

[This video](https://www.youtube.com/watch?v=UBUNrFtufWo&ab_channel=Fireship) will help differenciate Cookie vs Token auth flows.

## Cookies

**Cookies** are one of the tools for building sessions. They let the server store a little bit of data in the browser, which the browser will send back on subsequent requests.

Cookies are stored _per domain_. That means your application will only ever see cookies that it set, and other applications will never see the cookies your application sets.

Cookies are added using the `Set-Cookie` HTTP header in the response from the server. On subsequent requests, the browser will include the data in the `Cookie` header.

Here's an example of a cookie flow.

Request:
```http
POST /cart

item_id=fancy_scarf_498
```

Response:
```http
HTTP/1.1 200 OK
Set-Cookie: cart=fancy_scarf_498

{ "message": "added Fancy Scarf to your cart" }
```

Request:
```http
GET /view_cart
Cookie: cart=fancy_scarf_498
```

The first HTTP response set the cookie. Then the browser included Cookie on subsequent requests.

> **Further Reading: Cookies**
> 
> [Read more about Cookies on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)

## Sessions

Sessions contain information about the user's browsing session. There are a few ways to design sessions:

- include the session information in the cookie itself
- store the session information in your database, then store a session id in the cookie

For authentication, it's typical to store information about the user in the session. For several reasons (especially cookie size limitations and server-side session expiration), it's often a good idea to store the session information in a database instead of in the cookie itself.

Typically, that means:
- creating a table called `sessions`
- saving data in the sessions table when the user signs in
- looking up data from the sessions table based on the data in the cookie

Since this is so common, most frameworks have a way to handle it for you. You configure how the sessions should be stored, and then can access them and add or lookup data in your request handlers.

Since sessions don't have to be saved forever and are written and read more often than other data, many applications use a separate, secondary database for sessions. Key-value stores like Redis are a common choice for session databases.

## Session security

The session authenticates the user. That means that if an attacker can get the session, then they can impersonate the user! Cookies are better than other methods for implementing sessions (it's theoretically possible to use a URL parameter or something, but that could lead to several kinds of vulnerabilities).

Session cookies should be _encrypted_ so that only the server can decrypt and understand their contents.

There are also several attributes you can set on Cookies that improve their security:

- The `Secure` attribute limits cookies to HTTPS. That prevents insecure networks from leaking the cookie.
- The `HttpOnly` attribute prevents JavaScript on the page from accessing the cookie. That's good, because it means that a JavaScript bug will not give the attacker access to the cookie.
- The `SameSite` attribute means the cookie will only be included in requests from the same origin. That prevents specific kinds of cross-origin attacks.
- The `Domain` attribute restricts the domain the cookie is used on, so it will only be sent to your domain.
- The `Expire` and `Max-Age` attributes will make the cookie expire after some time.

> **Further reading**: Session Management
>
> Read more about best practices on [OWASP Cheatsheets: Session Management](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)

## Example: Sessions in Flask

By default, if you've set a secret key, Flask will store session data in an encrypted cookie. As discussed, that loses some of the advantages of server-side sessions.

Flask sessions are easy to use:

```python
# add something to the session
session['cart'] = ['fancy_scarf_489']
# read data from the session
cart_items = session['cart']
```

You can configure the Flask session to store data in a database. This is a bit tricky -- the libraries that handle it for you are small and out of date, and there is a Google name collision with the concept of a _session_ in SQLAlchemy.

Read more in the [Flask Docs on sessions](https://flask.palletsprojects.com/en/2.2.x/api/?highlight=session#sessions), or this blog, [Server-side sessions in Flask with Redis](https://testdriven.io/blog/flask-server-side-sessions/).

## Example: Sessions in Express

Express requires installing the [`express-session` package](https://expressjs.com/en/resources/middleware/session.html), which provides a configurable session implementation. It adds a `session` key to the `request` object, so you can read and modify session data like this:

```javascript
req.session.cart = ['fancy_scarf_489'];
let cartItems = req.session.cart;
```

The session id is stored in an encrypted cookie, and session data is stored on the server in a _session store_. The default session store is an in-memory store within the node app. That doesn't work great in a big production app, but there are tons of available options for the session store. 

There are lots of packages available for connecting to different backing stores, like [connect-redis](https://github.com/tj/connect-redis) to connect to Redis for a session store, [connect-sqlite3](https://www.npmjs.com/package/connect-sqlite3) to connect to SQLite3, or [@quixo3/prisma-session-store](https://www.npmjs.com/package/@quixo3/prisma-session-store) to use Prisma.

View the list of compatible session stores on the [express-session Github page](https://github.com/expressjs/session#compatible-session-stores).

## Legal history: The cookie popup

You have seen the popup on every website "This site uses cookies, approve / deny". It's the worst! 

It's a consequence of the European privacy law, the General Data Protection Regulation (GDPR). Much of the law is good, but the cookie popups are a bane.

Cookies are used for lots of helpful features, but also for tracking users across sites. The EU regulators wanted citizens to be notified and have the ability to opt out of tracking on privacy grounds -- quite reasonable! 

However, the implementation of the cookie consent box across every website has made every website worse, without accruing real privacy benefits to end users. It's very easy for sites to include the cookie banner, so they all to. Users have been trained to basically ignore the notice and find the button to dismiss the popup as quickly as possible to get to the content, rendering the protection ineffective.

If you build a website for a company, you will probably use cookies, and someone on the team will be asked to build the cookie consent box. You should do it, because the penalties for non-compliance are bad. Hold in your heart a rebellious spirit that ever yearns to remove the cookie consent box forever.
