# Authorization

The first part of 'auth' (Authentication) is all about proving that a user is who they say they are.

The next part, Authorization, is about giving users the right access, based on who they are.

## User-specific data

When a user visits the home page, they expect to see their own data - not someone else's.

One key, but subtle, component of Authorization is fetching data based on the current user. Often, frameworks will provide a helper to get the current user from the session, which can then be used to look up data for that user.

```javascript
return {
  posts: currentUser().posts()
}
```

Usually, Authorization refers to checking that a user has access to particular data. If you fetch data related to the user, the assumption is that they have access to that data.

## Basics of Authorization

At it's core, authorization is about if statements. If the user has permission, then continue. If they don't, raise an exception and show a Forbidden response instead of continuing.

Authorization in many apps uses if statements like this, spread throughout the application.

[This post from Oso](https://www.osohq.com/post/why-authorization-is-hard) runs through some of the reasons why authorization tends to get complicated.

## Role-based access control

A very common starting point for authorization is _role based access control_. Users have Roles, and different Roles have different access.

For instance, in Gradescope, there is a Student role and an Instructor role. Students can submit assignments, and Instructors can view all the assignments and give grades.

In the application, you can imagine a code snippet like this:

```javascript
if (currentUser().instructor) {
  let scores = getAssignmentScores()
  render('scores.html', { scores });
} else {
  redirect('/', 302);
}
```

If the current user is an instructor, show the scores. Otherwise, redirect to the home page, since they are not authorized.

Roles are important to design carefully. Can a user be both an instructor and a student? What if they are in multiple classes? Getting the data model right for roles takes careful thought.

## Further Reading: Authorization

If you want to learn more about designing Authorization, check out [Authorization Academy by Oso](https://www.osohq.com/academy).
