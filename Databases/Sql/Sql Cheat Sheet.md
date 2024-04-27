### **Basic SQL Syntax**

- **Selecting Data**
  ```sql
  SELECT column1, column2 FROM table_name;
  ```
  Use to specify the columns you want to retrieve from a particular table.

- **Selecting All Columns**
  ```sql
  SELECT * FROM table_name;
  ```
  Retrieves all columns from the specified table.

- **Selecting with Conditions**
  ```sql
  SELECT column1, column2 FROM table_name WHERE condition;
  ```
  Retrieves data that meet the specified conditions.

- **Unique Rows**
  ```sql
  SELECT DISTINCT column1 FROM table_name;
  ```
  Returns only distinct (different) values in the specified column.

- **Counting Rows**
  ```sql
  SELECT COUNT(*) FROM table_name;
  ```
  Counts the number of rows in a table.

- **Limiting Results**
  ```sql
  SELECT * FROM table_name LIMIT number;
  ```
  Limits the number of results returned (useful in large datasets).

- **Sorting Results**
  ```sql
  SELECT column1 FROM table_name ORDER BY column1 ASC|DESC;
  ```
  Sorts the results by a specified column in ascending or descending order.

### **Filtering**

- **Using AND, OR, NOT**
  ```sql
  SELECT * FROM table_name WHERE condition1 AND|OR condition2;
  SELECT * FROM table_name WHERE NOT condition;
  ```
  Combines multiple conditions; AND requires both to be true, OR requires at least one to be true, NOT negates a condition.

- **Between**
  ```sql
  SELECT * FROM table_name WHERE column BETWEEN value1 AND value2;
  ```
  Retrieves rows where column values fall within a specified range.

- **Like (Pattern Matching)**
  ```sql
  SELECT * FROM table_name WHERE column LIKE pattern;
  -- Example: '%abc%' (Contains), 'abc%' (Starts with), '%abc' (Ends with)
  ```
  Used for matching a column value against a specified pattern. Percent signs (`%`) denote wildcard characters.

- **In**
  ```sql
  SELECT * FROM table_name WHERE column IN (value1, value2, ...);
  ```
  Returns rows where the column value matches any value in the list.

### **Joins**

- **Inner Join**
  ```sql
  SELECT * FROM table1 INNER JOIN table2 ON table1.common_column = table2.common_column;
  ```
  Returns rows when there is a match in both tables.

- **Left Join**
  ```sql
  SELECT * FROM table1 LEFT JOIN table2 ON table1.common_column = table2.common_column;
  ```
  Returns all rows from the left table and matched rows from the right table; if no match, returns NULL on the side of the right table.

- **Right Join**
  ```sql
  SELECT * FROM table1 RIGHT JOIN table2 ON table1.common_column = table2.common_column;
  ```
  Returns all rows from the right table and matched rows from the left table; if no match, returns NULL on the side of the left table.

- **Full Outer Join**
  ```sql
  SELECT * FROM table1 FULL OUTER JOIN table2 ON table1.common_column = table2.common_column;
  ```
  Returns all rows when there is a match in one of the tables.

- **Cross Join**
  ```sql
  SELECT * FROM table1 CROSS JOIN table2;
  ```
  Produces the Cartesian product of the two tables, combining each row of the first table with each row of the second table.

### **Aggregation Functions**

- **Count, Sum, Average, Min, Max**
  ```sql
  SELECT COUNT(column_name) FROM table_name;
  SELECT AVG(column_name) FROM table_name;
  SELECT SUM(column_name) FROM table_name;
  SELECT MIN(column_name) FROM table_name;
  SELECT MAX(column_name) FROM table_name;
  ```
  Performs calculations on a column to determine count, average, sum, minimum, and maximum values.

- **Group By**
  ```sql
  SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name;
  ```
  Groups rows that have the same values in specified columns into summary rows.

- **Having (Filter on Aggregates)**
  ```sql
  SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name HAVING COUNT(*) > value;
  ```
  Adds a condition to the `GROUP BY` clause, filtering the groups based on the condition.

### **Subqueries**

- **Subquery in WHERE**
  ```sql
  SELECT * FROM table_name WHERE column_name IN (SELECT column_name FROM table_name WHERE condition);
  ```
  Uses a subquery (aquery inside another query) to specify which rows from the outer query are to be returned, based on the conditions met by the inner query.

### **Data Manipulation**

- **Inserting Data**
  ```sql
  INSERT INTO table_name (column1, column2) VALUES (value1, value2);
  ```
  Adds new rows to a table with specified values.

- **Updating Data**
  ```sql
  UPDATE table_name SET column1 = value1 WHERE condition;
  ```
  Modifies existing data within a table based on the specified condition.

- **Deleting Data**
  ```sql
  DELETE FROM table_name WHERE condition;
  ```
  Removes existing records from a table where the conditions are met.

### **Database and Table Schema**

- **Creating Table**
  ```sql
  CREATE TABLE table_name (
      column1 datatype constraints,
      column2 datatype constraints,
      ...
  );
  ```
  Defines a new table and its columns in the database with specified data types and constraints (like `NOT NULL`, `PRIMARY KEY`).

- **Altering Table**
  ```sql
  ALTER TABLE table_name ADD|DROP|MODIFY column_name datatype;
  ```
  Modifies an existing table structure, such as adding, deleting, or modifying columns.

- **Dropping Table**
  ```sql
  DROP TABLE table_name;
  ```
  Deletes a table and all its data permanently from the database.

### **Transactions**

- **Basic Transaction Control**
  ```sql
  BEGIN TRANSACTION;
  COMMIT;
  ROLLBACK;
  ```
  Manages the transactions to ensure data integrity. `BEGIN TRANSACTION` starts a new transaction, `COMMIT` saves the changes, and `ROLLBACK` undoes them if an error occurs.

### Advanced Concepts

- **Indexes**
  ```sql
  CREATE INDEX index_name ON table_name (column_name);
  ```
  Enhances the speed of data retrieval operations by creating a physical storage structure which holds the indexed data.

- **Views**
  ```sql
  CREATE VIEW view_name AS
  SELECT column1, column2 FROM table_name WHERE condition;
  ```
  Creates a virtual table based on the result-set of a SQL statement. Views are used to simplify complex queries, enhance security, and manage data access.

- **Triggers**
  ```sql
  CREATE TRIGGER trigger_name
  BEFORE|AFTER INSERT|UPDATE|DELETE
  ON table_name FOR EACH ROW
  EXECUTE PROCEDURE function_name(arguments);
  ```
  Defines a set of actions that are automatically executed in response to specific changes on a particular table, such as insertions, updates, or deletions.

- **Stored Procedures**
  ```sql
  CREATE PROCEDURE procedure_name
  AS
  SQL_statement
  GO;
  ```
  A stored procedure is a prepared SQL code that you can save and reuse. It can perform complex operations, return values, and can be parameterized.

- **Foreign Keys**
  ```sql
  ALTER TABLE child_table ADD CONSTRAINT fk_name
  FOREIGN KEY (child_column) REFERENCES parent_table(parent_column);
  ```
  Enforces a link between the data in two tables to control the data that can be stored in the foreign key table.

- **Normalization**
  - Explains the process of structuring a relational database in accordance with a series of so-called normal forms in order to reduce data redundancy and improve data integrity.

- **ACID Properties**
  - Stands for Atomicity, Consistency, Isolation, and Durability. These properties ensure that database transactions are processed reliably and guarantee the validity of the data even in case of errors, power failures, and other mishaps.

### **Performance Optimization**

- **Query Performance Tips**
  - Use indexes to speed up searches on columns that are frequently searched or used as join keys.
  - Optimize query logic; avoid unnecessary columns in SELECT statements.
  - Use `EXPLAIN PLAN` to understand and optimize the execution plan for complex queries.

### **Security**

- **SQL Injection**
  ```sql
  -- Avoid constructing SQL directly using user input:
  SELECT * FROM users WHERE username = '${input}';
  -- Use parameterized queries instead
  ```
  Discusses how SQL injection exploits can be prevented by avoiding direct inclusion of user input in SQL statements and using parameterized queries or prepared statements instead.