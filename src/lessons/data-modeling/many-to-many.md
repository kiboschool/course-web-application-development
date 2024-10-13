# Many to many relationships

You've seen the use of foreign keys to represent the relationships between tables. Up until this point, the relationships have been between two tables: one with a primary key, and the other that uses a foreign key to indicate which item in the other table it is associated with. For example, an orders table keeps track of the customer_id of each order.

What about many-to-many relationships? 

## Think about it: Model these situations

How would you model these scenarios? Think about what tables you'd need, and what foreign keys would go on those tables.

- Actors can appear in many films. Films can have many actors.
- Posts can have many tags. Tags can be applied to many posts.
- Users can follow (and be followed by) many other users.

<details><summary>Where would you put the foreign keys on these tables?</summary>

If you only have two tables, there's no good answer. 

Take the `posts` and `tags` example. 

- If the foreign key goes on the posts table (`posts.tag_id`), then each post can only have one tag. 
- If the foreign key goes on the tags table (`tags.post_id`), then each tag can only apply to one post. 

There are some bad answers possible here, like adding more than one column (`posts.tag1_id`, `posts.tag2_id`), or storing more than one id in a column (`posts.tag_ids` with a comma-separated list of ids). However, these violate the principles of normalization.

Instead, we'll need to introduce a _third table_ in between `posts` and `tags` to represent the association between them.

</details>

## Associative entities

Many to many relationships in SQL databases are surprising because they **require an additional table** in order to establish the relationship between two entities. This table contains foreign keys to _both_ of the related entities, and is used to represent the many to many relationship.

This third table is called an association table (there are lots of other names for it, like "junction table" and "join table").

Let's see how it would work for the examples above.

- To connect `actors` and `films`, you could have an `appearances` table. Each `appearance` would have an `actor_id` and `film_id`, to capture the fact that the actor appeared in that film.
- To connect `posts` and `tags`, you might have a `post_tags` table, with `post_id` and `tag_id` columns. Each row in the `post_tags` table would connect one tag to one post. 
- To connect users to the users that they follow, you might introduce a `following` table, with a `follower_id` and `follows_id`, which both point back to the `users` table!


## Terminology: belongs-to, has-many, and has-many-through

When discussing relationships between entities, it's common to use the terms "belongs to" and "has many" for this kind of relationship. An order _belongs to_ a customer. A customer _has many_ orders. An order also _belongs to_ a product, and a product _has many_ orders.

For many to many relationships, it can be helpful to describe the with the phrase "has-many-through". A post has many tags _through_ the `post_tags` table. A film has many actors _through_ appearances.

## JOIN for many-to-many relationships

To write the JOIN query for a many-to-many relationship, you need to join the main entity tables with the association table. Here's an example, using the tables `students`, `courses`, and `enrollments`:

To fetch all the courses enrolled by a student with id = 1, you would write the following JOIN:

```sql
SELECT courses.* 
FROM courses 
JOIN enrollments ON courses.id = enrollments.course_id 
JOIN students ON enrollments.student_id = students.id 
WHERE students.id = 10;
```

In this statement, we first join the "courses" table with the "enrollments" table on the course_id column. Then we join the "enrollments" table with the "students" table on the student_id column. Finally, we filter the results to only show the courses enrolled by the student with `id = 10`.

When we're writing JOIN queries, it's important to include the name of the table in the `WHERE` clause. Since more than one table has a column called `id`, SQL needs the name of the table to determine which `id` is meant.

## Practice: querying many-to-many

Practice reading and writing queries for multiple tables using a restaurant dataset on Replit.

[Open Restaurant Reviews on Replit](https://replit.com/@kibocurriculum/Restaurant-Reviews)

Fork the repl to begin.

1. Start by reading schema.sql to get a sense for the tables
2. Read and run main.sql to see a little bit about what the data is like, and to see some example queries.
3. Try writing some queries! Follow the instructions at the bottom of main.sql for some queries to try.



<!-- ## Try it: Draw an ERD for a many to many relationship

Consider a situation where you have two entities, students and courses. A student can enroll in multiple courses, and a course can have multiple students.

Draw the ERD representing this schema. Include a table called "enrollments" with foreign keys to both the "students" and "courses" tables. -->
