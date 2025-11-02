# 🧩 SQL — DDL, DML, DQL, DCL, TCL

This session demonstrates the main SQL command categories with practical examples:  
**Data Definition (DDL), Data Manipulation (DML), Data Query (DQL), Data Control (DCL), and Transaction Control (TCL).**

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

-- # DDL (Data Definition Language)

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

-- # DQL (Data Query Language)

-- Select all records from Product table
SELECT * 
FROM test_schema.Product;

-- # DML (Data Manipulation Language)

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

-- # DCL (Data Control Language)

-- Grant access to a user
GRANT 
    SELECT, UPDATE 
ON Product TO user1;

-- Revoke access
REVOKE 
    UPDATE 
ON Product FROM user1;

-- # TCL (Transaction Control Language)

-- COMMIT Example
UPDATE test_schema.Product  
SET price = 10.5 
WHERE product_id = 2;
COMMIT;

-- ROLLBACK Example
DELETE FROM test_schema.Product   
WHERE product_id = 2;
ROLLBACK;

-- # Copying Data Between Databases (Scenario)

-- Create destination table on the fly while inserting
SELECT *
INTO TEST_DB.test_schema.ProductAdvWDB2014
FROM AdventureWorks2014.Production.Product p 
WHERE p.StandardCost > 0;

-- Verify the data
SELECT *
FROM TEST_DB.test_schema.ProductAdvWDB2014
WHERE StandardCost > 0;

-- # (Optional) Insert additional records where StandardCost = 0:

/*
INSERT INTO TEST_DB.test_schema.ProductAdvWDB2014
SELECT *
FROM AdventureWorks2014.Production.Product p
WHERE p.StandardCost = 0;
*/

-- # Drop the table if needed:

-- Drop the destination table
DROP TABLE TEST_DB.test_schema.ProductAdvWDB2014;

-- # Insert Data from One Table to Another

-- Insert into an existing table from another
INSERT INTO TEST_DB.test_schema.Product_1
SELECT *
FROM TEST_DB.test_schema.Product
WHERE product_id > 1;

-- Display results
SELECT *
FROM TEST_DB.test_schema.Product_1;
