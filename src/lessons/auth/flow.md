# Authentication flows

Before diving into each of the pieces of authentication and authorization in more detail, it's good to have an overview of the basics of the flow.

You've likely signed into applications hundreds or thousands of times, so the steps might be familiar:

- **Sign up**: Create a new account with the credentials you'll use later on
- **Sign in**: Enter the credentials, and move to a 'logged in' state
- **Logged-in Navigation**: Navigate to various pages, with your identity and authorization
- **Sign out**: move from a 'logged in' state to a 'logged out' state

There are also several other pieces of the authentication and authorization that we will mention, but not cover in depth here:

- Email verification
- Multi-factor authentication
- Forgot password and password reset
- Update email or password
- Revalidation
- Invite or approve users

## Illustration: Authentication flows 

This image illustrates the requests and responses involved in basic password authentication. 

![Illustration of the HTTP requests and responses involved in the sign up, sign in, and sign out flows](/images/sign-up-in-out-flow.png)

It can get even more complicated than this!

## Sign up

Creating an account uses the familiar two-part flow involved in creating any REST resource.

1. First, render a form with the necessary inputs
2. Then, handle the submission of the form, creating the account

There are lots of considerations when it comes to validating sign up form data, verifying email addresses, and storing passwords that we'll cover in more depth.

## Sign in

Sign in relies on the user to remember their credentials and enter them. It's a lot like the sign up form, though frequently asks for less information.

1. Render a form with the required inputs
2. Check the inputs to see if the credentials match
3. If they _do_, issue a persistent cookie or token to authenticate subsequent requests

Once again, there are lots of nuances to checking the credentials to prevent different kinds of attacks. We'll cover those in greater depth.

## Authenticated Navigation

Once the user is logged in, their device stores a cookie or token that authenticates them. 

1. Requests for other pages include the cookie or token. For cookies, this inclusion is handled automatically by the browser.
2. The server checks the cookie or token included with the request and uses that to determine who the user is
3. Based on the user, the server grants access to different resources and different abilities.

We'll cover more later about cookies and Authorization (granting different access to different users)

## Sign out

Sign out is the simplest part.

A signout route removes the stored identifier (whether that's a cookie or a token), so the user is no longer identified.

> **Further reading: Sign in forms**
>
> Sign in forms are everywhere. Some are nice to use, and some are unfriendly. These pages from web.dev explain how to design sign-in forms that are user-friendly.
>
> - [Web.Dev: Sign in form best practices](https://web.dev/sign-in-form-best-practices/)
> - [Web.Dev: Codelab - Build a sign in form](https://web.dev/codelab-sign-in-form-best-practices/)