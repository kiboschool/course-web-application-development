# Database constraints

A key software design principle is "Defense in depth". It's commonly applied to security, but it applies equally well to data validity and ensuring that there aren't bugs.

Client-side validation can be bypassed by an attacker. Even server-side validation can still have errors.

Database validation can provide another layer of constraints that ensure that your data is valid.

While the constraints provided by a database are often less flexible than ones you can write for your server, they are critical to prevent weird bugs and situations.

For instance, your application probably is not designed to have two different users with the same email address. That would probably cause all kinds of headaches! Database constraints can prevent that kind of issue.

Read the [SQLBolt Lesson on Creating Tables](https://sqlbolt.com/lesson/creating_tables) for a taste of the types of constraints you can create, and the syntax for doing so.

<details><summary>What are some of the key ways constriants can protect the validity of your data?</summary>

- Validate the type of data
- Check the uniqueness of a field across all the rows in a table
- Make sure a field is not null
- Confirm that a foreign key exists in another table (e.g. make sure that a `user` exists before creating an `order` associated with them)

You can also create custom CHECK constraints, but we won't cover those.

</details>

Next week, we'll discuss constraints in more detail when we cover Data Modeling.
