# What are web applications?

A web application is a software application that runs on the web. It is accessed through a web browser, such as Google Chrome or Firefox, and can be used to perform a wide variety of tasks, such as checking the weather, sending email, or sharing photos.

## Web apps vs. Native apps

Check out this video on what makes a web app different from a native app.

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.youtube.com/embed/qt6gSW-uYKI" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

> ### Key ideas
> - Web apps are applications that are delivered over the internet and accessed through a web browser, whereas mobile apps or native apps are downloaded and run directly on a device.
> - Web apps can be accessed from any internet-connected platform, including laptops, desktops, tablets, and smartphones.
> - Native apps are designed specifically for certain devices and operating systems, making use of device-specific resources like cameras or GPS.
>- Web apps do not need to be downloaded, while native apps must be downloaded from an app store.
## What is a web server?

This video provides an overview of what a web server is and what it does.

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.youtube.com/embed/kzyfIiVZPJA" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

> For a deeper dive into what a web server does, see this video:

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.youtube.com/embed/9J1nJOivdyw" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

> ### Key Ideas
>- A web server is a piece of software that serves web content, and it can run on any hardware with a network connection, including laptops, smartphones, and Raspberry Pis.
>- Web servers operate by listening on a port for incoming requests, which are sent via a transport protocol, and then return a response containing the requested resource.
>- Once a web server starts up, it remains idle, waiting for incoming requests, much like a customer service representative waiting for incoming calls.
>- The operating system on which a web server runs provides a range of network ports for communication, and a web server listens on one or more of these ports for incoming requests.
>- Web servers and web clients, such as web browsers, communicate via the Hypertext Transfer Protocol (HTTP), which is a simple, text-based protocol.
>- An HTTP request consists of three blocks: a start line, headers, and an optional body. The start line specifies the type of request, the headers provide metadata, and the body contains data to be processed.
>- The response from a web server follows the same structure as an HTTP request, but the start line is referred to as the status line, which contains the HTTP version and a status code indicating the outcome of the request.
>- Web servers can serve static or dynamic content. Static content is pre-existing files, such as images or HTML pages, while dynamic content is generated on-the-fly based on the specific request, often involving database queries.
>- A single computer can host multiple web servers listening on different ports, and each web server can serve different content or be programmed in different languages.
>- The process of serving dynamic content typically involves routing incoming requests to a single entry point, such as a specific file or executable, which acts as the entry point for the web application. The application then processes the request and generates a response based on the data stored in a database or other sources.

## Check your understanding

1. What is a web application and how does it differ from a native app?
2. How are web apps accessed, and what platforms can they be accessed from?
3. Why are native apps limited to specific devices and operating systems?
4. Can web apps make use of device-specific resources? Why or why not?
5. What is the key difference in how web apps and native apps are installed and run on a device?
6. What is the primary function of a web server?
7. How does a web server respond to incoming requests?
8. What is the Hypertext Transfer Protocol (HTTP), and why is it important in the context of web applications?
9. What are the three blocks that make up an HTTP request?
10. How does a web server distinguish between requests for static and dynamic content?