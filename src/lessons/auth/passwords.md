# Passwords

Passwords are one of the most common ways of authenticating users. Since only the user knows their password, if someone presents the password, they must be the user.

Since passwords are so common, there are lots of ways that attackers have come up with to break them. We'll briefly cover a few of the most common attacks, and the rules and recommendations for implementing passwords to prevent attackers from succeeding.

> **This page has a lot of material and external references**. You don't need to learn all of it now -- you can bookmark this and return to it.

## Summary of password attacks

There are lots of ways to attack passwords. Attackers might want to impersonate users and gain unauthorized access, or they might want to steal data and sell credentials online. Either way, there are a standard set of attacks and standard defenses to put in place to prevent those attacks from succeeding.

Attacks:

- Brute force
- Credential stuffing and password spraying
- Offline cracking and rainbow tables
- Timing attacks
- Phishing

### Brute force

Brute force attacks are when the attacker tries lots of passwords. If the passwords are short or among the top list of passwords, an attacker can find a working set of credentials and impersonate a user.

Brute force attacks like this are prevented a few ways:

- **Rate limiting** login attempts, so attackers cannot try thousands of passwords
- **Password rules** to require long and complex passwords that aren't among the most commonly used passwords, so that attackers have a harder time guessing working passwords

> Read more:
> - [OWASP: Brute force attack](https://owasp.org/www-community/attacks/Brute_force_attack)

### Offline cracking and rainbow tables

If an attacker downloaded your whole database, then they could try to get access to the original passwords.

While you should prevent an attacker from downloading your database, _defense in depth_ means designing your system so that even if they gained access to the database, they still could not get access to the passwords.

The basic strategy for preventing attackers from reading the passwords from the database is to apply a one-way hash function and **store the hashed value**, instead of storing the plaintext password.

Hashing alone will not prevent all offline attacks. If users use common passwords or reuse passwords across sites, the attacker can recognize the hashes. An attacker can also build something called a _rainbow table_, which reduces the time it takes to break hashed passwords.

- **Hashing** passwords is the core way to prevent attackers from getting the plaintext values of users' credentials
- **Salting** the hashes makes rainbow table attacks less effective

### Timing attacks

If the attacker can tell how close they are to a correct answer, they can use that knowledge to break your security. A _timing attack_ is when the difference in time between responses tells the attacker critical information about the security of the system.

For example, if you compare strings character by character, and respond with a failure on the first character that fails, the attacker can use that information to tell when they have the first character right, because it takes a little bit more time to respond.

- Use a **constant time comparison** when you are checking if secure values are equal (Python and JavaScript `==` comparison does a character-by-character comparison under the hood, so it isn't a secure way to compare passwords!)

### Credential stuffing and password spraying

Credential stuffing takes advantage of people who use the same password across multiple sites. If one site leaks the passwords, attackers will try those credentials across lots of other sites.

Password Spraying is attempting the same common or default passwords for many usernames.

- **Multi-factor Authentication** is the best prevention
- **Rate limiting** login attempts helps to prevent both of these attacks
- **Default passwords** should be avoided, and if absolutely needed, should be required to be changed when users first log in

> Read more: 
> - [OWASP: Credential stuffing](https://owasp.org/www-community/attacks/Credential_stuffing)
> - [OWASP: Password Spraying](https://owasp.org/www-community/attacks/Password_Spraying_Attack)
> - [OWASP Cheatsheet: Credential Stuffing Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Credential_Stuffing_Prevention_Cheat_Sheet.html)

### Phishing

Phishing is when attackers send fake messages to try to steal someone's credentials. Often, attacker swill impersonate a service, then ask the victim for their login details. Since they think that the service is legitimate, they share their details with the attacker, who can then impersonate them.

Users have an obligation to avoid phishing scams, but there are some ways to make them harder:

- Use HTTPS and a recognizable, valid domain.
- Always use the same domain for the service. If users usually sign into `google.com`, but you sometimes use `serviceaccount-google.net`, they will either think the second domain is fake, or learn to trust alternate domains.
- Use Multi-factor authentication. It's not perfect, because the attacker can also show a multi-factor-auth field, but it makes an attack harder

> Read more:
> - [Phishing.org: What is Phishing?](https://www.phishing.org/what-is-phishing)
> - Follow recommendations to prevent related attacks: 
>   - [XSS](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
>   - [CSRF](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html)
>   - [Tabnabbing](https://owasp.org/www-community/attacks/Reverse_Tabnabbing)

## Rate limiting

Rate limiting prevents an attacker from making thousands of requests per minute, which can prevent or slow down many kinds of attacks.

To implement rate limiting, applications need to track how many times different devices make requests. Then, based on the kind of application and what 'normal' requests look like, it can set rules and thresholds that prevent additional requests after the limit has been exceeded.

> **Questions**
> - Why would a JSON-based API service have a different rate limit threshold than an HTML-based website?
> - What thresholds would you set for how many requests a user can make per minute to the `POST /signin` route?


> **Further Reading**
> One way around IP-based rate limits is to use a network of bots, sending requests from different devices in different locations
> Read more: [Cloudflare: What is a DDOS attack?](https://www.cloudflare.com/learning/ddos/what-is-a-ddos-attack/)

## Password Rules and validation

In the Mathematical Thinking course, you compared the sizes of the sets of different passwords and calculated how long different password schemes would take to break, if an attacker could try all of them.

As you saw, setting good password rules can dramatically increase the difficulty for an attacker to guess someone's password. As the same time, password rules can be frustrating as a user!

The [NIST password guidelines](https://www.itsasap.com/blog/nist-password-guidelines) give a list of rules to follow for validating passwords:

- Ensure passwords are at least 8 characters long
- Allow longer passwords, at least 64 characters
- Forbid commonly reused passwords by checking user's passwords against a dictionary of commonly used passwords
- Provide clear feedback about why a password isn't valid
- Enable copy/paste (don't disable it!)
- Don't use other character limitations, like requiring numbers or symbols
- Don't allow password hints
- Don't require password rotation
- Don't use security questions

There are lots of other rules and guidelines, like this one:

> Store passwords in offline-attack-resistant forms.

## Storing passwords

Tons of data breaches have resulted in users' passwords being released to the world. That isn't necessary! Even if the database is hacked, users' passwords still should not be accessible to attackers.

Instead of storing the password in plain text in the database, applications should store a hash of the password instead. When checking the password in the sign-in step, applications hash the entered password, and compare with the hashed password in the database.

To increase the resistance to offline attacks, the stored hashes should also include a _salt_ – a set of random bytes added onto the password.

> **Read more: storing passwords**
>
> - [OWASP: Password storage cheat sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)
> - [Google Cloud: Authentication and Password Management Best Practices](https://cloud.google.com/blog/products/identity-security/account-authentication-and-password-management-best-practices)

## Example: Express JS Password Auth with Passport

PassportJS is a JS auth library that provides different _strategies_ for verifying a user. The `LocalStrategy` is the one it uses for password auth.

> **Follow along**: Read through Passport's [guide to password authentication](https://www.passportjs.org/concepts/authentication/password/).
>
> You can follow along with code in the examples to build your own password auth in Express.

_Note: Passport's docs use PBKDF2 as the hashing function for storing passwords. That function works fine, but it's now recommended that you use Scrypt instead. See [this dev.to article on Scrypt](https://dev.to/farnabaz/hash-your-passwords-with-scrypt-using-nodejs-crypto-module-316k) for an explanation and code snippets._
