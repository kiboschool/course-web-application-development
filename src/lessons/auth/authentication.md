# Authentication

Authentication is **how a user proves they are who they say they are**.

Apps can use different combinations of factors to authenticate who a user is. That could mean:

* Credentials: tokens, usernames, email accounts, or passwords
* Device identifiers: cookies, long-lived application sessions, phone numbers, or multi-factor auth
* Third-party services and SSO: using protocols like Oauth for 'Sign in with Github' (or other providers)

We'll cover the basics of how to build some of these flows in applications, and discuss how to decide which authentication experience is appropriate for the kind of application you are building.

We will also discuss experiences that work without sign-in: phone and email-based services and guest checkout.

> **Authentication is a complex topic**.
>
> We won't cover everything in this class, and there's a ton more to do to build secure systems. Thankfully, organizations like [OWASP](https://owasp.org/) make cheatsheets like the [Authentication Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html) that can help you if you are building an authentication system.

## Authentication Factors

It's common to talk categorize the different kinds of factors that applications can use to verify someone's identity:

- Something you **know**
- Something you **have**
- Something you **are**

_Passwords_, _pin codes_, and _security questions_ are something **only the user knows** (at least in theory). If only the user knows the password, then if the password is entered, then the person who entered it must be the user!

_A device_ or a _token_ are examples of something **only the user has**. If you show the user a message in their authenticator app, or send them an SMS confirmation code, and they confirm the code, then they have the device, so the application has more confidence that they are who they say they are.

Biometric identifiers, like FaceID or fingerprint log in represent something that **only the user is**. Biometric identifiers aren't something we'll build in this class, but they are a great option for identification if you are building applications for iOS or Android, since those platforms provide developers with biometric identification tools.

### Further Reading: What is authentication?

Read more about authentication from Cloudflare and Auth0:

> - [Cloudflare: What is authentication?](https://www.cloudflare.com/learning/access-management/what-is-authentication/)
> - [Auth0: What is authentication](https://auth0.com/intro-to-iam/what-is-authentication)

## Credentials

### Usernames, Emails, and Passwords

The most familiar way of authenticating a user is the username (or email) and password.

Users enter their information into a form, submit it, and the application checks whether their information matches what they entered on sign up.

This is a feature you could build now, using the tools you already know -- it's just a form and some fields in a database... or is it?

> **Warning**: it is very easy to design password authentication _wrong_, in a way that leads to subtle security bugs! We'll cover these in more detail in the next lessons.

Because users will inevitably forget their passwords, it's also very common to consider the _password reset flow_ as a critical part of building a secure authentication system. Because this is so key, you'll learn a bit about sending email from applications this week.

### Tokens

As you saw with APIs, one common way of authenticating a request is to include a token as part of the HTTP request.

```js
fetch("https://api.example.com/?token=ABCD1234EFGH")
```

When someone signs up for a developer account, the API stores their information and generates a unique token. When the token is included with the request, the app can look up the user.

This is a very common pattern, and it is often used in conjunction with other strategies here.

There are some variants to know, such as:
- including the token in the body of the request, instead of the url params
- including the token in an HTTP Header instead of in the url params or the body
- generating fresh tokens based on other credentials, and expiring old tokens after a time limit

There are some important distinctions between these different token strategies, but we're going to skip over the nuances for right now.

## Device Identifiers and Multi-factor auth

When you sign into a site or an app, you don't need to sign in again each time you reload the page. Cookies, sessions, and device tokens are ways to identify particular devices as belonging to a particular user. If the request includes this identifier, then it must come from this device, and therefore be the same user who is making the request.

These features are really important, but require learning a bit more about cookies and sessions.

Multi-factor authentication is a way to confirm that a user is who they say they are by prompting them to confirm their sign-in using a second device. This is a powerful way to secure applications, but building it so that it is still convenient can be challenging! We won't cover building MFA flows in this course, but we will link to external resources so you can read more if you are interested.

## Third-party authentication and Single sign-on

Because people are so bad at remembering passwords, many sites build a "Log in with X" feature (log in with Google, log in with Github, log in with Facebook, or many others). That way, users can identify themselves without having to create a new account and enter their email and password.

There are several different protocols for applications to build these integrated flows, the most popular and common being OAuth2. Implementing OAuth is a many-step dance of links, requests, and callbacks between the user, the application, and the OAuth provider (Google, Facebook, Github, etc.). It's increasingly common to use a provider like Stytch or Auth0 to build this feature for you, instead of building these flows by hand.

Single Sign-on is a common enterprise feature, where users sign into their corporate account, and then are automatically authenticated into the other applications that they use. It's common for enterprises to use services like Octa or OneLogin to provide this feature, but applications need to integrate with the SSO providers in order to make the system work. The typical protocols you'll see related to SSO are SAML and OpenID Connect.

We also won't cover OAuth or Single sign-on in depth in this course, but we will link to resources in case you want to learn more.

> [Cloudflare: What is SSO?](https://www.cloudflare.com/learning/access-management/what-is-sso/)

## Passwordless experiences

Signing into a website in order to view a resource, purchase a product, or complete some action is _annoying to users_ and _difficult to build effectively_. When possible, it's great to **not build authentication at all**. This could mean:

- building a guest checkout or shopping cart with a session cookie, but no sign in
- building a whatsapp, sms, or email-based experience, where the user never needs to sign in or create an account
- designing 'magic link' style sign-in experiences, where the user gets a link sent to their email address or phone, and clicks that to be signed into their account

We won't cover building passwordless flows or magic links, and will only briefly touch on building with anonymous session cookies. When designing applications, you keep your eye out for ways to avoid authenticating users when possible.
