# MySQL Practice & Cheat Sheet

SQL is a programming language used to interect with relation databases.
It is used to perform CRUD operations: Create, Read, Update, and Delete.

---

## Basic Commands

```sql
-- List all databases
SHOW DATABASES;

-- Select a database to use
USE practice_db;

-- Show tables in current database
SHOW TABLES;

---

---

# Database & Table Management

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

# Data Manipulation (CRUD)
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

# Joins & Subqueries
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

# Indexes, Alterations & Optimization
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

# Stored Procedures & Functions
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

