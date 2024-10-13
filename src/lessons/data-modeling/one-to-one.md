# One-to-one relationships

### What is a One-to-One Relationship?

A one-to-one relationship between two entities (or tables) means that a single record in the first entity corresponds to one (and only one) record in the second entity, and vice versa.

For instance, consider the relationship between a person and a passport. In many countries, a person can have only one valid passport, and each passport is issued to a single individual. This relationship between a person and a passport is a one-to-one relationship.

![one-to-one-relationship](../../images/one-to-one-passport.jpeg)

#### Characteristics

1. **Uniqueness**: Each record in Table A can have only one corresponding record in Table B.
2. **Bidirectional**: If Table A has a relation to Table B, then Table B also has a relation to Table A.
3. **Foreign Key**: One of the tables usually has a foreign key that references the primary key of the other table.

#### Implementation Guide

Let's use the aforementioned "Person and Passport" example to demonstrate a one-to-one relationship implementation in a relational database (using SQL as an example).

#### Step 1: Create the Tables

We'll start by creating the `Person` and `Passport` tables:

```sql
CREATE TABLE Person (
    person_id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);

CREATE TABLE Passport (
    passport_id INT PRIMARY KEY,
    issue_date DATE,
    expiration_date DATE,
    person_id INT,
    FOREIGN KEY (person_id) REFERENCES Person(person_id)
);
```

In the above structure, `person_id` in the `Passport` table acts as a foreign key that references `person_id` in the `Person` table.

#### Step 2: Inserting Data

Insert a person and a corresponding passport:

```sql
INSERT INTO Person (person_id, name, age) VALUES (1, 'John Doe', 30);

INSERT INTO Passport (passport_id, issue_date, expiration_date, person_id) VALUES (101, '2023-01-01', '2033-01-01', 1);
```

#### Step 3: Querying Data

To fetch the details of a person and their passport:

```sql
SELECT p.name, pp.issue_date, pp.expiration_date
FROM Person p
JOIN Passport pp ON p.person_id = pp.person_id
WHERE p.name = 'John Doe';
```

This will retrieve John Doe's passport details. The query uses a JOIN, we will review JOINs in a subsequent lesson.

