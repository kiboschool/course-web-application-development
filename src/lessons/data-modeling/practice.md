# Practice

> 💡 This is your chance to put what you’ve learned into action.
>
> Try solving these practice challenges to check that you understand the concepts.

### Submission

You are required to submit documentation for 10 practice exercises over the
course of the term. Each one will count for 1/10 of your practice grade, or 1%
of your overall grade.

To log your practice for credit:

> **[Submit a link using this form](https://forms.gle/z8GVWpkbPAtsu4b98)**

* Practice exercises will be graded for _completion_ not _correctness_. You have
to document that you did the work, but we won't be checking if you got it right.
* You are welcome to log practice that is not one of the exercises listed on the 
practice page.
* You can submit a link to a github repo, a replit, a Google doc, or some other 
resource.

Your log will count for credit as long as it:
- is accessible to your instructor
- shows your own work

## Draw a data model

Using a drawing tool like Figma, Lucidchart, [Excalidraw](https://excalidraw.com/), or [Visual Paradigm](https://online.visual-paradigm.com/diagrams/features/erd-tool/), draw an ERD to match the following description and features:

Ubolter is a phone-based taxi application. Customers can request rides, and drivers can accept them. A ride has a destination and a pickup location, a start time and end time. Each ride has an associated _payment_, which has a base cost that depends on the time and distance, as well as surcharges for service fees and taxes. The customer may also add a tip. After each ride, customers and drivers can leave a rating and review.

- Riders
- Drivers
- Rides
- Payments
- Ratings

After you've drawn the ERD, write the CREATE TABLE statements that would create the tables in your design.

## What's wrong with this picture?

You are working on an event management system, and a fellow engineer comes to you with a data modeling problem: they can't figure out how to write their queries!

They share this data model with you:

![ERD showing events and attendees](/images/event_attendees.png)

The ERD shows an events table with id, title, start_date, and end_date. The attendees table has event_id, registration_status, name, email, and password_hash.

Your colleague is having trouble with two SQL queries:
- updating the email of an attendee
- finding all the events that one person has attended

There's a normalization problem. Write an explanation to your colleague about why this data model is wrong, what problems it can cause, and how you can fix it. Draw an updated ERD to show what your fix would look like.

As a bonus, write the UPDATE and SELECT queries to solve your colleague's problems, based on the new data model.

## JOIN practice

If you have not already, [practice JOINs on SQLBolt](https://sqlbolt.com/lesson/select_queries_with_joins). 

You can get more JOIN practice with the exercises on SQLZoo:
- [The JOIN operation](https://sqlzoo.net/wiki/The_JOIN_operation)
- [JOIN Quiz](https://sqlzoo.net/wiki/JOIN_Quiz)
- [More JOIN Operations](https://sqlzoo.net/wiki/More_JOIN_operations)

<!-- 
## Tutorial: Wikipedia search 

Step-by-step tutorial 
  - link crawler
  - search using LIKE
-->
