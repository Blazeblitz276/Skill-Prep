# SQL prep

Q: Types of Queries in SQL?

A: There are 5 types of queries in SQL:

Data Definition Language (DDL) - `CREATE, ALTER, DROP, TRUNCATE, RENAME, COMMENT, EXPLAIN(for explaining query excution status)`, etc.

Data Manipulation Language (DML) -`SELECT, INSERT, UPDATE, DELETE, MERGE, CALL, EXPLAIN PLAN, LOCK TABLE`, etc.

Data Control Language (DCL) - `GRANT, REVOKE`, etc.

Transaction Control Language (TCL) - `COMMIT, ROLLBACK, SAVEPOINT, SET TRANSACTION`, etc.

Data Query Language (DQL) - `SELECT, JOIN, UNION, WHERE` etc.

Syntax:
```sql

CREATE TABLE [table_name] (
    [column_name] [datatype] [constraint],
    [column_name] [datatype] [constraint],
)

DROP [object type] [object name]

ALTER [object type] [object name] [action]
eg: ALTER TABLE table_name ADD column_name datatype

```

Data Manipulation operations : CRUD - create, read, update and delete data operations in a DBMS. These are done using `INSERT, SELECT, UPDATE, DELETE` operations.

```sql
INSERT INTO employees (employee_id, first_name, last_name, email, hire_date)
VALUES (1, 'John', 'Doe', 'john.doe@example.com', '2023-01-01');

SELECT employee_id, first_name, last_name, email
FROM employees
WHERE employee_id = 1;

UPDATE employees
SET email = 'john.newemail@example.com'
WHERE employee_id = 1;

DELETE FROM employees
WHERE employee_id = 1;
```

Data Control operations: These operations are used to control the access to the data in the database. These are done using GRANT and REVOKE operations.

`GRANT` privilidges include; `SELECT, INSERT, UPDATE, DELETE, REFERENCES, ALTER, INDEX, CREATE, DROP, GRANT OPTION, ALL PRIVILEGES`.
```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON employees TO  'john'@'localhost';

REVOKE SELECT, INSERT, UPDATE, DELETE ON employees FROM 'john'@'localhost';

GRANT ALL PRIVILEGES ON my_database.* TO 'alice'@'localhost' IDENTIFIED BY 'password123';

REVOKE ALL PRIVILEGES ON my_database.* FROM 'alice'@'localhost';
```

Transaction Control operations:  COMMIT, ROLLBACK, SAVEPOINT, SET TRANSACTION operations.

```sql

START TRANSACTION;
/*The COMMIT statement is used to permanently save all changes made during the current transaction.*/
INSERT INTO employees (employee_id, first_name, last_name, email, hire_date)
VALUES (1, 'John', 'Doe', 'john.doe@example.com', '2023-01-01');
COMMIT;

/*The ROLLBACK statement is used to undo all changes made during the current transaction.*/
INSERT INTO employees (employee_id, first_name, last_name, email, hire_date)
VALUES (2, 'Jane', 'Doe', 'jane.doe@example.com', '2023-01-01');
ROLLBACK;
```

Q: What is ACID property in SQL?

A: ACID stands for Atomicity, Consistency, Isolation, and Durability. These are the properties that guarantee that database transactions are processed reliably.

Illustrating all four ACID properties (Atomicity, Consistency, Isolation, and Durability) with a single coherent example using a banking application where we want to transfer money between two accounts.

Table Definitions:
```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    account_name VARCHAR(100),
    balance DECIMAL(10, 2) CHECK (balance >= 0) -- Ensure balance cannot be negative
);

CREATE TABLE transactions (
    transaction_id INT PRIMARY KEY AUTO_INCREMENT,
    account_id INT,
    amount DECIMAL(10, 2),
    transaction_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (account_id) REFERENCES accounts(account_id)
);
```

-   Atomicity: The transfer of money between two accounts should be an atomic operation, meaning it should either succeed completely or fail completely. If any part of the transaction fails, the entire transaction should be rolled back.

```sql
START TRANSACTION;

-- Debit from Account A
UPDATE accounts 
SET balance = balance - 100 
WHERE account_id = 1 AND balance >= 100;

-- Check if debit was successful
IF (ROW_COUNT() = 0) THEN
    ROLLBACK;
    SELECT 'Transaction failed: Insufficient funds in Account A';
ELSE
    -- Credit to Account B
    UPDATE accounts 
    SET balance = balance + 100 
    WHERE account_id = 2;
    
    -- Check if credit was successful
    IF (ROW_COUNT() = 1) THEN
        COMMIT;
        SELECT 'Transaction successful';
    ELSE
        ROLLBACK;
        SELECT 'Transaction failed: Unable to credit Account B';
    END IF;
END IF;
```

-   Consistency: The transfer of money should maintain the consistency of the database. This means that the database should be in a valid state before and after the transaction. Consistency ensures that the database transitions from one valid state to another, maintaining all predefined rules and constraints.

In this example, the balance of each account should not be negative. We have a CHECK constraint on the balance column to enforce this rule.
    - Balance Check Constraint: Ensures that no account balance becomes negative.
    - Foreign Key Constraint: Ensures all transactions reference valid accounts.

Isolation: The transfer of money between two accounts should be isolated from other transactions. This means that the transaction should be executed independently of other transactions and should not interfere with their results. It ensures that the concurrent transactions do not interfere with each other. This is typically handled by the database's isolation levels.

```sql
-- Setting isolation level to SERIALIZABLE to ensure highest isolation
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;

START TRANSACTION;

-- Debit from Account A
UPDATE accounts 
SET balance = balance - 100 
WHERE account_id = 1 AND balance >= 100;

-- Check if debit was successful
IF (ROW_COUNT() = 0) THEN
    ROLLBACK;
    SELECT 'Transaction failed: Insufficient funds in Account A';
ELSE
    -- Credit to Account B
    UPDATE accounts 
    SET balance = balance + 100 
    WHERE account_id = 2;
    
    -- Check if credit was successful
    IF (ROW_COUNT() = 1) THEN
        COMMIT;
        SELECT 'Transaction successful';
    ELSE
        ROLLBACK;
        SELECT 'Transaction failed: Unable to credit Account B';
    END IF;
END IF;
```
By setting the isolation level to SERIALIZABLE, we ensure that no other transactions can interfere with this transaction.

-  Durability: The transfer of money between two accounts should be durable, meaning that once the transaction is committed, the changes should persist even in the event of a system failure. This is typically achieved through mechanisms like write-ahead logging and database backups. Once the `COMMIT` statement is executed, all changes are saved permanently in the database. Even if the system crashes immediately after the commit, the changes will persist.

Q: What are Database isolation levels in SQL?

A: Database isolation levels define the degree to which one transaction must be isolated from the effects of other transactions. There are four standard isolation levels in SQL:

1. READ UNCOMMITTED: This is the lowest isolation level where transactions can read uncommitted changes made by other transactions. This level allows dirty reads, non-repeatable reads, and phantom reads.
```sql
-- Transaction 1
START TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;

-- Transaction 2
START TRANSACTION;
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
SELECT * FROM accounts WHERE account_id = 1;  -- Can see the uncommitted update by Transaction 1
```

2. READ COMMITTED: This isolation level ensures that a transaction can only read committed data from other transactions. It prevents dirty reads but allows non-repeatable reads and phantom reads.
```sql
-- Transaction 1
START TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;
COMMIT;

-- Transaction 2
START TRANSACTION;
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
SELECT * FROM accounts WHERE account_id = 1;  -- Cannot see the uncommitted update by Transaction 1
```

3. REPEATABLE READ: This isolation level ensures that a transaction can read the same data multiple times without changes from other transactions. It prevents dirty reads and non-repeatable reads but allows phantom reads.
```sql
-- Transaction 1
START TRANSACTION;
SELECT * FROM accounts WHERE account_id = 1;

-- Transaction 2
START TRANSACTION;
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
INSERT INTO accounts (account_id, account_name, balance) VALUES (3, 'Account C', 500);
COMMIT;

-- Transaction 1
SELECT * FROM accounts WHERE account_id = 1;  -- Can see the new row inserted by Transaction 2
```

4. SERIALIZABLE: This is the highest isolation level that ensures complete isolation between transactions. It prevents dirty reads, non-repeatable reads, and phantom reads by locking the data being read by a transaction until the transaction is completed.
```sql
-- Transaction 1
START TRANSACTION;
SELECT * FROM accounts WHERE account_id = 1;

-- Transaction 2
START TRANSACTION;
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
INSERT INTO accounts (account_id, account_name, balance) VALUES (3, 'Account C', 500);
COMMIT;

-- Transaction 1
SELECT * FROM accounts WHERE account_id = 1;  -- Cannot see the new row inserted by Transaction 2
```
Practical Usage
- Read Uncommitted: Used when performance is critical, and the application can tolerate dirty reads, such as in logging or monitoring systems.
- Read Committed: Commonly used as the default isolation level in many databases, balancing performance and data consistency.
- Repeatable Read: Used when applications require consistent reads within a transaction but can tolerate phantom reads.
- Serializable: Used when the highest level of data integrity is required, typically in financial applications or systems requiring strict consistency.

Q: Order of execution of SQL queries?

A: The order of execution of SQL queries is as follows:

1. `FROM`: The FROM clause specifies the tables from which the data will be retrieved.
2. `WHERE`: The WHERE clause filters the rows based on a specified condition.
3. `GROUP` BY: The GROUP BY clause groups the rows that have the same values into summary rows.
4. `HAVING`: The HAVING clause filters the groups based on a specified condition.
5. `SELECT`: The SELECT clause selects the columns that will be included in the result set.
6. `ORDER` BY: The ORDER BY clause sorts the result set by one or more columns.
7. `LIMIT`: The LIMIT clause limits the number of rows returned by the query.
8. `OFFSET`: The OFFSET clause specifies the number of rows to skip before starting to return rows.
9. `FETCH`: The FETCH clause is used to retrieve a specified number of rows from a result set.
10. `UNION`: The UNION clause combines the results of two or more SELECT statements into a single result set.
11. `JOIN`: The JOIN clause combines rows from two or more tables based on a related column between them.
12. `SUBQUERY`: The SUBQUERY clause is used to nest a query within another query.
13. `WINDOW` FUNCTION: The WINDOW FUNCTION clause is used to perform calculations across a set of rows related to the current row.
14. `COMMON` TABLE EXPRESSION: The COMMON TABLE EXPRESSION clause is used to define a temporary result set that can be referenced within a `SELECT, INSERT, UPDATE`, or `DELETE` statement.
15. `TRIGGER`: The TRIGGER clause is used to define a set of actions that are automatically performed when a specified event occurs.
16. `INDEX`: The INDEX clause is used to create an index on a table to improve the performance of SELECT, UPDATE, DELETE, and MERGE statements.
17. `VIEW`: The VIEW clause is used to create a virtual table based on the result set of a SELECT statement.
18. `STORED` PROCEDURE: The STORED PROCEDURE clause is used to define a set of SQL statements that can be executed as a single unit.
19. `FUNCTION`: The FUNCTION clause is used to define a set of SQL statements that can be executed as a single unit and return a value.



Q: What are the different types of SQL JOINS?

A: There are 6 types of SQL JOINS:

1. `INNER JOIN`: Returns records that have matching values in both tables.
2. `LEFT JOIN`: Returns all records from the left table and the matched records from the right table.
3. `RIGHT JOIN`: Returns all records from the right table and the matched records from the left table.
4. `FULL JOIN`: Returns all records when there is a match in either left or right table.
5. `SELF JOIN`: A self join is a regular join, but the table is joined with itself. This is useful for comparing values in a column with other values in the same column in the same table. 
6. `CROSS JOIN`: Returns the Cartesian product of the two tables. That is, it returns all possible combinations of rows from the two tables. It is useful when you want to combine every row from one table with every row from another table.

Q: What is NATURAL JOIN?

A: A NATURAL JOIN is a type of JOIN that automatically matches columns with the same name in both tables. It is a type of INNER JOIN that returns rows from both tables where the values in the matching columns are equal.

Q: What is an Equi Join?

A: An equi join is a type of join that combines rows from two tables based on a matching column between them. It is a type of INNER JOIN that uses the equality operator (=) to compare values in the specified columns. the difference between an equi join and a natural join is that an equi join requires you to specify the columns to join on, while a natural join automatically matches columns with the same name.

Q: Distinguish between nested subquery, correlated subquery, and join operation.

A: Nested subquery: A nested subquery is a subquery that is nested within another query. It is used to filter the results of the outer query based on the results of the inner query. The inner query is executed first, and its results are used to filter the results of the outer query.

```sql
SELECT column1, column2
FROM table1
WHERE column1 IN (SELECT column1 FROM table2 WHERE column2 = value);
```

Correlated subquery: A correlated subquery is a subquery that is executed once for each row processed by the outer query. It is used to filter the results of the outer query based on the results of the inner query. The inner query is executed for each row processed by the outer query.

```sql
SELECT column1, column2
FROM table1
WHERE column1 = (SELECT column1 FROM table2 WHERE column2 = table1.column2);
```

Join operation: A join operation is used to combine rows from two or more tables based on a related column between them. It is used to retrieve data from multiple tables in a single query. There are different types of join operations, such as INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL JOIN.

```sql
SELECT column1, column2
FROM table1
JOIN table2 ON table1.column1 = table2.column1;
```

Q: How are JOINS different from the UNION clause?

A: `JOIN` and `UNION` are used to combine data from multiple tables, but they are used in different ways. JOINS are used to combine rows from two or more tables based on a related column between them, while UNION is used to combine the results of two or more SELECT statements into a single result set. JOINS are used to retrieve data from multiple tables in a single query, while UNION is used to combine the results of multiple queries into a single result set. JOINS combine rows horizontally, while UNION combines rows vertically.

Q: What is the difference between `UNION` and `UNION ALL`?

A: `UNION` and `UNION ALL` are used to combine the results of two or more SELECT statements into a single result set, but they are used in different ways. `UNION` removes duplicate rows from the result set, while `UNION ALL` does not. This means that `UNION` returns only distinct rows, while `UNION ALL` returns all rows, including duplicates.

Q: What is the difference between `WHERE` and `HAVING` clause?

A: The `WHERE` clause is used to filter rows based on a specified condition, while the `HAVING` clause is used to filter groups based on a specified condition. The WHERE clause is used with the `SELECT, INSERT, UPDATE, and DELETE` statements to filter rows based on a specified condition. The `HAVING` clause is used with the SELECT statement to filter groups based on a specified condition. The `WHERE` clause is used before the `GROUP BY` clause, while the `HAVING` clause is used after the `GROUP BY` clause.

Q: What is the difference between `GROUP BY` and `ORDER BY` clause?

A: The `GROUP BY` clause is used to group rows that have the same values into summary rows, while the `ORDER BY` clause is used to sort the result set by one or more columns. The `GROUP BY` clause is used with the SELECT statement to group rows that have the same values into summary rows. The `ORDER BY` clause is used with the SELECT statement to sort the result set by one or more columns. The `GROUP BY` clause is used before the `ORDER BY` clause.

Q: Is it required that the JOIN condition be based on equality?

A: No, the JOIN condition does not have to be based on equality. The JOIN condition can be based on any condition that evaluates to true or false. We can use any of the common symbols such as <, <=, >, >=, !=, BETWEEN operators in the JOIN condition.
```sql
SELECT column1, column2
FROM table1
JOIN table2 ON table1.column1 > table2.column1;
```

Q: What is a HASH JOIN?

A: A `HASH JOIN` requires two inputs, an INNER table, and an OUTER table. `HASH JOINS` involve using a HASH table to identify matching rows between two tables. `HASH JOINS` are an option when other joins are not recommended. When joining large data sets that are unsorted or non-indexed `HASH JOINS` are better. `HASH JOINS` are faster than MERGE JOINS and LOOP JOINS. `HASH JOINS` are used when the tables are large and do not fit in memory. 

Q: What is a MERGE JOIN?

A: A MERGE JOIN is a join operation that combines two sorted data sets into a single result set. MERGE JOINS are used when the tables are already sorted on the join key. MERGE JOINS are faster than LOOP JOINS but slower than `HASH JOINS`. MERGE JOINS are used when the tables are small and fit in memory. 

```sql
SELECT column1, column2
FROM table1
JOIN table2 ON table1.column1 = table2.column1
ORDER BY column1;
```

Q: What is a LOOP JOIN?

A: A LOOP JOIN is a join operation that compares each row from the first table with each row from the second table to find matching rows. LOOP JOINS are the slowest of the three join types. LOOP JOINS are used when the tables are small and fit in memory. LOOP JOINS are used when the tables are not sorted on the join key.

Q: What is indexing in SQL?

A: Indexing in SQL is a technique used to improve the performance of SELECT, UPDATE, DELETE, and MERGE statements by creating an index on a table. An index is a data structure that stores the values of one or more columns in a table in a sorted order, allowing the database to quickly locate the rows that match a specified condition. Indexing can speed up the retrieval of data from a table by reducing the number of rows that need to be scanned. 

Q: What are the different types of indexes in SQL?

A: There are several types of indexes in SQL:

1. Single-column index: An index created on a single column in a table.
2. Composite index: An index created on multiple columns in a table.
3. Unique index: An index that enforces the uniqueness of values in one or more columns.
4. Clustered index: An index that stores the data rows in the table in the same order as the index.
5. Non-clustered index: An index that stores the data rows in the table in a separate location from the index.
6. Bitmap index: An index that stores the values of multiple columns in a single bitmap.
7. Function-based index: An index that is created based on the result of a function applied to one or more columns.
8. Spatial index: An index that is created on spatial data types to optimize spatial queries.

```sql
# Syntax for creating indexes in SQL

# Single-column index
CREATE INDEX index_name ON table_name (column1);

# Composite index
CREATE INDEX index_name ON table_name (column1, column2);

# Unique index
CREATE UNIQUE INDEX index_name ON table_name (column1, column2);

# Clustered index
CREATE CLUSTERED INDEX index_name ON table_name (column1, column2);

# Non-clustered index
CREATE NONCLUSTERED INDEX index_name ON table_name (column1, column2);

# Bitmap index
CREATE BITMAP INDEX index_name ON table_name (column1, column2);

# Function-based index
CREATE INDEX index_name ON table_name (UPPER(column1));

# Spatial index
CREATE SPATIAL INDEX index_name ON table_name (column1);

```

Q: Database Denormalization and its advantages?

A: Database denormalization is the process of optimizing a database by adding redundant data to one or more tables. This is done to improve the performance of SELECT, UPDATE, DELETE, and MERGE statements by reducing the number of joins required to retrieve data from the database. Denormalization can speed up the retrieval of data from a table by reducing the number of rows that need to be scanned. It can also reduce the complexity of the database schema and improve the readability of the SQL queries.

Advantages of database denormalization:
1. Improved performance: Denormalization can improve the performance of SELECT, UPDATE, DELETE, and MERGE statements by reducing the number of joins required to retrieve data from the database.
2. Reduced complexity: Denormalization can reduce the complexity of the database schema by adding redundant data to one or more tables.
3. Improved readability: Denormalization can improve the readability of the SQL queries by reducing the number of joins required to retrieve data from the database.

```sql
-- Normalized
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE
);

CREATE TABLE order_items (
    item_id INT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT,
    price DECIMAL(10, 2)
);

-- Denormalized
CREATE TABLE daily_sales_summary (
    sales_date DATE PRIMARY KEY,
    total_sales DECIMAL(10, 2),
    total_orders INT
);

-- Denormalized Cache for faster retrieval

CREATE TABLE product_cache (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category_name VARCHAR(100),
    inventory_count INT,
    price DECIMAL(10, 2)
);
```
Disadvantages of database denormalization:
1. Increased storage space: Denormalization can increase the storage space required to store redundant data in one or more tables.
2. Data redundancy: Denormalization can introduce data redundancy by storing the same data in multiple tables.
3. Data inconsistency: Denormalization can lead to data inconsistency by storing redundant data in one or more tables.
4. Complicated write operations: Denormalization can complicate write operations by requiring updates to redundant data in one or more tables.


Q: What are stored procedures in SQL?

A: Stored procedures in SQL are a set of SQL statements that are stored in the database and can be executed by calling the procedure name. Stored procedures can accept input parameters, return output parameters, and perform complex operations that involve multiple SQL statements. Stored procedures are used to encapsulate business logic, improve performance, and enhance security by preventing SQL injection attacks.

```sql
-- Syntax for creating a stored procedure in SQL

CREATE PROCEDURE procedure_name
    [ (parameter1 datatype, parameter2 datatype, ...) ]
AS
BEGIN
    SQL statements
END;
```
```sql

DELIMITER //

CREATE PROCEDURE GetEmployeeDetails(IN emp_id INT)
BEGIN
    SELECT * FROM employees WHERE employee_id = emp_id;
END //

DELIMITER ;
```

```sql
-- Calling a stored procedure in SQL

CALL procedure_name(parameter1, parameter2, ...);
```

```sql
-- Example of calling a stored procedure in SQL

CALL GetEmployeeDetails(1);
```

Q: What are triggers in SQL?

A: Triggers in SQL are special types of stored procedures that are automatically executed in response to certain events on a table. Triggers can be executed before or after `INSERT, UPDATE, DELETE`, and MERGE statements on a table. Triggers are used to enforce business rules, maintain data integrity, and perform complex operations that involve multiple SQL statements.

```sql
-- Syntax for creating a trigger in SQL

CREATE TRIGGER trigger_name
BEFORE | AFTER INSERT | UPDATE | DELETE | MERGE
ON table_name
FOR EACH ROW
BEGIN
    SQL statements
END;
```

```sql
-- Example of a trigger in SQL

DELIMITER //

CREATE TRIGGER UpdateEmployeeSalary

BEFORE UPDATE OF salary ON employees

FOR EACH ROW
BEGIN
    IF NEW.salary > OLD.salary THEN
        INSERT INTO salary_history (employee_id, old_salary, new_salary, change_date)
        VALUES (NEW.employee_id, OLD.salary, NEW.salary, NOW());
    END IF;
END //

DELIMITER ;
```

Q: What is a view in SQL?

A: A view in SQL is a virtual table that is based on the result set of a SELECT statement. Views are used to simplify complex queries, hide the complexity of the database schema, and provide a layer of security by restricting access to certain columns or rows. Views can be used to retrieve data from multiple tables in a single query, and they can be updated like regular tables.

```sql
-- Syntax for creating a view in SQL

CREATE VIEW view_name AS
SELECT column1, column2
FROM table_name
WHERE condition;
```

```sql
-- Example of a view in SQL

CREATE VIEW employee_details AS
SELECT employee_id, first_name, last_name, email
FROM employees
WHERE department_id = 10;
```

Q: What is a Common Table Expression (CTE) in SQL?

A: A Common Table Expression (CTE) in SQL is a temporary result set that can be referenced within a `SELECT, INSERT, UPDATE`, or `DELETE` statement. CTEs are used to simplify complex queries, improve readability, and provide a layer of abstraction by breaking down a query into smaller, more manageable parts. CTEs are defined using the WITH clause and can be referenced multiple times within a query. They can only be used within the scope of the query in which they are defined.

```sql
-- Syntax for creating a CTE in SQL

WITH cte_name AS (
    SELECT column1, column2
    FROM table_name
    WHERE condition
)
SELECT column1, column2
FROM cte_name;
```

```sql
-- Example of a CTE in SQL

WITH employee_details AS (
    SELECT employee_id, first_name, last_name, email
    FROM employees
    WHERE department_id = 10
)


SELECT employee_id, first_name, last_name, email
FROM employee_details;
```

Q: How to create functions in SQL?

A: Functions in SQL are a set of SQL statements that can accept input parameters, perform calculations, and return a single value. Functions can be used to encapsulate business logic, improve performance, and enhance security by preventing SQL injection attacks. There are two types of functions in SQL: scalar functions and table-valued functions.

```sql
-- Syntax for creating a scalar function in SQL

CREATE FUNCTION function_name (parameter1 datatype, parameter2 datatype, ...)
RETURNS return_datatype
FUNCTION_ATTRIBUTES
AS
BEGIN
    SQL statements
    RETURN return_value;
END;
```

```sql
-- Example of a scalar function in SQL

CREATE FUNCTION calculate_salary_bonus (salary DECIMAL(10, 2))
RETURNS DECIMAL(10, 2)
DETERMINISTIC
BEGIN
    DECLARE bonus DECIMAL(10, 2);
    SET bonus = salary * 0.1;
    RETURN bonus;
END;
```

```sql
-- Syntax for creating a table-valued function in SQL

CREATE FUNCTION function_name (parameter1 datatype, parameter2 datatype, ...)
RETURNS TABLE
FUNCTION_ATTRIBUTES
AS
RETURN
    SELECT column1, column2
    FROM table_name
    WHERE condition;
```

Q: WHat the the most used Window functions in SQL?

A: Window functions in SQL are used to perform calculations across a set of rows related to the current row. Some of the most commonly used window functions in SQL are:

1. `ROW_NUMBER()`: Assigns a unique sequential integer to each row in the result set.
2. `RANK()`: Assigns a unique rank to each row in the result set, with gaps in the ranking if there are ties.
3. `DENSE_RANK()`: Assigns a unique rank to each row in the result set, without gaps in the ranking if there are ties.
4. `NTILE()`: Divides the result set into a specified number of groups and assigns a group number to each row.
5. `LEAD()`: Returns the value of a specified column from the next row in the result set.
6. `LAG()`: Returns the value of a specified column from the previous row in the result set.
7. `FIRST_VALUE()`: Returns the first value of a specified column in the result set.
8. `LAST_VALUE()`: Returns the last value of a specified column in the result set.
9. `SUM() OVER()`: Calculates the sum of a specified column across a set of rows related to the current row.
10. `AVG() OVER()`: Calculates the average of a specified column across a set of rows related to the current row.
11. `MAX() OVER()`: Calculates the maximum value of a specified column across a set of rows related to the current row.
12. `MIN() OVER()`: Calculates the minimum value of a specified column across a set of rows related to the current row.

```sql
-- Example of using a window function in SQL

SELECT employee_id, first_name, last_name, salary,
       ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_number,
       RANK() OVER (ORDER BY salary DESC) AS rank,
       DENSE_RANK() OVER (ORDER BY salary DESC) AS dense_rank
FROM employees;
```


Q: What are clusters in SQL?

A: Clusters in SQL are used to group rows that have the same values in one or more columns. Clusters are used to organize data in a table based on the values of one or more columns. Clusters can improve the performance of SELECT, UPDATE, DELETE, and MERGE statements by reducing the number of rows that need to be scanned. Clusters can also improve the readability of the SQL queries by grouping related rows together.

```sql
-- Syntax for creating a cluster in SQL

CREATE CLUSTER cluster_name
ON table_name (column1, column2, ...);
```

```sql
-- Example of creating a cluster in SQL

CREATE CLUSTER employee_cluster
ON employees (department_id, job_id);
```

Q: What is partitioning in SQL?

A: Partitioning in SQL is a technique used to divide a large table into smaller, more manageable parts called partitions. Partitioning can improve the performance of SELECT, UPDATE, DELETE, and MERGE statements by reducing the number of rows that need to be scanned. Partitioning can also improve the manageability of the database by allowing data to be stored in separate partitions based on a specified condition. There are several types of partitioning in SQL, such as range partitioning, list partitioning, hash partitioning, and composite partitioning. Partitioning can be done based on a single column or multiple columns. 

```sql
-- Syntax for creating a partition in SQL

CREATE TABLE table_name
(
    column1 datatype,
    column2 datatype,
    ...
)
PARTITION BY RANGE (column1)
(
    PARTITION partition_name1 VALUES LESS THAN (value1),
    PARTITION partition_name2 VALUES LESS THAN (value2),
    ...
);
```

```sql
-- Example of creating a partition in SQL

CREATE TABLE employees
(
    employee_id INT,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    hire_date DATE
)
PARTITION BY RANGE (YEAR(hire_date))
(
    PARTITION p0 VALUES LESS THAN (1990),
    PARTITION p1 VALUES LESS THAN (2000),
    PARTITION p2 VALUES LESS THAN (2010),
    PARTITION p3 VALUES LESS THAN (2020)
);
```

Q: What is a database Deadlock?

A: A database deadlock is a situation in which two or more transactions are waiting for each other to release locks on resources that the other transaction needs. Deadlocks can occur when two transactions are trying to update the same rows in a table in a different order. Deadlocks can cause transactions to hang indefinitely, leading to performance issues and data inconsistency. Deadlocks can be prevented by using proper indexing, minimizing the duration of transactions, and using lock escalation techniques.

Q: What is Database Denormalization and the forms of denormalization?

A: Database denormalization is the process of optimizing a database by adding redundant data to one or more tables. This is done to improve the performance of SELECT, UPDATE, DELETE, and MERGE statements by reducing the number of joins required to retrieve data from the database. Denormalization can speed up the retrieval of data from a table by reducing the number of rows that need to be scanned. It can also reduce the complexity of the database schema and improve the readability of the SQL queries.

Forms of denormalization:
1. Horizontal denormalization: Horizontal denormalization involves splitting a table into multiple tables based on rows. This is done to reduce the number of rows in a table and improve the performance of SELECT, UPDATE, DELETE, and MERGE statements.
2. Vertical denormalization: Vertical denormalization involves splitting a table into multiple tables based on columns. This is done to reduce the number of columns in a table and improve the performance of SELECT, UPDATE, DELETE, and MERGE statements.
3. Star schema denormalization: Star schema denormalization involves denormalizing a star schema by adding redundant data to one or more tables. This is done to improve the performance of SELECT, UPDATE, DELETE, and MERGE statements by reducing the number of joins required to retrieve data from the database.

Q: What are database Normalization and the forms of normalization?

A: Database normalization is the process of organizing a database into tables and columns to reduce redundancy and improve data integrity. Normalization involves dividing a database into multiple tables and defining relationships between the tables. There are several normal forms in database normalization, such as First Normal Form (1NF), Second Normal Form (2NF), Third Normal Form (3NF), Boyce-Codd Normal Form (BCNF), and Fourth Normal Form (4NF).

Forms of normalization:
1. First Normal Form (1NF): A table is in 1NF if it has a primary key and all columns are atomic (i.e., each column contains a single value).
2. Second Normal Form (2NF): A table is in 2NF if it is in 1NF and all non-key columns are fully functionally dependent on the primary key.
3. Third Normal Form (3NF): A table is in 3NF if it is in 2NF and all non-key columns are transitively dependent on the primary key.
4. Boyce-Codd Normal Form (BCNF): A table is in BCNF if it is in 3NF and every determinant is a candidate key.
5. Fourth Normal Form (4NF): A table is in 4NF if it is in BCNF and has no multi-valued dependencies.

```sql
-- Example of creating a table in 1NF

CREATE TABLE employees
(
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(100)
);
```

```sql
-- Example of creating a table in 2NF

CREATE TABLE orders
(
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    total_amount DECIMAL(10, 2)
);
```
Here, the total_amount column is fully functionally dependent on the primary key (order_id) because it is dependent on the order_id and not on the customer_id or order_date.

```sql
-- Example of creating a table in 3NF

CREATE TABLE products
(
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category_id INT,
    category_name VARCHAR(100)
);
```
Here, the category_name column is transitively dependent on the primary key (product_id) through the category_id column. To normalize the table to 3NF, we can create a separate categories table with the category_id and category_name columns. 

```sql
-- Example of creating a table in BCNF

CREATE TABLE employees
(
    employee_id INT PRIMARY KEY,
    department_id INT,
    department_name VARCHAR(100)
);
```
Here, the department_name column is dependent on the department_id column, which is a candidate key. To normalize the table to BCNF, we can create a separate departments table with the department_id and department_name columns.

```sql
-- Example of creating a table in 4NF

CREATE TABLE employees
(
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(100),
    phone_numbers VARCHAR(100)
);
```
Here, the phone_numbers column contains multi-valued dependencies because it can contain multiple phone numbers for each employee. To normalize the table to 4NF, we can create a separate phone_numbers table with the employee_id and phone_number columns. 

Q: What is the difference between a primary key, a unique key, Candidate key, and a foreign key?

A: Primary key: A primary key is a column or a set of columns that uniquely identifies each row in a table. A primary key must be unique, not null, and have a unique constraint. A table can have only one primary key.

Unique key: A unique key is a column or a set of columns that uniquely identifies each row in a table. A unique key must be unique, but it can contain null values. A table can have multiple unique keys.