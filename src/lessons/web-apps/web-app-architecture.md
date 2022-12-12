# Web Application Architecture

Web applications typically follow a client-server architecture. 

The client is the web browser that the user interacts with, and the server is the remote computer that hosts the web application. The server serves content and functionality to the client.

On the web, the client and server communicate with each other using the HTTP protocol, which defines how requests and responses are formatted and handled.

But! Things aren't quite so simple.

Within the server, applications often have a layered architecture, with a presentation layer that handles the user interface and user experience, a business layer that implements the application's core functionality, and a data layer that manages access to the application's data and databases.

## Server Architecture


## MVC

The Model-View-Controller (MVC) architecture is a common design pattern for web applications. It is based on the idea of separating an application into three distinct parts, each with its own responsibilities and role in the overall application. These three parts are the model, the view, and the controller.

The **model** manages the application's data and business logic. It is responsible for managing the application's data, performing calculations and processing, and communicating with any external data sources or services.

The **view** handles the user interface and presentation of the application. It is responsible for rendering the application's content and layout, and providing users with a way to interact with the application.

The **controller** acts as the intermediary between the model and the view. It receives user input, passes it to the model for processing, and then sends the resulting data to the view for rendering.

Overall, the MVC architecture is designed to promote _separation of concerns_ in web applications. By dividing an application into these three distinct parts, developers can work on different parts of the application in parallel, and make changes to one part without affecting the other parts. This can make the development and maintenance of web applications more efficient and flexible.

## Platforms and Hosting

Web applications can be deployed on a variety of platforms and hosting environments, such as traditional web servers, cloud-based platforms, or even specialized "serverless" architectures.
