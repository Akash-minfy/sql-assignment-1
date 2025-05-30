```js
university_db=> CREATE TABLE students (
university_db(>     student_id INTEGER,
university_db(>     first_name VARCHAR(50),
university_db(>     last_name VARCHAR(50),
university_db(>     email VARCHAR(100),
university_db(>     date_of_birth DATE
university_db(> );
CREATE TABLE
```

```js
university_db=> ALTER TABLE students ADD COLUMN enrollment_date DATE;
ALTER TABLE
university_db=> ALTER TABLE students DROP COLUMN enrollment_date;
ALTER TABLE
university_db=> ALTER TABLE students ALTER COLUMN email TYPE VARCHAR(150);
ALTER TABLE
university_db=> ALTER TABLE students RENAME COLUMN date_of_birth TO dob;
ALTER TABLE
university_db=> ALTER TABLE students ADD CONSTRAINT unique_email UNIQUE (email);
ALTER TABLE
university_db=> ALTER TABLE students RENAME TO learners;
ALTER TABLE
university_db=> ALTER TABLE learners RENAME TO students;
ALTER TABLE
```
```js 
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (1, 'Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
INSERT 0 1
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (2, 'Bob', 'Johnson', 'bob.johnson@example.com', '2002-08-22'),
university_db->        (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
INSERT 0 2
```
```js
university_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)
```
```js
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (4, 'yash', 'Smith', 'yash.smith@example.com', '2003-05-15');
INSERT 0 1
```
```js
university_db=> SELECT * FROM students WHERE student_id = 1;
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15
(1 row)


university_db=> SELECT first_name, last_name FROM students WHERE last_name = 'Smith';
 first_name | last_name
------------+-----------
 Alice      | Smith
 yash       | Smith
(2 rows)


university_db=> SELECT * FROM students WHERE dob >= '2003-01-01';
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | yash       | Smith     | yash.smith@example.com    | 2003-05-15
(3 rows)

```
```js
university_db=> SELECT * FROM students WHERE dob BETWEEN '1995-01-01' AND '2002-12-31';
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(1 row)


university_db=> SELECT * FROM students WHERE student_id = 2;
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(1 row)


university_db=> SELECT * FROM students WHERE dob <= '2024-01-01';
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | yash       | Smith     | yash.smith@example.com    | 2003-05-15
(4 rows)

university_db=> SELECT * FROM students WHERE first_name LIKE 'B%' OR 'C%';
ERROR:  invalid input syntax for type boolean: "C%"
LINE 1: SELECT * FROM students WHERE first_name LIKE 'B%' OR 'C%';
                                                             ^
university_db=> SELECT * FROM students WHERE first_name LIKE 'B%' OR first_name LIKE 'C%';
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)


university_db=> SELECT * FROM students WHERE email LIKE '%example.com';
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | yash       | Smith     | yash.smith@example.com    | 2003-05-15
(4 rows)


university_db=> SELECT * FROM students WHERE email IS NULL;
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)

```

```js
university_db=> SELECT * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | yash       | Smith     | yash.smith@example.com    | 2003-05-15
(4 rows)

university_db=> UPDATE students
university_db-> SET dob='1999-01-12'
university_db-> where student_id=4;
UPDATE 1
university_db=> SELECT * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | yash       | Smith     | yash.smith@example.com    | 1999-01-12
(4 rows)
```

```js
university_db=> SELECT * FROM students ORDER BY last_name ASC;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          4 | yash       | Smith     | yash.smith@example.com    | 1999-01-12
(4 rows)

university_db=> SELECT * FROM students ORDER BY dob DESC;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          4 | yash       | Smith     | yash.smith@example.com    | 1999-01-12
(4 rows)


university_db=> SELECT * FROM students ORDER BY last_name DESC, first_name ASC;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          4 | yash       | Smith     | yash.smith@example.com    | 1999-01-12
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(4 rows)


university_db=> SELECT * FROM students ORDER BY dob ASC LIMIT 3;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          4 | yash       | Smith     | yash.smith@example.com    | 1999-01-12
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)


university_db=> SELECT * FROM students ORDER BY student_id LIMIT 2 OFFSET 1;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)

```
```js
university_db=> SELECT last_name FROM students;
 last_name
-----------
 Smith
 Johnson
 Brown
 Smith
(4 rows)


university_db=> SELECT DISTINCT last_name FROM students;
 last_name
-----------
 Smith
 Johnson
 Brown
(3 rows)


university_db=> SELECT COUNT(email) AS students_with_email FROM students;
 students_with_email
---------------------
                   4
(1 row)


university_db=> SELECT COUNT(*)-COUNT(email) AS students_without_email FROM students;
 students_without_email
------------------------
                      0
(1 row)

```
```js
university_db=> SELECT COUNT(DISTINCT last_name) AS unique_last_names FROM students;
 unique_last_names
-------------------
                 3
(1 row)


university_db=> SELECT COUNT(DISTINCT first_name) AS first_last_names FROM students;
 first_last_names
------------------
                4
(1 row)

 
university_db=> SELECT EXTRACT(YEAR FROM dob) AS birth_year, COUNT(*) AS student_count FROM students GROUP BY birth_year ORDER BY birth_year;
 birth_year | student_count
------------+---------------
       1999 |             1
       2002 |             1
       2003 |             2
(3 rows)
```
```js
university_db=> DROP TABLE IF EXISTS students;
DROP TABLE
university_db=> CREATE TABLE students(student_id INTEGER,first_name VARCHAR(50) NOT NULL,last_name VARCHAR(50) NOT NULL, email VARCHAR(50) NOT NULL,email VARCHAR(100) UNIQUE,dob DATE, enrollment_status VARCHAR(10) CHECK (enrollment_status IN ('enrolled','graduated','dropped')));
ERROR:  column "email" specified more than once
university_db=> CREATE TABLE students(student_id INTEGER,first_name VARCHAR(50) NOT NULL,last_name VARCHAR(50) NOT NULL, email VARCHAR(100) UNIQUE, dob DATE, enrollment_status VARCHAR(10) CHECK (enrollment_status IN ('enrolled','graduated','dropped')));
CREATE TABLE

university_db=> DROP TABLE IF EXISTS students;
DROP TABLE
university_db=> CREATE TABLE students (
university_db(>     student_id SERIAL PRIMARY KEY,
university_db(>     last_name VARCHAR(50) NOT NULL,
university_db(>     email VARCHAR(100) UNIQUE,
university_db(> dob DATE,
university_db(>     enrollment_status VARCHAR(20) CHECK (enrollment_status IN ('enrolled', 'graduated', 'dropped', 'pending'))
university_db(> );
CREATE TABLE
university_db=> CREATE TABLE courses(
university_db(> course_id SERIAL PRIMARY KEY,
university_db(>     course_name VARCHAR(100) NOT NULL UNIQUE,
university_db(>     credits INTEGER CHECK (credits > 0 AND credits < 10) -- Example of CHECK
university_db(> );
CREATE TABLE
```
```js
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Introduction to SQL', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Database Design', 4);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Web Development', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Data Structures', 4);
INSERT 0 1
```
```js
university_db=> CREATE TABLE enrollments (
university_db(>     enrollment_id SERIAL PRIMARY KEY,
university_db(>     student_id INTEGER NOT NULL,
university_db(>     course_id INTEGER NOT NULL,
university_db(>     enrollment_date DATE DEFAULT CURRENT_DATE,
university_db(> grade CHAR(1) CHECK (grade IN ('A', 'B', 'C', 'D', 'F', 'W', NULL)),
university_db(> CONSTRAINT fk_student
university_db(>         FOREIGN KEY (student_id)
university_db(>         REFERENCES students(student_id)
university_db(>         ON DELETE CASCADE,
university_db(> CONSTRAINT fk_course
university_db(>         FOREIGN KEY (course_id)
university_db(>         REFERENCES courses(course_id)
university_db(>         ON DELETE RESTRICT,
university_db(> UNIQUE (student_id,course_id) );
CREATE TABLE
```

```js
university_db=> ALTER TABLE students ADD COLUMN first_name VARCHAR(50) NOT NULL;
ALTER TABLE
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
INSERT 0 1
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
INSERT 0 1
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10', 'pending');
INSERT 0 1
university_db=> SELECT * FROM students;
 student_id | last_name |           email           |    dob     | enrollment_status | first_name
------------+-----------+---------------------------+------------+-------------------+------------
          1 | Smith     | alice.smith@example.com   | 2003-05-15 | enrolled          | Alice
          2 | Johnson   | robert.j@example.com      | 2002-08-22 | enrolled          | Robert          3 | Brown     | charlie.brown@example.com | 2003-01-10 | pending           | Charlie
(3 rows)


university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 1, 'A');
INSERT 0 1
university_db=> INSERT INTO enrollments (student_id, course_id) VALUES (1, 2);
INSERT 0 1
university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (2, 1, 'B');
INSERT 0 1
```
