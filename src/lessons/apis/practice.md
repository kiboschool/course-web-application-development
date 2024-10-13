# Practice: APIs

> 💡 This is your chance to put what you’ve learned into action.
>
> Try solving these practice challenges to check that you understand the concepts.

### Submission
To log your practice for credit:

> **[Submit on Gradescope](/assignments/week_8_practice_-_apis.pdf)**

* Practice exercises will be graded for _completion_ not _correctness_. You have
to document that you did the work, but we won't be checking if you got it right.
* You are encouraged to engage with all the exercises listed on the practice page.
* You are expected to submit only the details requested on the Gradescope submission.

## Fetching from an API in Node

Pick one of the following APIs, read the documentation and get data from the API using NodeJS and fetch:

- [Giphy API](https://developers.giphy.com/): An API for searching for and retrieving animated GIFs. The API documentation includes information about endpoints, request and response formats, and examples of how to use the API.
- [News API](https://newsapi.org/): An API for retrieving news articles from around the world. The API documentation includes information about endpoints, request and response formats, and examples of how to use the API.
- [OpenWeatherMap](https://openweathermap.org/api): A weather API that provides weather data for cities around the world. The API documentation includes example requests and responses, as well as information about the data format and available endpoints.

## Writing Documentation: Sample Node App (optional)

This [Sample app on Replit](https://replit.com/@kibocurriculum/Documentation-Practice#README.md) is missing documentation.

Based on what's in `index.js`, write documentation for the methods. Include the path and HTTP verb, any expected parameters, what values to expect in return, as well as a general description of the path.

- Remember to consider the [purpose](https://c4s.vercel.app/communicating-for-success/planning-structuring/know-your-purpose.html) and [audience](https://c4s.vercel.app/communicating-for-success/planning-structuring/analyse-your-audience.html) of the documentation you write.
- You are encouraged to share your documentation with other students for feedback.

## Serving an API: Flask (optional)

Open up your previous Flask number guessing game project. Instead of using HTML templates, write an updated version as an API that communicates using JSON. It won't be easy to play using the browser. Instead, you can write a program that uses the `requests` package to play the guessing game by JSON API instead.
