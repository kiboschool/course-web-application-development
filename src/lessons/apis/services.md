# External services

You've written programs that make API requests. You've written web applications (and at least seen ones that act as APIs).

You can combine the two! You can make API requests from your web applications.

Many web applications rely on external services for features such as payment processing, mapping, and social media integration. These services are often provided through APIs that allow web applications to interact with them programmatically.

## Client-side requests

Since JavaScript runs in the browser, you can make requests to APIs from within your client-side code.

This is very common in frontend web development, especially for richly-featured web applications. Instead of requesting new HTML pages, JavaScript-based apps request data from the server, and then update what is displayed on the page.

In this course, we aren't focused on client-side JavaScript, so we won't cover this in any more detail for now.

## Server-side requests

There are some requests that it's better to make from the server. If there is a secret that the application knows, and the rest of the world should not know (like an authentication token), then making those requests from the client side would be dangerous! Remember, any code that executes on the client side means that other people will have access to the code and its data as it runs -- including any requests it makes.

For instance, if your application uses Sendgrid to send emails, it authenticates itself using a secret key. From the server, the application can send an HTTP request to Sendgrid to trigger sending an email. If you tried to send that HTTP request from the client, then random users might be able to get your Sendgrid key and send emails on your behalf!

## How to make third-party requests from your server

You can make requests from your server the same way you would from another program.

Here's a mini-example in Flask, using NewsAPI.org:

```python
@app.route('/news')
def news():
    API_KEY = 'your-api-key-here'
    URL = f'http://newsapi.org/v2/top-headlines?country=ng&apiKey={API_KEY}'
    response = requests.get(URL)
    if response.status_code == 200:
        news_data = response.json()
        return jsonify(news_data)
    else:
        return 'Error retrieving news headlines'
```

In this example, the `/news` endpoint uses the `requests` library to make a GET request to the NewsAPI.org service. The response is checked for a 200 status code, and if successful, the JSON data is returned to the client as a JSON response. If there is an error, a simple error message is returned.

Here's the same example, but using Express:

```javascript
app.get('/news', (req, res) => {
  const API_KEY = 'your-api-key-here';
  const URL = `http://newsapi.org/v2/top-headlines?country=ng&apiKey=${API_KEY}`;

  fetch(URL)
    .then(response => {
      if (response.ok) {
        return response.json();
      } else {
        res.send('Error retrieving news headlines');
      }
    })
    .then(data => {
      res.json(data);
    })
    .catch(error => {
      res.send('Error retrieving news headlines');
    });
});
```

## Using a package to do the work

Instead of making API requests manually, some services offer a "Client Library", a package that makes the API requests for you. NewsAPI.org offers client libraries for [Python](https://newsapi.org/docs/client-libraries/python) and [Node](https://newsapi.org/docs/client-libraries/node-js).

Here are the examples again, but using the client libraries:

```python
from newsapi import NewsApiClient
newsapi = NewsApiClient(api_key='API_KEY')

@app.route('/news')
def news():
  top_headlines = newsapi.get_top_headlines(country="ng")
  return top_headlines
```

The client library handles building the query and parsing the response.

```js
const NewsAPI = require('newsapi');
const newsapi = new NewsAPI('API_KEY');

app.get('/news', (req, res) => {
  newsapi.v2.topHeadlines({country: 'ng'})
    .then(data => { res.json(data); });
})
```

Not every API offers client libraries, and client libraries don't always stay up to date with all the options offered by the HTTP API... but they save a lot of work if they are available!



