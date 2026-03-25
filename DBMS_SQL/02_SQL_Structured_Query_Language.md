# 🔶 PART 2: SQL (Structured Query Language)
### The Complete Practical Guide | Queries, Joins, Triggers & Window Functions 🚀

---

## 📌 TABLE OF CONTENTS
1. [Types of SQL Commands (DDL, DML, DQL, DCL, TCL)](#1-types-of-sql-commands)
2. [Basic SQL Queries (`SELECT`, `WHERE`, `ORDER BY`, `DISTINCT`)](#2-basic-sql-queries)
3. [Filtering & Conditions (`AND/OR`, `BETWEEN`, `IN`, `LIKE`)](#3-filtering--conditions)
4. [Aggregate Functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`)](#4-aggregate-functions)
5. [GROUP BY & HAVING](#5-group-by--having)
6. [Joins (VERY IMPORTANT)](#6-joins-very-important)
7. [Subqueries (Nested & Correlated)](#7-subqueries)
8. [Constraints (`NOT NULL`, `UNIQUE`, `PK`, `FK`, `CHECK`)](#8-constraints)
9. [Views (Virtual Tables)](#9-views)
10. [Indexes in SQL](#10-indexes-in-sql)
11. [Stored Procedures & Functions](#11-stored-procedures--functions)
12. [Triggers](#12-triggers)
13. [Set Operations (`UNION`, `INTERSECT`, `MINUS`)](#13-set-operations)
14. [Window Functions (ADVANCED 🔥)](#14-window-functions-advanced-)

---

## 1. Types of SQL Commands

*   **DDL (Data Definition Language):** Defines structure. Auto-commits!
    *   `CREATE TABLE Users (id INT);`
    *   `ALTER TABLE Users ADD age INT;`
    *   `DROP TABLE Users;` (Deletes table and structure entirely).
    *   `TRUNCATE TABLE Users;` (Deletes all rows instantly, keeps the empty table structure).
*   **DML (Data Manipulation Language):** Manipulates data inside tables. Does NOT auto-commit.
    *   `INSERT INTO Users VALUES (1, 20);`
    *   `UPDATE Users SET age = 21 WHERE id = 1;`
    *   `DELETE FROM Users WHERE id = 1;`
*   **DQL (Data Query Language):** Getting data out.
    *   `SELECT * FROM Users;` (Most Important Command).
*   **DCL (Data Control Language):** Admin security.
    *   `GRANT SELECT ON Users TO 'Arjun';`
    *   `REVOKE UPDATE ON Users FROM 'Arjun';`
*   **TCL (Transaction Control Language):** Managing saving/undoing of DML statements.
    *   `COMMIT;` (Save changes permanently).
    *   `ROLLBACK;` (Undo changes since last commit).
    *   `SAVEPOINT A;` (Create a rollback checkpoint).

---

## 2. Basic SQL Queries

```sql
-- 1. Get everything
SELECT * FROM Employees;

-- 2. Filter rows
SELECT Name FROM Employees WHERE Salary > 50000;

-- 3. Sort Results (ASC is default, DESC is descending)
SELECT * FROM Employees ORDER BY Salary DESC;

-- 4. Remove Duplicates (Find all unique departments)
SELECT DISTINCT Department FROM Employees;
```

---

## 3. Filtering & Conditions

*   **AND, OR, NOT:** Connect multiple conditions.
    ```sql
    ... WHERE Dept = 'IT' AND Salary > 60000;
    ... WHERE NOT Dept = 'HR';
    ```
*   **BETWEEN:** Range (Inclusive of both start and end numbers).
    ```sql
    ... WHERE Age BETWEEN 25 AND 35;
    ```
*   **IN:** Matches multiple specific values (Saves you from writing 10 ORs).
    ```sql
    ... WHERE City IN ('Mumbai', 'Delhi', 'Chennai');
    ```
*   **LIKE (Pattern Matching):**
    *   `%` = Zero or more characters.
    *   `_` = Exactly ONE character.
    ```sql
    ... WHERE Name LIKE 'A%';   -- Starts with A
    ... WHERE Name LIKE '%a';   -- Ends with a
    ... WHERE Name LIKE '_rjun'; -- Second letter is 'r'
    ```
*   **IS NULL:** Checks if a field is completely blank. (You cannot use `= NULL`).
    ```sql
    ... WHERE Bonus IS NULL;
    ```

---

## 4. Aggregate Functions

Performs math on a whole column and returns ONE single number.

```sql
SELECT COUNT(EmpID) FROM Employees; -- How many employees?
SELECT SUM(Salary) FROM Employees;  -- Total payroll cost
SELECT AVG(Salary) FROM Employees;  -- Average pay
SELECT MIN(Salary) FROM Employees;  -- Lowest pay
SELECT MAX(Salary) FROM Employees;  -- Highest pay
```

---

## 5. GROUP BY & HAVING

Use `GROUP BY` to bundle rows with the exact same values into summary rows. Almost always used with aggregate functions!
*   **`HAVING` is just the `WHERE` clause for `GROUP BY`.** You cannot use `WHERE` on aggregate math!

```sql
-- Q: Find the number of employees in every single department.
SELECT Department, COUNT(*) as TotalStaff
FROM Employees
GROUP BY Department;

-- Q: Find departments that have MORE than 50 employees.
SELECT Department, COUNT(*) 
FROM Employees
GROUP BY Department
HAVING COUNT(*) > 50; 
```

---

## 6. Joins (VERY IMPORTANT)

*   **INNER JOIN:** Returns ONLY rows that map in BOTH tables.
*   **LEFT JOIN:** Returns EVERYTHING from Table A, plus matching from B (NULL if no match).
*   **RIGHT JOIN:** Returns EVERYTHING from Table B, plus matching from A.
*   **FULL JOIN:** Returns EVERYTHING everywhere. (MySQL requires a `UNION` of Left and Right).

```sql
-- Join Employees (A) with Departments (B)
SELECT E.Name, D.DeptName
FROM Employees E
INNER JOIN Departments D ON E.DeptID = D.DeptID;
```

---

## 7. Subqueries

### Nested Query (Executes from Inside -> Out)
```sql
-- Find everyone making more than the average salary.
SELECT Name FROM Employees 
WHERE Salary > (SELECT AVG(Salary) FROM Employees);
```

### Correlated Subquery (Executes line-by-line)
The inner query references a column from the outer query. Very slow, but powerful.
```sql
-- Find employees who earn more than the average salary in THEIR SPECIFIC department!
SELECT Name, Salary, Department
FROM Employees E1
WHERE Salary > (
    SELECT AVG(Salary) 
    FROM Employees E2 
    WHERE E1.Department = E2.Department -- The Correlation!
);
```

---

## 8. Constraints

```sql
CREATE TABLE Users (
    ID INT PRIMARY KEY,            -- NOT NULL + UNIQUE combined
    Phone VARCHAR(10) UNIQUE,      -- No duplicates allowed globally
    Age INT NOT NULL,              -- Must provide age
    City VARCHAR(50) DEFAULT 'NYC',-- Defaults to NYC if left blank
    Salary INT CHECK (Salary > 0), -- Prevents negative salaries
    DeptID INT,
    FOREIGN KEY (DeptID) REFERENCES Departments(ID) -- Links tables
);
```

---

## 9. Views

A Virtual Table. It's just a saved `.sql` query acting like a table. Great for security (hiding salary columns from basic users).

```sql
CREATE VIEW ActiveHRUsers AS 
SELECT Name, Email FROM Employees WHERE Status = 'Active' AND Dept = 'HR';

-- Anyone can now query the View, keeping Salaries hidden safely!
SELECT * FROM ActiveHRUsers;
```

---

## 10. Indexes in SQL

Speeds up data retrieval massively (`O(N)` vs `O(log N)`) via a B-Tree structure.
```sql
CREATE INDEX idx_lastname ON Employees (LastName);
```
**Benefits:** Ultra-fast `SELECT` speeds.
**Drawbacks:** Slows down `INSERT` / `UPDATE` / `DELETE` (Index must be rebuilt). Takes up massive hard drive space.

---

## 11. Stored Procedures & Functions

Precompiled SQL code saved directly on the Database Server.

*   **Function:** MUST return a value. Cannot modify database state (No DELETE/UPDATE). Called inside `SELECT` queries.
*   **Procedure:** A script that can return multiple values, modify the database, loop, and IF/ELSE. Cannot be run inside a `SELECT`.

```sql
DELIMITER //
CREATE PROCEDURE GiveRaises(IN dept_name VARCHAR(50))
BEGIN
    UPDATE Employees SET Salary = Salary + 1000 WHERE Dept = dept_name;
END //
DELIMITER ;

-- Execute it:
CALL GiveRaises('IT');
```

---

## 12. Triggers

Special Stored Procedures that run **AUTOMATICALLY** when an event (`INSERT`, `UPDATE`, `DELETE`) occurs (`BEFORE` or `AFTER`).

```sql
-- Log every time a salary is updated
CREATE TRIGGER after_salary_update 
AFTER UPDATE ON Employees
FOR EACH ROW
BEGIN
    INSERT INTO AuditLog (EmpID, OldSalary, NewSalary)
    VALUES (NEW.ID, OLD.Salary, NEW.Salary);
END;
```

---

## 13. Set Operations

Combines the results of TWO entire queries (Not matching columns like Joins, but stacking data rows vertically!). Both tables must have the exact same column types.

*   **UNION:** Stacks two queries together and auto-removes duplicates.
*   **UNION ALL:** Stacks two queries together but KEEPS duplicates (Faster).
*   **INTERSECT:** Keeps only rows that exist in BOTH queries (MySQL doesn't support this natively).
*   **MINUS / EXCEPT:** Query 1 MINUS Query 2 (Removes anything from Q1 that also exists in Q2).

```sql
SELECT Email FROM Customers
UNION
SELECT Email FROM Suppliers;
```

---

## 14. Window Functions (ADVANCED 🔥)

Unlike Aggregate Functions (which squash 100 rows into 1 row), Window Functions perform math across multiple rows but **KEEP ALL ROWS INTACT!**

*   `ROW_NUMBER()`: Gives every row a sequential ID (1, 2, 3...) based on an `ORDER BY`.
*   `RANK()`: Gives ranks (1, 2, 2, 4...). Skips numbers if there's a tie.
*   `DENSE_RANK()`: Gives ranks (1, 2, 2, 3...). NO gaps between ties!

```sql
-- Q: Rank employees inside each department by their salary!
SELECT Name, Department, Salary,
       RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) as PayRank
FROM Employees;
```
*(The `PARTITION BY` restarts the rank counter back to 1 for every new Department!)*

---
*SQL Comprehensive Guide | Master Queries & Logic | Prepared for Technical Placements*
