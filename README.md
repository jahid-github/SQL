# MySQl
# MySQL Practice & Cheat Sheet


SQL is a programming language used to interect with relation databases.
It is used to perform CRUD operations: Create, Read, Update, and Delete.


This repository contains SQL scripts, examples, and practice exercises for MySQL.  
It follows the MySQL Cheat Sheet by Brad Traversy. :contentReference[oaicite:1]{index=1}  

---

## 💡 Table of Contents

1. [Setup / Installation](#setup)
2. [Basic Commands](#basic-commands)
3. [Database & Table Management](#database--table-management)
4. [Data Manipulation (CRUD)](#data-manipulation-crud)
5. [Joins & Subqueries](#joins--subqueries)
6. [Indexes, Alterations & Optimization](#indexes-alterations--optimization)
7. [Stored Procedures & Functions](#stored-procedures--functions)
8. [Examples](#examples)
9. [How to Run Locally](#how-to-run-locally)
10. [License / Credits](#license--credits)

---

## ✅ Setup / Installation

Make sure you have:
- MySQL Server installed and running
- MySQL Workbench (optional but helpful)
- MySQL user credentials (e.g., `root`)
- (Optional) Python + MySQL connector for integration with Jupyter

---

## 🔰 Basic Commands

```sql
-- List all databases
SHOW DATABASES;

-- Select a database to use
USE practice_db;

-- Show tables in current database
SHOW TABLES;

## Database & Table Management

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

## Data Manipulation (CRUD)
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

## Joins & Subqueries
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

## Indexes, Alterations & Optimization
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

## Stored Procedures & Functions
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
