# Web Application Architecture

Web applications typically follow a *client-server architecture*. 

The client is the web browser that the user interacts with, and the server is 
the remote computer that hosts the web application. The server serves content 
and functionality to the client.

On the web, the client and server communicate with each other using the HTTP 
protocol, which defines how requests and responses are formatted and handled.

But! Things aren't quite so simple.

The term _architecture_ refers to both the _components_ of an application, like 
a server and database, as well as how the _code_ is organized for a server.

The most common components of a web application architecture are the client, 
server, and database.

Within the server, application code often has a layered architecture, with a data 
layer that manages access to the application's data and databases, a 
presentation layer that handles the user interface and user experience, and a 
business layer that implements the application's core functionality. A common 
pattern for this separation in the server code is called **MVC**: Model, View, 
Controller.

## What is web app architecture?

> This video explains the basics of web app architecture, and some of the
> different kinds of architecture that different applications might use.

<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.youtube.com/embed/sDlCSIDwpDs?start=152" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

### Conceptual components vs. Physical components

Drawings of web app architecture often show boxes for many different computers. 
The client, the server (or several servers), and the database each appear as a
separate machine.

But, when we're building web apps, we usually just have one computer where we
write code. How do we deal with this?

Instead of having multiple _physical_ computers, we have multiple _conceptual_ 
computers.

In this class, you'll run the server, database, and client all on your laptop. 
Each component will communicate with the others as if they were separate -- but 
they'll just be on your computer.

> ### How does one computer act like multiple computers?
> **Ports**. Each component of your local application will use a different 
> _port_ on your computer. For instance, the server might use port 8000, the 
> database might use port 5432, and the browser might use port 50025.
> 
> When you have multiple tabs open in your browser, it may use multiple ports to
> communicate with different websites. Read more on [this post on superuser](https://superuser.com/questions/1055281/do-web-browsers-use-different-outgoing-ports-for-different-tabs).

## Local Development

Running multiple components on your computer is called _local_ development. As
the architectures you design get more complicated, you'll learn how to configure
your local _environment_ so that you can run the components you need.

When you deploy web applications, you'll run the server and database on 
different computers, and make your application available at a public URL so that 
client web browsers on laptops and phones can communicate with the server.

## Check your understanding

Try answering these questions. You may need to search online for the answers.

1. What port is typically used for local development with Flask? What about
   Express? Postgres?
2. Why might developers split an application into multiple pieces?
3. Imagine an application that's been split into multiple services that each run
   on separate machines. How do you think they would communicate with each
   other?
