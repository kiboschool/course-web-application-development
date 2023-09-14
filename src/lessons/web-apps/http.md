# HTTP

_HTTP_, or the Hypertext Transfer Protocol, is a protocol that defines how web applications communicate over the internet. It is the foundation of the modern web, and is used every time you visit a website or use a web-based application.

> This video explains the basics of HTTP

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.youtube.com/embed/8QjYUp3w5U0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

### Further Reading: HTTP

> Check out the [MDN page on HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)
>
> See also this [HTTP breakdown from Cloudflare](https://www.cloudflare.com/learning/ddos/glossary/hypertext-transfer-protocol-http/)

## Requests and Responses

HTTP is a client-server protocol, which means that it is based on a request-response model. 

When you visit a website in your web browser, your browser (the client) sends an HTTP **request** to the server that hosts the website, asking for the content or data that you want to access. The server then processes the request and sends an HTTP **response** back to your browser, which contains the requested data or content.

> This video explains the format of HTTP Requests

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.youtube.com/embed/5X7wcZuO5mU" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

> This video fleshes out the details of HTTP Responses

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.youtube.com/embed/I4kUB17pTno" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

HTTP uses a simple, text-based format for requests and responses. An HTTP request typically includes a **verb**, such as GET or POST, that specifies the type of action the server should take, as well as a **path** that specifies which resource on the server the request is for. For example, a GET request to the path "/index.html" would tell the server to retrieve the web page at that location and send it back to the client.

An HTTP response includes a **status code**, which indicates the result of the request. For example, a status code of 200 (OK) indicates that the request was successful and that the response contains the requested data. A status code of 404 (Not Found) indicates that the requested resource could not be found on the server.

## HTTP Request Format

HTTP requests consist of a request line, headers, and an optional message body. 

Here are some examples of HTTP requests:

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

### HTTP Headers and Cookies

In addition to the request and response, HTTP also includes other elements, such as headers and cookies, that provide additional information and control how the request and response are handled.

When we discuss authorization and security, you'll learn more about some
specific HTTP headers.

### HTTPS

You may sometimes see a trailing 's' on HTTP, and the lock icon in your browser.
HTTPS is a _secure_ version of HTTP. Instead of sending the plain text of the
requests and responses, HTTPS _encrypts_ the requests and responses using a
protocol called Transport Layer Security, TLS.

The protocol is otherwise the same -- it's still HTTP underneath. When we
discuss deployment, you'll learn more about how to configure HTTPS to securely 
encrypt traffic to your server.

## Check your understanding

1. What is a status code in an HTTP response, and why is it important?
2. Can you explain the difference between a GET and a POST request in HTTP?
3. Search the web to find:
  - a list of all the HTTP verbs (including GET, POST, and PUT)
  - a list of HTTP status codes, and what they mean

If you find a good resource, you're encouraged to share it with the class in
Discord.

## Further reading: Who Sets the Standards?

> The HTTP protocol is standardized by the Internet Engineering Task Force (IETF), which is an international organization that develops and promotes voluntary internet standards. The IETF's HTTP Working Group is responsible for defining and maintaining the HTTP specification, which outlines how HTTP should work and what features it should include.
>
> The HTTP Working Group is made up of experts in web technologies, networking, and internet protocols. They collaborate to develop and refine the HTTP specification through a process of discussion, review, and testing. The HTTP specification is published as a series of Request for Comments (RFCs), which are publicly available documents that describe the technical details of HTTP and how it should be implemented.
>
> Overall, the IETF and the HTTP Working Group play a crucial role in maintaining and evolving the HTTP protocol, ensuring that it continues to meet the needs of the web and the users who depend on it.
