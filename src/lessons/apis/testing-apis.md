# Testing APIs

API testing involves verifying that APIs function correctly, that means, that the return the correct information when visiting a particular endpoint.

There are severals ways of testing this APIs, but we are going to see the 3 more popular.

For starters, we are only going to test GET methods, in a very popular API called PokeApi. This API returns information about pokemons.

### 1. Testing API with a Browser (Chrome, Firefox, etc)

One of the simplest ways to test a GET API is by using a web browser.

Open and new tab and got to the next address:
`https://pokeapi.co/api/v2/pokemon/ditto`

You should receive a JSON response displaying the data. 

This means your browser is doing a `GET` request to the PokeApi and receiving a response.

For a better visual experience, when using Google Chrome, it's recommended to add an extension called [**JSON formater**](https://chrome.google.com/webstore/detail/json-formatter/bcjindcccaagfpapjjmafapmmgkkhgoa). This will ensure the JSON response is displayed in a readable format.

### 2. Testing API with `curl` command

`curl` is a versatile command-line tool available on most platforms that lets you send HTTP requests.

Open your terminal and type the following command:

```bash
curl https://pokeapi.co/api/v2/pokemon/ditto
```

This command will retrieve information about the Pokémon "Ditto" from the PokeAPI. Remember, this particular API does not support POST requests, so you'll be limited to GET requests.

### 3. Testing API with Postman

While browsers and `curl` offer quick ways to test APIs, the recommended method for a more comprehensive testing experience is a dedicated software called [Postman](https://www.postman.com/).

[This video](https://www.youtube.com/watch?v=wmz1sGZp814) shows some basic steps on how to use Postman