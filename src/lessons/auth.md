# Auth

Many applications require you to sign into your account in order to use the
services. Users of the application should see their own data, not someone
else's. Similarly, users might have different _roles_ within an application. An
admin might be able to see different pages and take different actions than a
normal user.

In the news, you frequently hear about hacks and leaks of passwords and user
data. Despite how vulnerable companies websites seem to be, it is _possible_ to
design secure applications.

This week, you'll learn about the key patterns for _authenticating_ users
(verifying they are who they say), and _authorizing_ them to access particular
pages and actions within your application. You'll see and learn to recognize 
some of the common mistakes that developers make in building auth flows, and
learn about some schemes to create 'defense in depth' to make sure users can use 
the features as intended, and no more.

As part of managing authentication, you'll learn about using external services
to sign in, and learn more about sending emails from your application.

## Authentication and Authorization

There are two key words that both start with "Auth".

**Authentication** is about verifying who someone is.

**Authorization** is about granting access, based on who they are.

Read more about the basics of [Authentication vs. Authorization from Auth0](https://auth0.com/docs/get-started/identity-fundamentals/authentication-and-authorization).

