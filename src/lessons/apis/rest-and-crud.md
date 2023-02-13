# REST

REST, or Representational State Transfer, is a pattern for API design based on resources. It matches common names and behaviors to HTTP verbs and paths.

REST APIs are widely used in web development and have become a popular way of creating web-based services that can be consumed by a variety of clients, including web browsers, mobile apps, and other server-side systems.

## Resources

Resources are the fundamental building blocks of REST architecture. Resources are abstract representations of objects or data entities, and they are accessed and manipulated using standard HTTP methods, such as GET, POST, PUT, and DELETE.

For example, in a RESTful API that provides access to a chat, a resource might represent a message. This resource can be accessed and manipulated in standard ways: retrieving the message using a GET request, creating a new message using a POST request, updating an existing message using a PUT request, and deleting a message using a DELETE request.

Each resource in a RESTful API is identified by a unique URL, and the API defines a set of standard operations that can be performed on each resource. This provides a consistent and predictable interface for interacting with the API, making it easier for developers to understand and use the API.

## Standard names and actions for HTTP methods

Here are the standard actions associated with each HTTP method:

- `GET`: Retrieve a representation of a resource. This method is used to retrieve the current state of a resource, and it should be safe (i.e., it should not modify the state of the resource).
- `POST`: Create a new resource. This method is used to create a new resource, and it should return a representation of the new resource.
- `PUT`: Update a resource. This method is used to update an existing resource, and it should return a representation of the updated resource.
- `PATCH`: Partially update a resource. This method is used to partially update an existing resource, and it should return a representation of the updated resource.
- `DELETE`: Delete a resource. This method is used to delete an existing resource.

These standard actions are the foundation of RESTful APIs, and they provide a predictable and consistent interface for accessing and manipulating resources.

> Note: PUT and PATCH play similar roles. It's common to mix the two up, so don't be surprised if you see a full update using PATCH or a partial update using PUT. Also... there's a lot of updates that just use POST to a dedicated update route, in part because HTML forms cannot send PUT or PATCH HTTP requests.

## Standard URL patterns

Here are some common URL patterns and resource names used in RESTful APIs:

- _Collection of resources_: A collection of resources is often represented as a list, and it is accessed using a URL pattern such as `/resources`. For example, `/messages` might represent a collection of chat messages.
- _Single resource_: A single resource is accessed using a URL pattern that includes an identifier, such as `/resources/:id`. For example, `/messages/1` might represent a single message with an ID of 1.
- _Sub-resources_: Sub-resources are resources that are related to a parent resource, and they are accessed using a URL pattern that includes both the parent resource and the sub-resource. For example, `/messages/1/replies` might represent the replies for a message with an ID of 1.
- _Search_: Search for resources can be performed using a URL pattern that includes a query string, such as /resources?query=search_term. For example, `/messages?author=John` might search for all chat messages written by John.

## Create, Read, Update, and Delete

The typical actions on a resource are these 4: Create, Read, Update, and Delete (CRUD). Those are typically the actions you'd expect to be ablet to perform on a resource in a REST API.

You may be noticing a parallel between the HTTP Verbs, REST, and SQL. At each level of the application, we have parallel versions of similar CRUD actions.

- HTTP GET mirrors SQL SELECT
- HTTP POST mirrors SQL INSERT
- HTTP DELETE mirrors SQL DELETE (nice!)
- HTTP PATCH mirrors SQL UPDATE

When you start using a new API, a new database, or a new web framework, it's often a good idea to start with CRUD. If you can Create, Read, Update, and Delete the relevant resources, you are on the right track with your new tool!

## Example: Flask

Here's small but complete example of how you might implement REST API routes for a "message" resource using Flask:

```python
from flask import Flask, request, jsonify

app = Flask(__name__)

messages = [
    {
        "id": 1,
        "message": "Hello World!"
    },
    {
        "id": 2,
        "message": "Goodbye World!"
    }
]

# Get all messages
@app.route("/messages", methods=["GET"])
def get_all_messages():
    return jsonify(messages), 200

# Get a single message by id
@app.route("/messages/<int:message_id>", methods=["GET"])
def get_message(message_id):
    message = [message for message in messages if message["id"] == message_id]
    if len(message) == 0:
        return jsonify({"error": "Message not found"}), 404
    return jsonify(message[0]), 200

# Create a new message
@app.route("/messages", methods=["POST"])
def create_message():
    message = {
        "id": messages[-1]["id"] + 1,
        "message": request.json["message"]
    }
    messages.append(message)
    return jsonify(message), 201

# Update an existing message
@app.route("/messages/<int:message_id>", methods=["PUT"])
def update_message(message_id):
    message = [message for message in messages if message["id"] == message_id]
    if len(message) == 0:
        return jsonify({"error": "Message not found"}), 404
    message[0]["message"] = request.json["message"]
    return jsonify(message[0]), 200

# Delete a message
@app.route("/messages/<int:message_id>", methods=["DELETE"])
def delete_message(message_id):
    message = [message for message in messages if message["id"] == message_id]
    if len(message) == 0:
        return jsonify({"error": "Message not found"}), 404
    messages.remove(message[0])
    return jsonify({"message": "Message deleted"}), 200

if __name__ == "__main__":
    app.run(debug=True)
```

This example implements the standard CRUD (Create, Read, Update, Delete) operations for a "message" resource. The messages list represents the current state of the resource, and the API routes perform the appropriate action for each HTTP method (e.g., GET retrieves the current state of the resource, POST creates a new resource, PUT updates an existing resource, and DELETE deletes a resource).

## Example: Express

Here's an equivalent example using Express:

```javascript
const express = require('express');
const app = express();
const bodyParser = require('body-parser');

app.use(bodyParser.json());

const messages = [
  {
    id: 1,
    message: 'Hello World!'
  },
  {
    id: 2,
    message: 'Goodbye World!'
  }
];

// Get all messages
app.get('/messages', (req, res) => {
  res.status(200).json(messages);
});

// Get a single message by id
app.get('/messages/:messageId', (req, res) => {
  const message = messages.find(message => message.id === parseInt(req.params.messageId));
  if (!message) {
    return res.status(404).json({ error: 'Message not found' });
  }
  res.status(200).json(message);
});

// Create a new message
app.post('/messages', (req, res) => {
  const message = {
    id: messages[messages.length - 1].id + 1,
    message: req.body.message
  };
  messages.push(message);
  res.status(201).json(message);
});

// Update an existing message
app.put('/messages/:messageId', (req, res) => {
  const message = messages.find(message => message.id === parseInt(req.params.messageId));
  if (!message) {
    return res.status(404).json({ error: 'Message not found' });
  }
  message.message = req.body.message;
  res.status(200).json(message);
});

// Delete a message
app.delete('/messages/:messageId', (req, res) => {
  const messageIndex = messages.findIndex(message => message.id === parseInt(req.params.messageId));
  if (messageIndex === -1) {
    return res.status(404).json({ error: 'Message not found' });
  }
  messages.splice(messageIndex, 1);
  res.status(200).json({ message: 'Message deleted' });
});

const port = process.env.PORT || 3000;
app.listen(port, () => {
  console.log(`Listening on port ${port}`);
});
```

This example uses the express library and the body-parser middleware to handle HTTP requests and responses. The REST API routes are defined using the `app.get()`, `app.post()`, `app.put()`, and `app.delete()` methods, and the response is constructed using the `res.status()` and `res.json()` methods.

As with the Flask example, this implementation uses an in-memory array to represent the "message" resource, and implements the standard CRUD operations for the resource.
