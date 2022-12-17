# API Considerations

## Availability

## Errors

- often the solution for "what do we do if they have an error" is "show the user their error"

## Retry, rate limiting and backoff

## Data and caching

- is it cool to cache someone's API?

## APIs for other kinds of services

There are APIs for all kinds of things.

- get the weather
- send an email
- process a payment or bank transfer
- add an event to someone's calendar
- start a server
- send physical mail
- drive a car

They follow the same kind of process, as a developer:
- read the documentation
- figure out how to do the basics (usually, make an authenticated request)
- figure out how to do what you want
- brainstorm and design around edge cases
