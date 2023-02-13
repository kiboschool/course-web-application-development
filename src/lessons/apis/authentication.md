# API Authentication

API authentication is the process of verifying the identity of the user or the client making API requests. The goal of API authentication is to ensure that the API is only used by authorized users and to prevent unauthorized access to sensitive data. If a particular user is misusing the API, identifying the user and intervening is easy if every request has to be authenticated.

There are several common methods of API authentication, including:

- API Key: An API key is a string of characters that is passed in with each API request as a parameter. The API key is used by the API to identify the client making the request and to determine if the client is authorized to access the requested data.
- OAuth: OAuth is an open standard for authorization that provides a secure way for API clients to access resources on behalf of a user. OAuth allows API clients to obtain an access token, which can be used to make API requests on behalf of the user.
- Basic Authentication: Basic authentication is a simple authentication method that involves sending a username and password with each API request. The API server then verifies the credentials and grants access to the requested data if the credentials are valid.
- Token-based Authentication: Token-based authentication involves the client sending a token with each API request. The API server verifies the token and grants access to the requested data if the token is valid. Tokens can be generated and stored on the server or sent to the client as part of an authentication process.

For most APIs where you are requesting data, you'll use an API key. If you want to act on behalf of a user, or implement sign-on with another service, you'll need to learn about Oauth.

## What it means for you

When you use external APIs, you'll often need to sign up for a developer key. Some services give you a key instantly, others have a wait.

When you make requests to the API, you'll need to include your key in the request. The documentation for the API should explain how to authenticate your requests (it's often the first thing in the docs).
