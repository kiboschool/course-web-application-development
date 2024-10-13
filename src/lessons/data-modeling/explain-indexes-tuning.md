# Bonus: Database performance

This is not a course on database performance. We're focused on the basics of web applications. The databases we're working with are small, the queries are pretty simple, and we don't have enough users to make our applications slow down much.

One day, though, you will be working on large applications with slow databases, and you'll need some tricks up your sleeve for figuring out why things are slow and what to do to fix them. Database performance is a deep topic, so we'll just touch on some of the briefest. 

Even if you don't read this in depth now, you'll have a reference to return to, or at least some keywords to search.

## Database performance overview

When you send a SQL query to the database, it has to interpret and run that query. Depending on the query, the data in the database, and what other queries are running at the same time, it will run faster or slower. 

Unlike thinking through the performance of your Python code, where you can consider how many times you might execute a loop, SQL statement performance is harder to reason about.

The keys to managing database performance are:

- **Normalization**: Normalizing the database schema can minimize data redundancy and improve data consistency, resulting in improved performance. It's one reason we focus so much on Normalization.
- **Batch processing** (avoiding the N+1 query problem): Processing data in batches instead of processing each record one by one can greatly improve performance, especially when dealing with large datasets.
- **Indexing**: Creating indexes on columns that are frequently used in WHERE clauses, JOIN conditions, and ORDER BY statements can greatly improve query performance.
- **Monitoring and tuning**: Regularly monitoring the database performance, the CPU and memory consumption of your database, looking out for slow queries, and tuning the database parameters (such as the buffer size and the number of connections can help to identify and resolve performance bottlenecks.
- **Measuring and optimizing queries**: If you find slow queries, you can find out why they are slow using tools like explain plans, performance profiling, and query optimization techniques to identify and resolve performance issues.

## Normalization and Batch Processing

You learned about normalization and N+1 queries already. Two of the biggest database issues are data that is _not_ normalized and the N+1 query problem. If you normalize your schema and avoid N+1 queries, you are well on your way to solid database performance.

## Indexes

Indexes are data structures maintained by the database so that they don't have to loop through every row in order to find data to match your query.

Without an index, when you run a SQL query like `SELECT * FROM users WHERE id = 105`, the database has to do something like this under the hood:

```python
results = []
for user in users:
  if user.id == 105:
    results.append(user)
return results
```

If you have a lot of users, that could take a long time!

An index makes that lookup process more like this:

```python
return users[105]
```

No looping through all the users.

Having the right index can make a _world_ of difference to the speed of a query. So, why not index everything?

Indexes also have a cost! When you update a row, the database also has to update any indexes that contain that row. That makes each `INSERT` or `UPDATE` a bit slower.

Since accessing tables by their PRIMARY KEY is so common, SQLite automatically indexes based on the primary key (and has a [specialized, faster index for INTEGER PRIMARY KEYs](https://www.sqlite.org/lang_createtable.html#rowid)). SQLite also creates an index for any UNIQUE column, because it needs to check those columns values every time it inserts or updates a row to confirm there is no duplicate.

If you are frequently querying by a particular column or group of columns, you can create an index manually using the CREATE INDEX command.

> Note: the behavior of indexes is one of the big differences between different databases. SQLite won't be the same as Postgres, which will be different from MySQL. They all have indexes, but the specifics of tuning the indexes on each database is different.

If you want to learn more about indexing in different databases, check out [Use the Index, Luke](https://use-the-index-luke.com/).

## Database Monitoring and Tuning

When we're running small SQLite databases on localhost, there is not a lot to monitor. When you use a hosted database service for a production application, however, you'll usually get graphs and charts that tell you things like:

- how long does each query take?
- what are the average times for different queries?
- what are the slowest queries?
- how much CPU is the database using over time?
- how much memory is the database using over time?
- how many different database connections are there, over time?
- how much time is spent processing the query, vs. sending the results to the application?

Each of these could lead to different moves to make your database or application work better. We won't cover the tuning moves in depth here, but knowing what the problem is can help you to identify potential solutions.

Your application might also log some or all of your SQL queries, which can provide even more data to inspect as you are debugging sources of slowness (or opportunities for speed).

## `EXPLAIN` queries

A particularly helpful tool as you are looking for ways to understand your database and the speed or slowness of queries is the `EXPLAIN` query.

`EXPLAIN` asks the database to tell you how it plans to execute your query.

Different databases offer different kinds of EXPLAIN queries. SQLite offers a high-level overview of the plan of a query with [EXPLAIN QUERY PLAN](https://www.sqlite.org/eqp.html). It tells you the steps that SQLite will do to fulfill your query:

```sql
sqlite> EXPLAIN QUERY PLAN SELECT * FROM students;
QUERY PLAN
`--SCAN students
sqlite> EXPLAIN QUERY PLAN SELECT * FROM students ORDER BY name;
QUERY PLAN
|--SCAN students
`--USE TEMP B-TREE FOR ORDER BY
sqlite> EXPLAIN QUERY PLAN
   ...> SELECT * FROM students
   ...> JOIN assignment_scores on assignment_scores.student_id = students.id
   ...> JOIN assignments ON assignments.id = assignment_scores.assignment_id
   ...> ORDER BY students.id;
QUERY PLAN
|--SCAN assignment_scores
|--SEARCH students USING INTEGER PRIMARY KEY (rowid=?)
|--SEARCH assignments USING INTEGER PRIMARY KEY (rowid=?)
`--USE TEMP B-TREE FOR ORDER BY
```

- `SCAN` means it has to look through the whole table. It's expensive!
- `SEARCH ... USING` means it can use an index. It's typically cheaper than a SCAN
- `USE ...` says how SQLite is doing sorting or grouping for an ORDER, GROUP BY, or DISTINCT statement

You can read more about the output in the [SQLite docs](https://www.sqlite.org/eqp.html).
