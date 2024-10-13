# Entity-Relationship Diagrams

An entity-relationship diagram (ERD) is a graphical representation of entities and their relationships to each other, used in the design of a relational database. It provides a visual representation of the entities, attributes, and relationships in a system, and helps to illustrate how data is organized and related.

An ERD typically consists of entities, which are objects or concepts that are being modeled, and relationships, which describe the connections between entities. Each entity is represented as a rectangle, and each relationship is represented as a line connecting two entities.

ERDs are a useful tool for modeling and visualizing the structure of relational databases, and can help to ensure that data is organized, consistent, and free of redundancies and anomalies.

ERDs also help with communication between database designers, developers, and stakeholders, providing a common understanding of the data structure and relationships.

## Video: Introduction to ERDs

This video from LucidChart explains how to create ERDs.

<div class="embed"><iframe src="https://www.youtube.com/embed/QpdhBUYk7Kk" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

## Example: Customers, Products, Orders

Here's two different ERDs showing the relationships between customers, products, and orders.

![Basic ERD](/images/erd-basic.png)

![ERD showing columns](/images/erd-with-details.png)

The ERD with more details is a complete specification of the schema.

When there are more tables or the schema is not yet fully designed, it's often useful to create a more basic ERD without all the details.

> Note: there are many different visual syntaxes you can find for representing entities and attributes. A common notation is to [show attributes as ovals](https://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model#/media/File:ER_Diagram_MMORPG.png). It is visually noisy, so we stick to showing tables with lines and arrows in these materials.

## Practice: Draw an ERD

ERDs are a powerful design tool. Practice drawing an ERD based on a schema.

You can use any drawing tool you like. The ERDs above were created using [Excalidraw](https://excalidraw.com/) and [Visual Paradigm](https://online.visual-paradigm.com/diagrams/features/erd-tool/); Figma and LucidChart are other popular tools.

Create an ERD based on this schema. The diagram should include entities for `student`, `course`, `assignment`, and `assignment_score`, as well as relationships between these entities to represent the foreign key constraints. You can choose whether to represent the attributes of each entity.

```sql
CREATE TABLE student (
    student_id INTEGER PRIMARY KEY,
    name TEXT,
    email TEXT
);

CREATE TABLE instructors (
  instructor_id INTEGER PRIMARY KEY,
  name TEXT,
);

CREATE TABLE course (
    course_id INTEGER PRIMARY KEY,
    course_name TEXT,
    instructor_id INTEGER
    FOREIGN KEY (instructor_id) REFERENCES instructors (instructor_id)
);

CREATE TABLE assignment (
    assignment_id INTEGER PRIMARY KEY,
    course_id INTEGER,
    assignment_name TEXT,
    due_date DATE,
    FOREIGN KEY (course_id) REFERENCES course (course_id)
);

CREATE TABLE assignment_score (
    student_id INTEGER,
    assignment_id INTEGER,
    score INTEGER,
    FOREIGN KEY (student_id) REFERENCES student (student_id),
    FOREIGN KEY (assignment_id) REFERENCES assignment (assignment_id)
);
```

## Practice: Translate an ERD into a schema

In addition to creating an ERD, you also need to be able to take an ERD and create a schema.

From the image of the ERD below, write the CREATE TABLE statements needed to make the database tables that match the diagram. Note that `N`` stands for "nullable" – you use it when there can be NULL values in a column. Otherwise, the NULL values won't be accepted.

![ERD showing photo, album, location, member, comment, and tag entities](https://i.pinimg.com/originals/2e/a3/71/2ea371ef6415382d1eda71d125d30c24.png)

## Practice: Draw an ERD for a many to many relationship

Consider a situation where you have two entities, students and courses. A student can enroll in multiple courses, and a course can have multiple students.

Draw the ERD representing this schema. Include a table called "enrollments" with foreign keys to both the "students" and "courses" tables.
