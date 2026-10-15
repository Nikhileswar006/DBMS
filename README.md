# DBMS
DBMS project
# Smart Student Study Planner

## 1. Project Title

**Smart Student Study Planner — Database Management System Project**

**Technology Stack:** HTML, CSS, JavaScript, Python Flask, PostgreSQL

**Database:** `smart_student_study_planner`

### Team Members

| S. No. | Team Member  | Roll Number     |
| ------ | ------------ | --------------- |
| 1      | B. Nikhil    | CB.SC.U4AIE24063|
| 2      | Sane Sandeep | CB.SC.U4AIE24047|
| 3      | Adith        | CB.SC.U4AIE24003|

---

## 2. Project Overview

### Introduction

The Smart Student Study Planner is a database-driven web application designed to organize student information and academic activities in a structured manner.

Students often need to manage multiple subjects, topics, study schedules, study sessions, examinations, and reminders. Managing these activities manually can make it difficult to track progress and maintain organized records.

This project uses a relational database to store and manage academic information. The frontend provides a user interface, the Flask backend processes user requests, and PostgreSQL stores the application data.

### Problem Statement

Managing student information, subjects, study plans, topics, study logs, examinations, and reminders manually can lead to duplicate records, inconsistent information, and difficulty retrieving related data.

The objective is to develop a centralized database-backed application that organizes these records, maintains relationships between entities, enforces data integrity, and supports efficient database operations.

### Objectives

- Store and manage student information.
- Maintain subject details and student-subject relationships.
- Organize topics under subjects.
- Maintain study plans and study-session records.
- Store examination schedules and marks.
- Manage reminders associated with study plans.
- Implement CRUD operations (Create, Read, Update, Delete).
- Apply database constraints and normalization.
- Demonstrate SQL queries for retrieving and analyzing related records.

### Project Scope

The database schema contains eight tables:

1. `students`
2. `subjects`
3. `student_subject`
4. `topics`
5. `study_plan`
6. `study_log`
7. `exams`
8. `reminders`

The implemented application features should be distinguished from the complete database design. Only features actually connected to the frontend and backend should be claimed as fully implemented.

---

## 3. System Requirements and Architecture

### Hardware Requirements

- Computer or laptop
- Minimum 4 GB RAM recommended
- Sufficient storage for the application, database, and project files

### Software Requirements

| Component               | Requirement                      |
| ----------------------- | -------------------------------- |
| Operating System        | Windows, Linux, or macOS         |
| Programming Language    | Python                           |
| Backend Framework       | Flask                            |
| Frontend                | HTML, CSS, JavaScript            |
| Database                | PostgreSQL                       |
| Database Administration | pgAdmin                          |
| Python Database Driver  | psycopg2                         |
| Code Editor             | Visual Studio Code or equivalent |
| Browser                 | Chrome, Firefox, or equivalent   |

### System Architecture

The application follows a three-layer architecture.

**1. Presentation Layer**

HTML, CSS, and JavaScript provide the user interface, forms, navigation, and display of application data.

**2. Application Layer**

Python Flask receives requests, validates input, executes application logic, and communicates with PostgreSQL through `psycopg2`.

**3. Database Layer**

PostgreSQL stores student, subject, topic, study-plan, study-log, examination, and reminder records.

### Architecture Diagram

```text
+-----------------------------+
|       User / Student        |
+-----------------------------+
              |
              v
+-----------------------------+
|       Frontend Layer        |
|    HTML, CSS, JavaScript    |
+-----------------------------+
              |
        HTTP Requests
              |
              v
+-----------------------------+
|       Backend Layer         |
|         Python Flask        |
|   Validation and CRUD Logic |
+-----------------------------+
              |
        psycopg2 Driver
              |
              v
+-----------------------------+
|       Database Layer        |
|          PostgreSQL         |
|  smart_student_study_planner|
+-----------------------------+
```

---

## 4. ER Diagram and UML Diagram

### 4.1 Entity–Relationship (ER) Diagram

The ER diagram represents the entities, attributes, primary keys, foreign keys, and relationships in the Smart Student Study Planner.

The database design contains the following entities:

- **STUDENT:** Stores student details.
- **SUBJECT:** Stores subject information.
- **STUDENT_SUBJECT:** Connects students and subjects through a many-to-many relationship.
- **TOPIC:** Stores topics belonging to subjects.
- **STUDY_PLAN:** Stores study plans created for students.
- **STUDY_LOG:** Records study sessions for topics.
- **EXAMS:** Stores examination details and marks.
- **REMINDERS:** Stores reminders associated with study plans.

Save the ER diagram image in the repository and reference it as follows:

<p align="center">
  <img src="Your paragraph text (1).png" width="700" alt="Image">
</p>

Replace `docs/er_diagram.png` with the actual path and filename of your image.

### 4.2 UML Use-Case Diagram

The UML use-case diagram represents the actions available to the Student user.

Depending on the features implemented in the application, these actions may include:

- Managing student information
- Managing subjects
- Managing topics
- Creating and viewing study plans
- Recording study sessions
- Managing examination details
- Managing reminders

Save the UML diagram image in the repository and reference it as follows:

<p align="center">
  <img src="Student Study Management Use-Case Diagram.png" width="700" alt="Use-Case Diagram">
</p>

Replace the image path with the actual location of your UML diagram.

---

## 5. Relational Schema Mapping

The relational schema is derived from the ER model. Each entity is represented as a table, and relationships are represented using foreign keys or a junction table.

### 5.1 STUDENTS

```text
STUDENTS(
    student_id PK,
    name,
    email UNIQUE
)
```

- `student_id` is the primary key.
- `email` is unique and cannot be null.

### 5.2 SUBJECTS

```text
SUBJECTS(
    subject_id PK,
    subject_name,
    description,
    credits
)
```

- `subject_id` is the primary key.
- `credits` must be positive when a value is provided.

### 5.3 STUDENT_SUBJECT

```text
STUDENT_SUBJECT(
    student_id PK, FK,
    subject_id PK, FK
)
```

This junction table implements the many-to-many relationship between students and subjects.

The composite primary key `(student_id, subject_id)` prevents the same student-subject association from being inserted more than once.

### 5.4 TOPICS

```text
TOPICS(
    topic_id PK,
    topic_name,
    description,
    subject_id FK
)
```

Each topic belongs to a subject.

### 5.5 STUDY_PLAN

```text
STUDY_PLAN(
    study_plan_id PK,
    student_id FK,
    plan_name,
    start_date,
    end_date,
    status
)
```

Each study plan belongs to a student. The end date cannot be earlier than the start date.

### 5.6 STUDY_LOG

```text
STUDY_LOG(
    study_log_id PK,
    topic_id FK,
    study_date,
    duration_minutes,
    notes
)
```

Each study log records a study session associated with a topic.

### 5.7 EXAMS

```text
EXAMS(
    exam_id PK,
    student_id FK,
    subject_id FK,
    exam_name,
    exam_date,
    exam_time,
    total_marks,
    marks_obtained
)
```

The table connects an examination to a student and a subject. Check constraints validate marks and prevent negative values or marks obtained exceeding total marks.

### 5.8 REMINDERS

```text
REMINDERS(
    reminder_id PK,
    study_plan_id FK,
    title,
    reminder_date,
    reminder_time,
    is_completed
)
```

Each reminder belongs to a study plan. The completion flag defaults to `FALSE`.

### Relationship Summary

| Relationship              | Cardinality |
| ------------------------- | ----------- |
| STUDENT — STUDENT_SUBJECT | One-to-many |
| SUBJECT — STUDENT_SUBJECT | One-to-many |
| SUBJECT — TOPICS          | One-to-many |
| STUDENT — STUDY_PLAN      | One-to-many |
| TOPICS — STUDY_LOG        | One-to-many |
| STUDENT — EXAMS           | One-to-many |
| SUBJECT — EXAMS           | One-to-many |
| STUDY_PLAN — REMINDERS    | One-to-many |

Together, `STUDENT_SUBJECT` and its two foreign keys represent the many-to-many relationship between STUDENTS and SUBJECTS.

---

## 6. Normalization and Functional Dependencies

Normalization organizes data into relations to reduce redundancy and prevent insertion, update, and deletion anomalies.

### 6.1 Functional Dependencies

A functional dependency (X \rightarrow Y) means that the attributes in (X) uniquely determine the attributes in (Y).

| Table           | Functional Dependencies                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------ |
| STUDENTS        | `student_id → name, email`                                                                       |
| STUDENTS        | `email → student_id, name`                                                                       |
| SUBJECTS        | `subject_id → subject_name, description, credits`                                                |
| STUDENT_SUBJECT | `(student_id, subject_id)` uniquely identifies each association                                  |
| TOPICS          | `topic_id → topic_name, description, subject_id`                                                 |
| STUDY_PLAN      | `study_plan_id → student_id, plan_name, start_date, end_date, status`                            |
| STUDY_LOG       | `study_log_id → topic_id, study_date, duration_minutes, notes`                                   |
| EXAMS           | `exam_id → student_id, subject_id, exam_name, exam_date, exam_time, total_marks, marks_obtained` |
| REMINDERS       | `reminder_id → study_plan_id, title, reminder_date, reminder_time, is_completed`                 |

**Note:** The dependency `email → student_id, name` is valid because the `students` table declares `email` as both `UNIQUE` and `NOT NULL`. Email is therefore a candidate key, although `student_id` is the selected primary key.

### 6.2 First Normal Form (1NF)

A relation is in 1NF when each attribute contains a single value and there are no repeating groups.

In this project:

- Student details are stored in separate columns.
- Each subject is represented by an individual record.
- Study sessions are stored as separate records.
- Student-subject associations are stored in individual rows in `student_subject`.

### 6.3 Second Normal Form (2NF)

A relation is in 2NF when it is in 1NF and every non-key attribute depends on the whole candidate key.

Most tables use single-column primary keys, so partial dependencies on a composite primary key do not arise.

The `student_subject` table has a composite primary key but contains no non-key attributes. Therefore, it has no partial dependency involving non-key attributes.

### 6.4 Third Normal Form (3NF)

A relation is in 3NF when it is in 2NF and non-key attributes do not have inappropriate transitive dependencies on a candidate key.

The design separates student, subject, topic, study-plan, study-log, examination, and reminder information into their respective tables. This avoids repeatedly storing complete details of related entities in the same table.

The final 3NF claim should be verified against all actual functional dependencies in the implemented schema.

---

## 7. Methodology and Database Design

The project follows a structured database development methodology.

### Step 1: Requirement Analysis

Identify the information needed to manage students, subjects, topics, study plans, study sessions, examinations, and reminders.

### Step 2: Conceptual Design

Identify entities, attributes, primary keys, and relationships. Represent these using the ER diagram.

### Step 3: Logical Design

Convert the ER model into relational tables. Use a junction table for the many-to-many relationship between students and subjects.

### Step 4: Normalization

Identify functional dependencies and examine the tables for 1NF, 2NF, and 3NF.

### Step 5: Physical Database Implementation

Create the tables in PostgreSQL using primary keys, foreign keys, uniqueness constraints, check constraints, and default values.

### Step 6: Backend Development

Use Flask and `psycopg2` to connect the application to PostgreSQL and process database operations.

### Step 7: Frontend Development

Use HTML, CSS, and JavaScript to create the interface and interact with the Flask backend.

### Step 8: Testing

Test database connectivity, CRUD operations, foreign-key constraints, uniqueness constraints, and invalid input handling.

### Database Integrity Rules

- Student email addresses must be unique and non-null.
- Subject credits must be positive when specified.
- A student-subject association must reference existing students and subjects.
- Topics must reference an existing subject.
- Study plans must reference an existing student.
- Study-log durations must be greater than zero.
- Examination marks must satisfy the defined check constraints.
- Reminders must reference an existing study plan.

Foreign keys use `ON DELETE CASCADE` where defined in the schema. Deleting a referenced record can therefore remove its dependent records.

---

## 8. Advanced SQL Queries and Their Purpose

The following queries are based on the project's schema.

### 8.1 Insert a Student

**Purpose:** Adds a new student record.

```sql
INSERT INTO students (name, email)
VALUES ('Asha Kumar', 'asha@example.edu');
```

The database generates `student_id` automatically.

### 8.2 Retrieve All Students

**Purpose:** Displays all student records.

```sql
SELECT student_id, name, email
FROM students
ORDER BY student_id;
```

### 8.3 Update a Student

**Purpose:** Changes a student's name.

```sql
UPDATE students
SET name = 'Asha K.'
WHERE student_id = 1;
```

### 8.4 Delete a Student

**Purpose:** Deletes a student and applies the configured cascading rules to dependent records.

```sql
DELETE FROM students
WHERE student_id = 1;
```

Use this query carefully because dependent records can also be deleted through cascading foreign keys.

### 8.5 Retrieve Subjects for Each Student

**Purpose:** Uses joins to display the many-to-many relationship.

```sql
SELECT
    s.student_id,
    s.name,
    sub.subject_id,
    sub.subject_name
FROM students AS s
JOIN student_subject AS ss
    ON ss.student_id = s.student_id
JOIN subjects AS sub
    ON sub.subject_id = ss.subject_id
ORDER BY s.name, sub.subject_name;
```

### 8.6 Count Topics per Subject

**Purpose:** Uses an aggregate function to count topics under each subject, including subjects with no topics.

```sql
SELECT
    s.subject_id,
    s.subject_name,
    COUNT(t.topic_id) AS topic_count
FROM subjects AS s
LEFT JOIN topics AS t
    ON t.subject_id = s.subject_id
GROUP BY s.subject_id, s.subject_name
ORDER BY s.subject_name;
```

### 8.7 Find Study Time per Topic

**Purpose:** Calculates the total recorded study time for each topic.

```sql
SELECT
    t.topic_id,
    t.topic_name,
    COALESCE(SUM(sl.duration_minutes), 0) AS total_minutes
FROM topics AS t
LEFT JOIN study_log AS sl
    ON sl.topic_id = t.topic_id
GROUP BY t.topic_id, t.topic_name
ORDER BY total_minutes DESC;
```

### 8.8 Find Upcoming Exams

**Purpose:** Retrieves examinations scheduled from the current date onward.

```sql
SELECT
    e.exam_name,
    e.exam_date,
    e.exam_time,
    s.name,
    sub.subject_name
FROM exams AS e
JOIN students AS s
    ON s.student_id = e.student_id
JOIN subjects AS sub
    ON sub.subject_id = e.subject_id
WHERE e.exam_date >= CURRENT_DATE
ORDER BY e.exam_date, e.exam_time;
```

### 8.9 Find Incomplete Reminders

**Purpose:** Displays reminders that have not been completed.

```sql
SELECT
    r.title,
    r.reminder_date,
    r.reminder_time,
    sp.plan_name
FROM reminders AS r
JOIN study_plan AS sp
    ON sp.study_plan_id = r.study_plan_id
WHERE r.is_completed = FALSE
ORDER BY r.reminder_date, r.reminder_time;
```

### 8.10 Find Subjects with Above-Average Credits

**Purpose:** Demonstrates a subquery by comparing each subject's credits against the average.

```sql
SELECT subject_id, subject_name, credits
FROM subjects
WHERE credits > (
    SELECT AVG(credits)
    FROM subjects
    WHERE credits IS NOT NULL
);
```

### 8.11 Verify All Database Tables

**Purpose:** Lists the base tables in the current PostgreSQL schema.

```sql
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'public'
  AND table_type = 'BASE TABLE'
ORDER BY table_name;
```

---

## 9. Installation, Setup, and Execution Instructions

### Prerequisites

Install the following software:

- Python
- PostgreSQL
- pgAdmin (optional, but useful for database administration)
- Visual Studio Code or another code editor

### Step 1: Clone the Repository

Replace the URL with your actual GitHub repository URL.

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <YOUR_PROJECT_FOLDER>
```

### Step 2: Create a Virtual Environment

```bash
python -m venv venv
```

Activate it on Windows PowerShell:

```powershell
.\venv\Scripts\Activate.ps1
```

On Windows Command Prompt:

```bat
venv\Scripts\activate
```

On Linux or macOS:

```bash
source venv/bin/activate
```

### Step 3: Install Dependencies

If the project contains `requirements.txt`, run:

```bash
pip install -r requirements.txt
```

Otherwise, install the packages required by the application:

```bash
pip install Flask psycopg2-binary
```

If the application uses additional Python libraries, install those as well.

### Step 4: Create the PostgreSQL Database

Open pgAdmin or connect through `psql` and execute:

```sql
CREATE DATABASE smart_student_study_planner;
```

Connect to the newly created database before executing the schema.

### Step 5: Create the Tables

Run the complete database schema SQL supplied with the project.

Execute the `CREATE TABLE` statements in dependency order:

1. `students`
2. `subjects`
3. `student_subject`
4. `topics`
5. `study_plan`
6. `study_log`
7. `exams`
8. `reminders`

Run the table-verification query afterward to confirm that all eight tables exist.

If the tables already exist, do not rerun the `CREATE TABLE` statements blindly. Use a fresh database or a carefully prepared migration to avoid relation-already-exists errors.

### Step 6: Configure Database Credentials

Configure the database connection in the Flask application.

Prefer environment variables rather than hardcoding passwords.

Example PowerShell configuration:

```powershell
$env:DB_HOST = "localhost"
$env:DB_PORT = "5432"
$env:DB_NAME = "smart_student_study_planner"
$env:DB_USER = "postgres"
$env:DB_PASSWORD = "<YOUR_POSTGRESQL_PASSWORD>"
```

The application must read the same environment variable names used in this example, or the variable names must be adjusted to match its configuration.

Never commit real database passwords to GitHub.

### Step 7: Run the Flask Application

If the main application file is named `app.py`, run:

```bash
python app.py
```

Alternatively, if the application is configured for the Flask CLI:

```bash
flask --app app run --debug
```

Use only the command appropriate for the existing application.

### Step 8: Open the Application

Open the local URL printed in the terminal, commonly:

```text
http://127.0.0.1:5000
```

Use the application's navigation to access the available pages and test the implemented features.

---

## 10. Demonstration Instructions and Database Reproduction

This section explains how to reproduce the database state and demonstrate the project.

### 10.1 Reproduce the Database

1. Create a new PostgreSQL database named `smart_student_study_planner`.
2. Execute the complete schema SQL.
3. Verify that all eight tables have been created.
4. Insert sample data in the correct dependency order.
5. Start the Flask backend with valid database credentials.
6. Open the application in a browser.
7. Perform the supported operations and verify the results in PostgreSQL.

### 10.2 Suggested Sample Data

Use the following fictional sample records for demonstration.

```sql
INSERT INTO students (name, email)
VALUES
    ('Asha Kumar', 'asha@example.edu'),
    ('Rahul Das', 'rahul@example.edu');

INSERT INTO subjects (subject_name, description, credits)
VALUES
    ('Database Systems', 'Relational databases and SQL', 4),
    ('Python Programming', 'Programming fundamentals', 3);

INSERT INTO student_subject (student_id, subject_id)
VALUES
    (1, 1),
    (1, 2),
    (2, 1);

INSERT INTO topics (topic_name, description, subject_id)
VALUES
    ('Normalization', 'Database normal forms', 1),
    ('SQL Joins', 'Combining relational tables', 1),
    ('Python Functions', 'Function definitions and calls', 2);

INSERT INTO study_plan
    (student_id, plan_name, start_date, end_date, status)
VALUES
    (1, 'DBMS Revision', CURRENT_DATE,
     CURRENT_DATE + 7, 'Pending');

INSERT INTO study_log
    (topic_id, study_date, duration_minutes, notes)
VALUES
    (1, CURRENT_DATE, 45, 'Studied normalization');

INSERT INTO exams
    (student_id, subject_id, exam_name, exam_date,
     exam_time, total_marks, marks_obtained)
VALUES
    (1, 1, 'DBMS Internal', CURRENT_DATE + 10,
     '10:00', 100, 85);

INSERT INTO reminders
    (study_plan_id, title, reminder_date, reminder_time)
VALUES
    (1, 'Revise normalization',
     CURRENT_DATE + 1, '18:00');
```

**Important:** These example inserts assume the database is fresh and that the generated student and subject IDs begin at 1. If existing data or sequence values differ, retrieve the actual IDs and use them instead.

### 10.3 Demonstrate CRUD Operations

**Create:** Add a student or subject through the application. Verify that the row appears in PostgreSQL.

**Read:** Open the relevant page and verify that stored records are displayed correctly.

**Update:** Modify an existing record and confirm that the updated values are stored in PostgreSQL.

**Delete:** Delete a test record and confirm that the deletion is reflected in the database. Be aware of the cascading foreign-key rules.

### 10.4 Demonstrate Database Integrity

Test the following cases:

- Insert two students with the same email; the second insertion should fail.
- Insert a subject with zero or negative credits; the check constraint should reject it.
- Insert a student-subject association with a nonexistent student or subject; the foreign key should reject it.
- Insert a study log with a non-positive duration; the check constraint should reject it.
- Insert an examination where marks obtained exceed total marks; the check constraint should reject it.
- Attempt to create a study plan with an end date earlier than its start date; the check constraint should reject it.

### 10.5 Verify the Database State

Run:

```sql
SELECT COUNT(*) FROM students;
SELECT COUNT(*) FROM subjects;
SELECT COUNT(*) FROM student_subject;
SELECT COUNT(*) FROM topics;
SELECT COUNT(*) FROM study_plan;
SELECT COUNT(*) FROM study_log;
SELECT COUNT(*) FROM exams;
SELECT COUNT(*) FROM reminders;
```

These queries show the number of records in each table.

### 10.6 Demonstration Checklist

- [ ] PostgreSQL database created successfully.
- [ ] All eight tables created successfully.
- [ ] Flask application connects to PostgreSQL.
- [ ] Frontend pages load successfully.
- [ ] Implemented CRUD operations work.
- [ ] Changes made through the application appear in PostgreSQL.
- [ ] Primary-key, foreign-key, unique, and check constraints behave correctly.
- [ ] ER diagram and UML diagram are included in the repository.
- [ ] SQL queries execute successfully.
- [ ] Screenshots of the working application and query results are included if required.

---

## Conclusion

The Smart Student Study Planner demonstrates the use of relational database design, functional dependencies, normalization, primary and foreign keys, integrity constraints, SQL queries, and application-to-database connectivity.

The database design organizes student information, subjects, topics, study plans, study logs, examinations, and reminders into related tables. The Flask backend and web frontend provide a foundation for performing database operations through an application interface.

Future enhancements may include progress dashboards, study analytics, authentication, improved search, notifications, and additional study-planning features.

---

## Future Scope

- Develop study-progress dashboards and analytics.
- Add student authentication and authorization.
- Provide automated reminders for exams and study plans.
- Improve search, filtering, and data validation.
- Add reports showing study time and topic completion.
- Extend testing and improve the user interface.
