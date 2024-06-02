# SQL prep

Q: What is SQL JOINS?

A: The SQL JOIN component joins rows from one or more tables in a relational database. Create sets that can be stored in tabular form or used routinely. JOIN is to combine columns from one table or multiple tables using the same value.

Q: Types of Queries in SQL?

A: There are 5 types of queries in SQL:

Data Definition Language (DDL) - `CREATE, ALTER, DROP, TRUNCATE, RENAME, COMMENT`, etc.

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

`GRANT` privilidges include; SELECT, INSERT, UPDATE, DELETE, REFERENCES, ALTER, INDEX, CREATE, DROP, GRANT OPTION, ALL PRIVILEGES.
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

-  Durability: The transfer of money between two accounts should be durable, meaning that once the transaction is committed, the changes should persist even in the event of a system failure. This is typically achieved through mechanisms like write-ahead logging and database backups. Once the COMMIT statement is executed, all changes are saved permanently in the database. Even if the system crashes immediately after the commit, the changes will persist.

Q: Order of execution of SQL queries?

A: The order of execution of SQL queries is as follows:

1. FROM: The FROM clause specifies the tables from which the data will be retrieved.
2. WHERE: The WHERE clause filters the rows based on a specified condition.
3. GROUP BY: The GROUP BY clause groups the rows that have the same values into summary rows.
4. HAVING: The HAVING clause filters the groups based on a specified condition.
5. SELECT: The SELECT clause selects the columns that will be included in the result set.
6. ORDER BY: The ORDER BY clause sorts the result set by one or more columns.
7. LIMIT: The LIMIT clause limits the number of rows returned by the query.
8. OFFSET: The OFFSET clause specifies the number of rows to skip before starting to return rows.
9. FETCH: The FETCH clause is used to retrieve a specified number of rows from a result set.
10. UNION: The UNION clause combines the results of two or more SELECT statements into a single result set.
11. JOIN: The JOIN clause combines rows from two or more tables based on a related column between them.
12. SUBQUERY: The SUBQUERY clause is used to nest a query within another query.
13. WINDOW FUNCTION: The WINDOW FUNCTION clause is used to perform calculations across a set of rows related to the current row.
14. COMMON TABLE EXPRESSION: The COMMON TABLE EXPRESSION clause is used to define a temporary result set that can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement.
15. TRIGGER: The TRIGGER clause is used to define a set of actions that are automatically performed when a specified event occurs.
16. INDEX: The INDEX clause is used to create an index on a table to improve the performance of SELECT, UPDATE, DELETE, and MERGE statements.
17. VIEW: The VIEW clause is used to create a virtual table based on the result set of a SELECT statement.
18. STORED PROCEDURE: The STORED PROCEDURE clause is used to define a set of SQL statements that can be executed as a single unit.
19. FUNCTION: The FUNCTION clause is used to define a set of SQL statements that can be executed as a single unit and return a value.



Q: What are the different types of SQL JOINS?

A: There are 6 types of SQL JOINS:

1. INNER JOIN: Returns records that have matching values in both tables.
2. LEFT JOIN: Returns all records from the left table and the matched records from the right table.
3. RIGHT JOIN: Returns all records from the right table and the matched records from the left table.
4. FULL JOIN: Returns all records when there is a match in either left or right table.
5. SELF JOIN: A self join is a regular join, but the table is joined with itself. This is useful for comparing values in a column with other values in the same column in the same table. 
6. CROSS JOIN: Returns the Cartesian product of the two tables. That is, it returns all possible combinations of rows from the two tables. It is useful when you want to combine every row from one table with every row from another table.

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

A: JOINS and UNION are used to combine data from multiple tables, but they are used in different ways. JOINS are used to combine rows from two or more tables based on a related column between them, while UNION is used to combine the results of two or more SELECT statements into a single result set. JOINS are used to retrieve data from multiple tables in a single query, while UNION is used to combine the results of multiple queries into a single result set. JOINS combine rows horizontally, while UNION combines rows vertically.

Q: What is the difference between UNION and UNION ALL?

A: UNION and UNION ALL are used to combine the results of two or more SELECT statements into a single result set, but they are used in different ways. UNION removes duplicate rows from the result set, while UNION ALL does not. This means that UNION returns only distinct rows, while UNION ALL returns all rows, including duplicates.

Q: What is the difference between WHERE and HAVING clause?

A: The WHERE clause is used to filter rows based on a specified condition, while the HAVING clause is used to filter groups based on a specified condition. The WHERE clause is used with the SELECT, INSERT, UPDATE, and DELETE statements to filter rows based on a specified condition. The HAVING clause is used with the SELECT statement to filter groups based on a specified condition. The WHERE clause is used before the GROUP BY clause, while the HAVING clause is used after the GROUP BY clause.

Q: What is the difference between GROUP BY and ORDER BY clause?

A: The GROUP BY clause is used to group rows that have the same values into summary rows, while the ORDER BY clause is used to sort the result set by one or more columns. The GROUP BY clause is used with the SELECT statement to group rows that have the same values into summary rows. The ORDER BY clause is used with the SELECT statement to sort the result set by one or more columns. The GROUP BY clause is used before the ORDER BY clause.

Q: Is it required that the JOIN condition be based on equality?

A: No, the JOIN condition does not have to be based on equality. The JOIN condition can be based on any condition that evaluates to true or false. We can use any of the common symbols such as <, <=, >, >=, !=, BETWEEN operators in the JOIN condition.
```sql
SELECT column1, column2
FROM table1
JOIN table2 ON table1.column1 > table2.column1;
```

Q: What is a HASH JOIN?

A: A HASH JOIN requires two inputs, an INNER table, and an OUTER table. HASH JOINS involve using a HASH table to identify matching rows between two tables. HASH JOINS are an option when other joins are not recommended. When joining large data sets that are unsorted or non-indexed HASH JOINS are better. HASH JOINS are faster than MERGE JOINS and LOOP JOINS. HASH JOINS are used when the tables are large and do not fit in memory. 

Q: What is a MERGE JOIN?

A: A MERGE JOIN is a join operation that combines two sorted data sets into a single result set. MERGE JOINS are used when the tables are already sorted on the join key. MERGE JOINS are faster than LOOP JOINS but slower than HASH JOINS. MERGE JOINS are used when the tables are small and fit in memory. 

```sql
SELECT column1, column2
FROM table1
JOIN table2 ON table1.column1 = table2.column1
ORDER BY column1;
```

Q: What is a LOOP JOIN?

A: A LOOP JOIN is a join operation that compares each row from the first table with each row from the second table to find matching rows. LOOP JOINS are the slowest of the three join types. LOOP JOINS are used when the tables are small and fit in memory. LOOP JOINS are used when the tables are not sorted on the join key.
