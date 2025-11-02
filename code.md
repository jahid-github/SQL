# 🧩 SQL — DDL, DML, DQL, DCL, TCL

This session demonstrates the main SQL command categories with practical examples:  
**Data Definition (DDL), Data Manipulation (DML), Data Query (DQL), Data Control (DCL), and Transaction Control (TCL).**

---

## 🏗️ 1. Create Database and Schema

```sql
-- Create a new database
CREATE DATABASE TEST_DB;

-- Switch to the specific database
USE TEST_DB;

-- Create a table in the default schema (dbo)
CREATE TABLE Product(
    product_id INT,
    product_name VARCHAR(100)
);

-- Create a custom schema
CREATE SCHEMA test_schema;

---


## ⚙️ 2. DDL (Data Definition Language)


---

```sql
-- Create Table under test_schema
CREATE TABLE test_schema.Product(
    product_id INT,
    product_name VARCHAR(100),
    price DECIMAL
);

-- Alter Table: add a new column
ALTER TABLE test_schema.Product 
ADD quantity FLOAT;

-- Truncate Table: remove all rows/data
TRUNCATE TABLE test_schema.Product;

-- Drop Table: permanently remove the table
DROP TABLE test_schema.Product;


-- Select all records from Product table
SELECT * 
FROM test_schema.Product;


-- Insert full row data
INSERT INTO test_schema.Product 
VALUES (1, 'Book', 100, 5);

-- Insert data with selected columns
INSERT INTO test_schema.Product 
(product_id, product_name, quantity)
VALUES (2, 'Pen', 10);

-- Update specific record
UPDATE test_schema.Product  
SET price = 10.5 
WHERE product_id = 2;

-- Delete specific record
DELETE FROM test_schema.Product 
WHERE product_id = 2;

-- Grant access to a user
GRANT 
    SELECT, UPDATE 
ON Product TO user1;

-- Revoke access
REVOKE 
    UPDATE 
ON Product FROM user1;


-- COMMIT Example
UPDATE test_schema.Product  
SET price = 10.5 
WHERE product_id = 2;
COMMIT;

-- ROLLBACK Example
DELETE FROM test_schema.Product   
WHERE product_id = 2;
ROLLBACK;


-- Create destination table on the fly while inserting
SELECT *
INTO TEST_DB.test_schema.ProductAdvWDB2014
FROM AdventureWorks2014.Production.Product p 
WHERE p.StandardCost > 0;

-- Verify the data
SELECT *
FROM TEST_DB.test_schema.ProductAdvWDB2014
WHERE StandardCost > 0;

/*
INSERT INTO TEST_DB.test_schema.ProductAdvWDB2014
SELECT *
FROM AdventureWorks2014.Production.Product p
WHERE p.StandardCost = 0;
*/

-- Drop the destination table
DROP TABLE TEST_DB.test_schema.ProductAdvWDB2014;

-- Insert into an existing table from another
INSERT INTO TEST_DB.test_schema.Product_1
SELECT *
FROM TEST_DB.test_schema.Product
WHERE product_id > 1;

-- Display results
SELECT *
FROM TEST_DB.test_schema.Product_1;
