# N+1 queries

You've seen how to use JOIN to select rows from multiple related columns in one query.

A common mistake is to _forget to use JOIN_ in those situations, and instead fetch all the related data in a loop.

This is called the N+1 query problem, because there is 1 query for the initial list, plus N additional queries for each of the items in the list.

Because this results in so many queries going back and forth between the application and the database, this problem can cause big slowdowns in applications.

## An example N+1 query

Suppose you have a database with a table named "students" and another table named "courses", with a many-to-many relationship represented by an association table "enrollments".

To fetch the name of each student and the courses they're enrolled in, you might write the following code in your application:

```python
students = get_all_students()
for student in students:
    courses = get_courses_by_student(student.id)
    student.courses = courses
```

In this example, `get_all_students` returns a list of all students, and `get_courses_by_student` returns a list of courses for a given student id.

> Say the school had 200 students. How many SQL queries would be issued when running this code snippet?

This approach can quickly become inefficient when the number of students is large, as it requires N+1 queries to the database. 

For each student, an additional query is made to retrieve the courses they're enrolled in.

To solve this issue, you can write a `JOIN`, which, as you've seen, allows you to fetch all the required data in a single query, instead of multiple queries. This can significantly improve the performance of your application, especially when dealing with large datasets.

## Try it: Fix the enrollments N+1 query

Write the SQL statement that you'd use to fetch all of the students with their courses. Use the data model above, with tables for `students`, `courses`, and `enrollments`.

## Why does the N+1 query problem happen?

Since you've seen how to write this query using `JOIN`, you might wonder why any developer would ever write an N+1 query.

Let's think deeper about the python code above:

```python
students = get_all_students()
for student in students:
    courses = get_courses_by_student(student.id)
    student.courses = courses
```

The functions `get_all_students` and `get_courses_by_student` execute SQL queries (a _lot_ of queries!) But, that might not necessarily be obvious to the developer who wrote this code.

They might think that `get_all_students` returns a list of students in memory, or that `get_courses_by_student` is accessing courses in a fast cache.

Often, N+1 queries show up because the underlying functions hide the actual SQL queries and database calls away from the developer. It is not obvious when the database is getting called in a loop!

This is especially the case when teams use an ORM to access their data. Wrapping all of the functionality for the database models behind an object obscures which methods will run a query, and which ones just do some computation.
