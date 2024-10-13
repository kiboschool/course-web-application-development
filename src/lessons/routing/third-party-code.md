# Third-party code

Libraries and packages help you build common features that would be hard or
time-consuming to build on your own. In Python, you can use `pip` to install
packages and `import` to load them into your code. As it turns out, there are
lots of other ways to install and use packages.

When using third-party packages for the web, the big question is: "where does
this code run?" 

* **Server-side packages** might help you connect to a database,
render templates, or use an API. You install them using the package manager for
your server's language or framework. (For Flask, that's `pip`. For Express, it's
`npm`).

* **Client-side packages** are HTML, CSS, or JS that add some functionality to
your web page, like a set of styles, widgets, or interactive feature. The
code has to be loaded onto your webpage, so there are a few different ways
to set that up.

_Note: some packages have both a server-side and client-side component. We'll
ignore those for now, but they typically have setup guides that help install and
configure them._

This lesson will focus on client-side packages, since you've already got some
experience installing and using libraries in Python. There are several options for using client-side packages, they include:

- Using a CDN
- Serving the files yourself
- Bundling

## Loading third-party code from a CDN

The easiest way to load some third-party code into your page is by using some
other host.

As you remember from Web Development Fundamentals, you use the `<link>` tag to load CSS, and 
the `<script>` tag to load JavaScript. To load the client library Bootstrap onto
your site, you'd use

CSS:
```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
```

JS:
```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
```

(See [https://getbootstrap.com/](https://getbootstrap.com/) for more.)

Instead of hosting the code on your own server, you tell the browser to load it
from another server. In this case, [jsdelivr](https://www.jsdelivr.com/), which
offers free hosting for open-source assets like Bootstrap.

### Further Reading: What is a CDN?

A **Content Delivery Network (CDN)** is a set of servers that are configured for
serving static assets quickly, all over the world. There are lots of different
CDNs! They typically have datacenters in many locations, so that no matter where
the user is, they can get a quick response.

CDNs are great for serving static files like CSS, JavaScript, images, or
documents. There is not much configuration if you are just using a CDN to load
assets like Bootstrap, but if you want to host your own files on a CDN, there's
typically more steps.

Read more from [Cloudflare about what CDNs are and how they work](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/).

## Serving the files yourself

As you saw, you can serve static files in Flask by placing them in the `/static`
directory. There is usually a similar mechanism in any web framework.

If you download the CSS and JS files for the third-party code you want to use
(like Bootstrap), then you can host those static files from your server, instead
of relying on the CDN.

Instead of using urls that point to the CDN, you'll instead use urls that point
to your application, like:

CSS:
```html
<link href="static/bootstrap.min.css" rel="stylesheet">
```

JS:
```html
<script src="static/bootstrap.bundle.min.js"></script>
```

<!--
## Bundling


## Check your understanding: Use Bootstrap

-->
