# What are web applications?

A web application is a software application that runs on the web. It is accessed through a web browser, such as Google Chrome or Firefox, and can be used to perform a wide variety of tasks, such as checking the weather, sending email, or sharing photos.

Web applications work by sending and receiving data over the internet using the Hypertext Transfer Protocol (HTTP). When a user visits a web application in their web browser, their browser sends an HTTP request to the web application's server, asking for the data or content that the user wants to access. The server then processes the request and sends an HTTP response back to the user's browser, which contains the requested data or content.

HTTP is a protocol, or set of rules, that defines how web applications communicate over the internet. It specifies how requests and responses are formatted, and what actions should be taken in response to different types of requests. For example, an HTTP request might include a verb, such as GET or POST, that specifies what type of action the server should take, as well as a path that specifies which resource on the server the request is for. The HTTP response would then include a status code, such as 200 (OK) or 404 (Not Found), that indicates the result of the request.

Overall, the process of sending and receiving HTTP requests and responses is what allows web applications to provide users with dynamic, up-to-date content and functionality.

## HTTP

_HTTP_, or the Hypertext Transfer Protocol, is a protocol that defines how web applications communicate over the internet. It is the foundation of the modern web, and is used every time you visit a website or use a web-based application.

HTTP is a client-server protocol, which means that it is based on a request-response model. When you visit a website in your web browser, your browser (the client) sends an HTTP request to the server that hosts the website, asking for the content or data that you want to access. The server then processes the request and sends an HTTP response back to your browser, which contains the requested data or content.

HTTP uses a simple, text-based format for requests and responses. An HTTP request typically includes a verb, such as GET or POST, that specifies the type of action the server should take, as well as a path that specifies which resource on the server the request is for. For example, a GET request to the path "/index.html" would tell the server to retrieve the web page at that location and send it back to the client.

An HTTP response includes a status code, which indicates the result of the request. For example, a status code of 200 (OK) indicates that the request was successful and that the response contains the requested data. A status code of 404 (Not Found) indicates that the requested resource could not be found on the server.

In addition to the request and response, HTTP also includes other elements, such as headers and cookies, that provide additional information and control how the request and response are handled.

Overall, HTTP is a simple yet powerful protocol that enables web applications to send and receive data over the internet, allowing for the creation of dynamic and interactive websites and web-based applications.

## HTTP Request Format

HTTP requests use a simple, text-based format that consists of a request line, headers, and an optional message body. Here are some examples of what HTTP requests might look like:

```
GET /index.html HTTP/1.1
Host: www.example.com
Accept: text/html
```

This is a simple GET request that asks the server to retrieve the web page at the path "/index.html" on the host "www.example.com". The request includes the HTTP version (1.1), the host header, and the accept header, which indicates the type of content that the client is expecting in the response.

```
POST /users HTTP/1.1
Host: api.example.com
Content-Type: application/json

{"username": "johndoe", "password": "mypassword"}
````

This is a POST request that asks the server to create a new user with the specified username and password. The request includes the HTTP version (1.1), the host header, and the content-type header, which indicates the format of the data in the request body. The request body itself is a JSON object that contains the username and password for the new user.

```
PUT /users/123 HTTP/1.1
Host: api.example.com
Content-Type: application/json

{"username": "johndoe", "email": "john@doe.com"}
```

This is a PUT request that asks the server to update the user with the ID "123" with the specified username and email. The request includes the HTTP version (1.1), the host header, and the content-type header, as well as the updated user data in the request body.

Overall, the exact format of an HTTP request will vary depending on the type of request, the data being sent, and the specific implementation of the web application. But in general, HTTP requests follow a simple, standardized format that allows clients and servers to communicate effectively.

## Check your understanding

1. What is a web application, and how is it different from a regular application?
2. What is HTTP, and why is it important for web applications?
3. What is a status code in an HTTP response, and why is it important?
4. Can you explain the difference between a GET and a POST request in HTTP?
5. Search the web to find:
  - a list of all the HTTP verbs, other than GET, POST, and PUT
  - a list of HTTP status codes, and what they mean

> ## Further reading: Who Sets the Standards?
>
> The HTTP protocol is standardized by the Internet Engineering Task Force (IETF), which is an international organization that develops and promotes voluntary internet standards. The IETF's HTTP Working Group is responsible for defining and maintaining the HTTP specification, which outlines how HTTP should work and what features it should include.
>
> The HTTP Working Group is made up of experts in web technologies, networking, and internet protocols. They collaborate to develop and refine the HTTP specification through a process of discussion, review, and testing. The HTTP specification is published as a series of Request for Comments (RFCs), which are publicly available documents that describe the technical details of HTTP and how it should be implemented.
>
> Overall, the IETF and the HTTP Working Group play a crucial role in maintaining and evolving the HTTP protocol, ensuring that it continues to meet the needs of the web and the users who depend on it.

