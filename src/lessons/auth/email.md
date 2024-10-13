# Emails

Email has become a standard way for users to sign in. In many applications, it has replaced a separate username.

Since a user can be assumed to own their email account, their email address is used not only for messages and updates, but also for core authentication steps, like password reset and security notifications.

How can we tell if an email address is valid? How does a web application send an email anyway? 

## Email Verification

As mentioned in the overview of the auth flow, verifying that a user owns an email address is a key part of the sign up process.

There is often a check in the HTML form whether the email they entered is actually a valid email address (is it present? Has it got the '@' character?). The database should also have a constraint that email addresses are unique. But, none of that will guarantee that the email address is valid, or that the user can actually receive mail there.

The only way to actually tell they own an email address is to send them an email and have them confirm that they received the email!

Unless a user can prove (usually by entering a code or clicking a link) that they can see emails delivered to a particular address, you can't trust that their email address is correct.

The email verification process typically works like this:

1. After the user registers with their email address
2. The application saves the email address and a status of 'unverified'
3. The application creates a random _email verification code_ and saves that along with the email address
4. The application sends a verification email, with a link that has the verification code
5. The user is notified on the page that they should check their inbox for the verification email
6. The user clicks the link in the email (something like `/verify?code=[the random verification code]`)
7. The verification route handles that request. It looks up the email address using the verification code and marks the email status as 'verified', and expires the verification code (usually by deleting it).

See [OWASP Email Validation](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html#email-address-validation) for more.

## Sending emails

Email uses a protocol called SMTP (Simple Mail Transfer Protocol) that predates HTTP. It's also a text protocol, and you can read [examples](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol#SMTP_transport_example) of what it looks like. Mail is sent from a server to an address on another server, where it waits to be read.

Just like servers can "speak" HTTP, they can also send and receive SMTP. It's possible to set up a server to act as a mail server, and send and receive mail there.

However, most web applications don't act as mail servers. Instead, they send mail through another mail service, often using an HTTP API. 

The historical reasons for this are in large part due to spam messages. Spam email is such a large problem that most mail servers _by default_ will treat incoming mail as spam. Email senders have to build up a reputation as trustworthy before receiving servers will trust them enough to accept their messages.

There are lots of different email sending providers. Kibo uses Sendgrid. Other popular services include Mailgun, Mailjet, MailChimp, Sendinblue, SendLayer, SMTP.com, AWS SES, Postmark, and SparkPost. There's a lot! They are all pretty similar to set up (lots of configuration involving your DNS provider) and use (send messages to their API and they will deliver them). 

Many providers have a package you can install, configure and use with your web framework.

## Example: Sendgrid in Express

Using Sendgrid to send mail from a nodejs / express app uses the `@sendgrid/mail` package.

Here's what it looks like in code:

```js
const sgMail = require('@sendgrid/mail')
sgMail.setApiKey(process.env.SENDGRID_API_KEY)

const msg = {
  to: 'test@example.com', // Change to your recipient
  from: 'test@example.com', // Change to your verified sender
  subject: 'Sending with SendGrid is Fun',
  text: 'and easy to do anywhere, even with Node.js',
  html: '<strong>and easy to do anywhere, even with Node.js</strong>',
}

sgMail
  .send(msg)
  .then((response) => {
    console.log(response[0].statusCode)
    console.log(response[0].headers)
  })
  .catch((error) => {
    console.error(error)
  })
```

View the full example [in the Sendgrid documentation](https://docs.sendgrid.com/for-developers/sending-email/quickstart-nodejs)
