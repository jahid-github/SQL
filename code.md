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
