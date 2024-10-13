# Practice: Data Modeling

> 💡 This is your chance to put what you’ve learned into action.
>
> Try solving these practice challenges to check that you understand the concepts.


### Submission
To log your practice for credit:

> **[Submit on Gradescope](/assignments/week_5_practice_-_data_modeling.pdf)**

* Practice exercises will be graded for _completion_ not _correctness_. You have
to document that you did the work, but we won't be checking if you got it right.
* You are encouraged to engage with all the exercises listed on the 
practice page.
* You are expected to submit only the details requested on the Gradescope submission.


## JOIN practice

If you have not already, [practice JOINs on SQLBolt](https://sqlbolt.com/lesson/select_queries_with_joins).

You can get more JOIN practice with the exercises on SQLZoo:

- [The JOIN operation](https://sqlzoo.net/wiki/The_JOIN_operation)
- [JOIN Quiz](https://sqlzoo.net/wiki/JOIN_Quiz)
- [More JOIN Operations](https://sqlzoo.net/wiki/More_JOIN_operations)

> SQLBolt also has lessons on other kinds of queries, like aggregations. If you have time, it's good to get more SQL practice.

## Many to many relationships: Restaurants 

Practice working with many-to-many relationships by reading, running, and writing queries in the restaurant, tags, and reviews domain.

1. Fork the [Restaurant Reviews replit](https://replit.com/@kibocurriculum/Restaurant-Reviews)
2. Read the files there, and run the queries
3. Practice writing queries, following the instructions in the comments

## Draw a data model

Using a drawing tool like Figma, Lucidchart, [Excalidraw](https://excalidraw.com/), or [Visual Paradigm](https://online.visual-paradigm.com/diagrams/features/erd-tool/), draw an ERD to match the following description and features:

Ubolter is a phone-based taxi application. Customers can request rides, and drivers can accept them. A ride has a destination and a pickup location, a start time and end time. Each ride has an associated _payment_, which has a base cost that depends on the time and distance, as well as surcharges for service fees and taxes. The customer may also add a tip. After each ride, customers and drivers can leave a rating and review.

- Riders
- Drivers
- Rides
- Payments
- Ratings

After you've drawn the ERD, write the CREATE TABLE statements that would create the tables in your design.



<!-- ## What's wrong with this picture? (optional)

COMMENTED OUT SINCE IT IS A NORMALIZATION PROBLEM, WHICH WASN'T COVERED.

You are working on an event management system, and a fellow engineer comes to you with a data modeling problem: they can't figure out how to write their queries!

They share this data model with you:

![ERD showing events and attendees](/images/event_attendees.png)

The ERD shows an events table with id, title, start_date, and end_date. The attendees table has event_id, registration_status, name, email, and password_hash.

Your colleague is having trouble with two SQL queries:

- updating the email of an attendee
- finding all the events that one person has attended

There's a normalization problem. Write an explanation to your colleague about why this data model is wrong, what problems it can cause, and how you can fix it. Draw an updated ERD to show what your fix would look like.

As a bonus, write the UPDATE and SELECT queries to solve your colleague's problems, based on the new data model. -->