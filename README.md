# SQL Practice & Cheat Sheet (MySQL & PostgreSQL)

*SQL is a programming language used to interact with relational databases.*
*It is used to perform CRUD operations: Create, Read, Update, and Delete.*

### **What is data?**
*Data is raw, unprocessed facts and figures collected from different sources. It can be numbers, text, images, or symbols that by itself has no clear meaning until analyzed.*

### **What are the differences between data and information?**
| **Data**               | **Information**                           |
| ---------------------- | ----------------------------------------- |
| Raw, unprocessed facts | Processed, organized, and meaningful data |
| Example: `23, 45, 67`  | Example: "The average score is 45"        |
| Has no direct meaning  | Has meaning, helps in decision-making     |
| Input for processing   | Output of processing                      |

“Data is the raw material, and information is the finished product that gives meaning to the data.”

### **What is a database engineer?**

*A Database Engineer is a professional who designs, builds, and manages databases to make sure data is stored safely, organized efficiently, and retrieved quickly. They act like architects of data systems—ensuring the right structure, performance, and security so that businesses can make smart use of their information.*

- **Database:** *An organized collection of related data.*
- **Entities:** Real-world objects we store data about (e.g., Student, Course).
- **Relationships:** Associations between entities (e.g., John ENROLLED in Database course).
- **Database Management System (DBMS):** Software to create, store, update, and query databases. **(Provides security, consistency, and controlled access. *Examples: MySQL, PostgreSQL, Oracle, SQL Server.*)**

### **Types of Databases**
1. Relational Databases (RDBMS)
- Data stored in tables (rows & columns).
- Use SQL for querying.
- Examples: MySQL, PostgreSQL, Oracle.
- Used in banking and university systems.

2. NoSQL (Not Only SQL) Databases – non-relational
- Flexible, schema-less, handles big & unstructured data.
- Data not stored in tables.
- Data can be stored as: documents, graphs, key-value pairs
- Used in social media, recommendation systems

### **Database Users**
*Database users can be broadly grouped into two categories:*

**- Actors on the Scene (directly interact with the database)**
  
1. Database administrators - Control and monitor database use.
*Responsibilities:*
- Authorize access (who can read/write).
- Set up backups and recovery.
- Ensure security.
- 
2. Database Designers - Decide what data will be stored and how it will be organized.
*Responsibilities:*
- Define tables, relationships, and constraints.
- Design the ER model and schema.
- Ensure the database supports business requirements.

3. End-Users - The largest group — people who actually use the data.
*For example:*
- Naïve users → use standard applications (e.g., bank clerk).
- Sophisticated users → Sophisticated users like engineers or analysts interact directly with the database using SQL queries.

**- Workers Behind the Scene (don’t use the data directly, but make DBMS possible)**

- DBMS system developers → build the database engine itself.
- Tool developers → build utilities like MySQL Workbench
- Computer system operators → manage servers, hardware, and OS where DB runs.
- Maintenance staff → update, optimize DBMS software.


**Manipulating a Database**
- Querying → retrieve specific information (e.g., list all students in a course).
- Updating → insert, delete, modify records. e.g., Add/delete or update student information.
- Reporting → generate summaries and insights (e.g., average grades, monthly sales).

**Database engineer roles and responsibilities:**
1. Design and Implementation
2. Normalization
3. Optimization
4. Backup and Recovery
5. Security
6. Data Migration
7. Integration
8. Capacity Planning
9. Documentation
10. Testing and QA
11. Reporting

*ACID Properties: Atomicity, Consistency, Isolation, Durability*

### DBMS Data Models

A **data model** in DBMS is a framework used to define how data is structured, stored, and managed. It helps in bridging the gap between real-world data requirements and the internal structure of a database.
**Purpose of Data Modeling**
- To understand the data requirements of a system.
- To define entities (things), their attributes (properties), and relationships (connections).


**Layers of Data Modeling**

| Level | Purpose | Examples / Features |
|---|---|---|
| **Conceptual (High-level)** | Captures business semantics & requirements | Entity-Relationship (ER) diagram, entities, attributes, relationships |
| **Logical (Representational)** | Defines the logical structure independent of DBMS | Relational model: tables, relational algebra/calculus |
| **Physical** | Specifies how data is stored in the DBMS | Tables, indexes, data types, storage, file structures, access paths |

**Other Data Models**

- **Hierarchical Model** — tree-like parent-child data structure  
- **Network Model** — supports many-to-many relationships  
- **Object-Oriented Model** — data as objects with attributes and methods  
- **Float Model** — 2D array representation, limited scalability  
- **Context Model** — composite of multiple models  
- **Semi-Structured Model** — flexible schema (e.g. XML, JSON)

**Advantages:**
1. Accurate and clear representation of data  
2. Helps avoid redundancy, identify missing data  
3. Supports constraints, relationships, and security  
4. Provides a roadmap for implementing the database  

**Disadvantages:**
1. Complexity in large databases  
2. Requires deep DBMS / storage knowledge  
3. Structural changes can ripple across the system  
4. No universal data manipulation language  
5. Good modeling needs knowledge of physical storage constraints   

**Degree of a Relationship**
*Definition: Number of entity types that participate in a relationship.*
- Unary (degree 1): Relationship within the same entity (e.g., Employee manages Employee).
- Binary (degree 2): Between two entities (e.g., Student enrolls in Course).
- Ternary (degree 3): Among three entities (e.g., Doctor prescribes Medicine to Patient).

**Cardinality in Relationships**
*Definition: Specifies how many instances of one entity can/must be associated with instances of another entity.*
- One-to-One (1:1): Each Student has one Locker.
- One-to-Many (1:N): One Instructor teaches many Courses.
- Many-to-Many (M:N): Students enroll in many Courses, and each Course has many Students.

**[ER Diagrams Guide](https://nulab.com/learn/software-development/entity-relationship-diagrams-guide/?utm_source=chatgpt.com)**
**[Create Diagram with ERDPlus](https://erdplus.com/)**
### ER-to-Relational Mapping Algorithm
- Step 1: Mapping of Regular Entity Types 
- Step 2: Mapping of Weak Entity Types 
- Step 3: Mapping of Binary 1:1 Relation Types 
- Step 4: Mapping of Binary 1:N Relationship Types
- Step 5: Mapping of Binary M:N Relationship Types
- Step 6: Mapping of Multivalued attributes

## Relational Integrity Constraints Structured Query Language (SQL)
*Constraints are conditions that must be true on all valid tuples. These conditions are called Relational Integrity Constraints. 
There are three main types of constraints:* 
1. Key constraints 
- Every relation in the database should have at least one set of attributes which defines a tuple uniquely. Those set of attributes is called key.
- If there are more than one, these are called candidate keys. 
- Primary Key: A candidate key that is chosen to uniquely identify each tuple in the relation. 
- The primary key attributes are underlined. 
- Choose as primary key the smallest of the candidate keys (in terms of size). 
- A primary key has two properties: It should be unique for all tuples and It can’t have NULL values.

2. Entity integrity constraints 
- Entity Integrity: The primary key attributes of each relation cannot have null values in any tuple of a relation. *(No attribute participating in the primary key is allowed to accept null values.)*
- Note: Other attributes of the relation may be similarly constrained to disallow null values, even though they are not members of the primary key. 

3. Referential integrity constraints 
*(These constraints are checked before performing any operation (insert, delete and update) in database. If there is a violation in any of constraints, operation will fail.)*


## **Row-Oriented DB**

* Stores data **row by row**.
* Best for **transactions (OLTP-Online transaction processing)**.
* **Fast for writes & updates**.
* Slower for analytics (must read all columns).
* Examples: **MySQL, PostgreSQL, Oracle**.

## **Column-Oriented DB**

* Stores data **column by column**.
* Best for **analytics (OLAP-Online Analytical Processing)**.
* **Fast for aggregations & queries** on few columns.
* Slower for frequent writes.
* Examples: **Redshift, BigQuery, ClickHouse**.

✅ **Rule of thumb:**

* **Row DB → good for many small transactions.**
* **Column DB → good for analyzing large datasets.**

**SQL Commands: DDL vs DML**
- DDL – Data Definition Language
- Defines structure of the database (schema).
- Commands:
          - CREATE → make new tables, databases
          - ALTER → change table (add/remove columns)
          - DROP → delete tables or databases
- DML – Data Manipulation Language
- Deals with the data inside the tables.
- Commands:
          - INSERT → add new records
          - UPDATE → modify existing records
          - DELETE → remove records
          - SELECT → query/retrieve data


---

**Basic Commands**

```sql
-- List all databases
SHOW DATABASES;

-- Select a database to use
USE practice_db;

-- Show tables in current database
SHOW TABLES;

---

---

**Database & Table Management**

-- Create a new database
CREATE DATABASE practice_db;

-- Use a database
USE practice_db;

-- Drop (delete) a database
DROP DATABASE practice_db;

-- Create a table
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  email VARCHAR(100),
  register_date DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- Show tables in the current database
SHOW TABLES;

-- Describe a table (structure)
DESCRIBE users;

-- Drop (delete) a table
DROP TABLE users;

---

---

**Data Manipulation (CRUD)**

-- Insert a row
INSERT INTO users (first_name, last_name, email)
VALUES ('Alice', 'Smith', 'alice@example.com');

-- Insert multiple rows
INSERT INTO users (first_name, last_name, email)
VALUES 
  ('Bob', 'Johnson', 'bob@example.com'),
  ('Charlie', 'Lee', 'charlie@example.com');

-- Select / read
SELECT * FROM users;
SELECT first_name, last_name FROM users WHERE email LIKE '%@example.com';

-- Update
UPDATE users
SET last_name = 'Brown'
WHERE first_name = 'Alice';

-- Delete
DELETE FROM users
WHERE first_name = 'Charlie';

---

---

**Joins & Subqueries**

-- Creating a second table
CREATE TABLE posts (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT,
  title VARCHAR(200),
  body TEXT,
  FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Inner Join example
SELECT u.first_name, u.last_name, p.title
FROM users u
JOIN posts p 
  ON u.id = p.user_id;

-- Subquery example
SELECT * FROM users 
WHERE id IN (SELECT user_id FROM posts WHERE title LIKE '%SQL%');

---

---

**Indexes, Alterations & Optimization**

-- Create index
CREATE INDEX idx_user_email ON users(email);

-- Drop index
DROP INDEX idx_user_email ON users;

-- Add a new column
ALTER TABLE users ADD age INT;

-- Modify a column
ALTER TABLE users MODIFY COLUMN age SMALLINT;

-- Analyze a query (explain plan)
EXPLAIN SELECT * FROM users WHERE email LIKE '%example%';

---

---

**Stored Procedures & Functions**

DELIMITER $$
CREATE PROCEDURE GetUsersByAge(IN min_age INT)
BEGIN
  SELECT first_name, last_name, age
  FROM users
  WHERE age >= min_age;
END $$
DELIMITER ;

-- Call procedure
CALL GetUsersByAge(25);

---
## Comments
-- This is a single-line comment
SHOW DATABASES;
# Another single-line comment
USE ecommerce_ai;
/* 
This is a multi-line comment
It can span several lines
*/
SHOW TABLES;
