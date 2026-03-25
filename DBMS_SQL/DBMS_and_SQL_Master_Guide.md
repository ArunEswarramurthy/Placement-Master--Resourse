# 🗄️ DBMS & MySQL: The Ultimate Zero-to-Hero Guide
### Master Databases, SQL Queries, Normalization & ACID Properties 🚀

---

## 📌 TABLE OF CONTENTS

### PART A — DATABASE FUNDAMENTALS
1. [What is Data, Database, and DBMS?](#1-what-is-data-database-and-dbms)
2. [File System vs DBMS (Why do we need it?)](#2-file-system-vs-dbms-why-do-we-need-it)
3. [RDBMS vs NoSQL (SQL vs Document)](#3-rdbms-vs-nosql-sql-vs-document)
4. [Keys in DBMS (Primary, Foreign, Super, Candidate)](#4-keys-in-dbms-primary-foreign-super-candidate)

### PART B — SQL ESSENTIALS (MySQL Syntax)
5. [The 5 Sub-languages of SQL (DDL, DML, DQL, DCL, TCL)](#5-the-5-sub-languages-of-sql-ddl-dml-dql-dcl-tcl)
6. [Basic Queries (`SELECT`, `WHERE`, `ORDER BY`, `LIMIT`)](#6-basic-queries-select-where-order-by-limit)
7. [Operators (`IN`, `BETWEEN`, `LIKE` / Wildcards)](#7-operators-in-between-like--wildcards)
8. [Aggregate Functions (`COUNT`, `MAX`, `MIN`, `SUM`, `AVG`)](#8-aggregate-functions-count-max-min-sum-avg)
9. [Grouping Data (`GROUP BY` & `HAVING`)](#9-grouping-data-group-by--having)

### PART C — ADVANCED SQL (The Interview Core)
10. [JOINS (Inner, Left, Right, Full, Cross, Self)](#10-joins-inner-left-right-full-cross-self)
11. [Subqueries (Nested Queries)](#11-subqueries-nested-queries)
12. [Constraints (`NOT NULL`, `UNIQUE`, `DEFAULT`, `CHECK`)](#12-constraints-not-null-unique-default-check)
13. [Views (Virtual Tables)](#13-views-virtual-tables)

### PART D — ARCHITECTURE & THEORY
14. [ACID Properties (Transactions)](#14-acid-properties-transactions)
15. [Normalization (1NF, 2NF, 3NF, BCNF)](#15-normalization-1nf-2nf-3nf-bcnf)
16. [Indexing (How databases search instantly)](#16-indexing-how-databases-search-instantly)

---

# ═══════════════════════════════════
# PART A — DATABASE FUNDAMENTALS
# ═══════════════════════════════════

## 1. What is Data, Database, and DBMS?

*   **Data:** Raw, unorganized facts (e.g., `Arjun`, `22`, `Engineer`).
*   **Database:** A highly organized collection of data, making it easy to access, manage, and update. Think of it as a huge digital filing cabinet.
*   **DBMS (Database Management System):** The **Software** you use to interact with the database. You write queries, and the DBMS safely fetches the data for you.
    *   *Examples:* MySQL, PostgreSQL, Oracle, MongoDB.

---

## 2. File System vs DBMS (Why do we need it?)

Storing data in Excel files (`.csv` or `.txt`) works for 100 people, but fails for Facebook.

**Why DBMS wins:**
1.  **No Data Redundancy:** Fixing an address changes it everywhere automatically.
2.  **Data Consistency:** If your bank transfer fails midway, the money isn't lost (Transactions).
3.  **Security & Access:** Only the HR team can see Salary data, everyone else just sees Names.
4.  **Concurrency:** 1 Million people booking IRCTC train tickets at the exact same second without overlapping seats!

---

## 3. RDBMS vs NoSQL (SQL vs Document)

| Feature | RDBMS (Relational Database) | NoSQL (Non-Relational) |
|---|---|---|
| **Structure** | Tables (Rows & Columns) | Documents (JSON style), Key-Value |
| **Schema** | Rigid (Must define columns beforehand) | Flexible (Can add random data fields anytime) |
| **Scaling** | Vertical (Buy a more expensive server) | Horizontal (Add 5 cheap servers together) |
| **Best For** | Complex banking, ERP, connected data | Huge dynamic data, social media feeds |
| **Examples** | MySQL, PostgreSQL, Oracle | MongoDB, Redis, Cassandra |

---

## 4. Keys in DBMS (Primary, Foreign, Super, Candidate)

Keys are used to **uniquely identify** a row in a table or establish a relationship between two tables.

1.  **Super Key:** Any combination of columns that uniquely identifies a row. (e.g., `[EmpID]`, `[EmpID, Name]`, `[Email, Phone]`).
2.  **Candidate Key:** A Super Key with NO extra columns. The absolute minimum needed to identify a row. (e.g., `[EmpID]`, `[Email]`).
3.  **Primary Key (PK):** The ONE Candidate Key the database designer explicitly chooses to be the main identifier. **Cannot be NULL. Cannot be Duplicate.**
4.  **Foreign Key (FK):** A column in Table B that points to the Primary Key in Table A. Used to link tables together (Relationships).
5.  **Composite Key:** A Primary Key made entirely of **two or more columns combined** (e.g., `[StudentID, CourseID]`).

---

# ═══════════════════════════════════
# PART B — SQL ESSENTIALS (MySQL Syntax)
# ═══════════════════════════════════

## 5. The 5 Sub-languages of SQL

Every SQL command falls into one of these 5 categories:

*   **DDL (Data Definition Language):** Defines the **Structure** of the table.
    *   `CREATE`, `ALTER` (modify table structure), `DROP` (delete table), `TRUNCATE` (delete all rows, keep structure).
*   **DML (Data Manipulation Language):** Deals with the **Data** inside the table.
    *   `INSERT`, `UPDATE`, `DELETE`.
*   **DQL (Data Query Language):** Getting data out.
    *   `SELECT`.
*   **DCL (Data Control Language):** Security & Permissions.
    *   `GRANT`, `REVOKE`.
*   **TCL (Transaction Control Language):** Managing saving/undoing.
    *   `COMMIT`, `ROLLBACK`, `SAVEPOINT`.

---

## 6. Basic Queries (`SELECT`, `WHERE`, `ORDER BY`, `LIMIT`)

Imagine a table named `Employees (EmpID, Name, Department, Salary)`.

```sql
-- 1. Fetch EVERYTHING from the table
SELECT * FROM Employees;

-- 2. Fetch specific columns
SELECT Name, Salary FROM Employees;

-- 3. Filter using WHERE (Only IT department)
SELECT * FROM Employees WHERE Department = 'IT';

-- 4. Multiple conditions (AND / OR)
SELECT * FROM Employees WHERE Department = 'IT' AND Salary > 50000;

-- 5. Sort the results (ORDER BY) - Default is Ascending (ASC)
SELECT * FROM Employees ORDER BY Salary DESC; -- Highest salary first

-- 6. Fetch only top 3 results (LIMIT)
SELECT * FROM Employees ORDER BY Salary DESC LIMIT 3;
```

---

## 7. Operators (`IN`, `BETWEEN`, `LIKE` / Wildcards)

```sql
-- IN: Matches any value in a list (Better than writing lots of ORs)
SELECT * FROM Employees WHERE Department IN ('IT', 'HR', 'Finance');

-- BETWEEN: Matches a range (Inclusive)
SELECT * FROM Employees WHERE Salary BETWEEN 40000 AND 60000;

-- LIKE: Pattern Matching (Wildcards -> '%' means zero/more chars, '_' means EXACTLY one char)
SELECT * FROM Employees WHERE Name LIKE 'A%';   -- Starts with 'A'
SELECT * FROM Employees WHERE Name LIKE '%a';   -- Ends with 'a'
SELECT * FROM Employees WHERE Name LIKE '%sh%'; -- Contains 'sh' anywhere
SELECT * FROM Employees WHERE Name LIKE '_rjun';-- Starts with any ONE letter, followed by "rjun"
```

---

## 8. Aggregate Functions (`COUNT`, `MAX`, `MIN`, `SUM`, `AVG`)

These functions perform calculations on multiple rows and return a **single** value.

```sql
SELECT COUNT(*) FROM Employees;             -- Total number of employees
SELECT MAX(Salary) FROM Employees;          -- Highest salary
SELECT MIN(Salary) FROM Employees;          -- Lowest salary
SELECT SUM(Salary) FROM Employees;          -- Total salary payout
SELECT AVG(Salary) FROM Employees WHERE Department = 'IT'; -- Average IT salary
```

---

## 9. Grouping Data (`GROUP BY` & `HAVING`)

**`GROUP BY`** clumps rows together based on a column. It is almost ALWAYS used with Aggregate functions.
**`HAVING`** is the `WHERE` clause for `GROUP BY`. You cannot use `WHERE` on aggregate functions!

```sql
-- Q: Find the average salary for EACH department.
SELECT Department, AVG(Salary) as AvgPay 
FROM Employees 
GROUP BY Department;

-- Q: Find departments where the average salary is greater than 60,000.
SELECT Department, AVG(Salary) as AvgPay 
FROM Employees 
GROUP BY Department 
HAVING AVG(Salary) > 60000; 
-- (You MUST use HAVING here, WHERE will throw an error!)
```

---

# ═══════════════════════════════════
# PART C — ADVANCED SQL (The Interview Core)
# ═══════════════════════════════════

## 10. JOINS (Inner, Left, Right, Full, Cross, Self)

Joins are used to combine rows from two or more tables, based on a related column between them (Primary Key -> Foreign Key).

Imagine `Table A (Employees)` and `Table B (Departments)`.

1.  **INNER JOIN:** Returns records that have matching values in BOTH tables. (The intersection).
2.  **LEFT (OUTER) JOIN:** Returns ALL records from the Left table, and the matched records from the Right table. If no match, right side gives NULLs.
3.  **RIGHT (OUTER) JOIN:** Returns ALL records from the Right table, and matched from the Left.
4.  **FULL (OUTER) JOIN:** Returns ALL records when there is a match in either left or right table. (MySQL doesn't support this directly; we use a workaround with `UNION`).
5.  **CROSS JOIN:** Returns the Cartesian product (Every row in Table A matches with every row in Table B).
6.  **SELF JOIN:** A regular join, but the table is joined with *itself*.

### JOIN Syntax
```sql
-- Inner Join Example
SELECT Employees.Name, Departments.DeptName
FROM Employees
INNER JOIN Departments ON Employees.DeptID = Departments.ID;

-- Left Join Example
SELECT Employees.Name, Departments.DeptName
FROM Employees
LEFT JOIN Departments ON Employees.DeptID = Departments.ID;
```

---

## 11. Subqueries (Nested Queries)

A query inside another query. The inner query executes first, and its result is passed to the outer query.

```sql
-- Q: Find employees who earn MORE than the average company salary.
-- Step 1 (Inner): Find Average Salary (e.g., this calculates to 50,000)
-- Step 2 (Outer): Find salaries > 50,000

SELECT Name, Salary 
FROM Employees 
WHERE Salary > (SELECT AVG(Salary) FROM Employees);

-- Q: Find employees working in the 'IT' department (using ID from another table)
SELECT Name FROM Employees 
WHERE DeptID IN (SELECT ID FROM Departments WHERE DeptName = 'IT');
```

---

## 12. Constraints

Rules applied to columns to ensure data accuracy and reliability.

*   `NOT NULL` - Column cannot have a NULL value.
*   `UNIQUE` - All values in a column must be different.
*   `PRIMARY KEY` - A combination of a `NOT NULL` and `UNIQUE`.
*   `FOREIGN KEY` - Prevents actions that would destroy links between tables.
*   `CHECK` - Ensures values satisfy a specific condition.
*   `DEFAULT` - Sets a default value if none is specified.

```sql
CREATE TABLE Persons (
    ID int PRIMARY KEY,
    Age int CHECK (Age >= 18),
    City varchar(255) DEFAULT 'Chennai'
);
```

---

## 13. Views (Virtual Tables)

A View is a virtual table based on the result-set of an SQL statement.
It doesn't store data itself. It's just a saved Query!

**Why?**
*   **Security:** Hide sensitive columns (like passwords or salaries) from specific users.
*   **Simplicity:** Turn an insane 5-table JOIN query into a simple View. You just `SELECT * FROM MyView`.

```sql
CREATE VIEW IT_Employees AS
SELECT Name, Email FROM Employees WHERE Department = 'IT';

-- Now you can query it like a real table!
SELECT * FROM IT_Employees;
```

---

# ═══════════════════════════════════
# PART D — ARCHITECTURE & THEORY
# ═══════════════════════════════════

## 14. ACID Properties (Transactions)

A Transaction is a single unit of work (e.g., Transferring money: Deduct $100 from A, Add $100 to B).
For a database to be reliable, transactions must follow **ACID rules**:

*   **A (Atomicity):** **"All or Nothing."** Either all steps of the transaction complete successfully, or none of them do. If the power dies after deducting from A, the computer rolls back A's deduction.
*   **C (Consistency):** Data must be valid before and after the transaction (e.g., Negative balances aren't allowed if a CHECK constraint exists).
*   **I (Isolation):** If two people transfer money at the exact same time, they shouldn't interfere with each other. Transactions execute as if they are alone.
*   **D (Durability):** Once a transaction is successfully `COMMIT`ted, it is PERMANENT. Even if the server instantly reboots, the data is safe on the hard drive.

---

## 15. Normalization (1NF, 2NF, 3NF, BCNF)

Normalization is the process of organizing data in a database to **reduce redundancy (duplication)** and improve data integrity.

*   **1NF (First Normal Form):**
    *   **Rule:** Every cell must contain a **Single (Atomic) Value**.
    *   *Bad:* User has `PhoneNumbers: 999999, 888888` in one cell.
    *   *Fix:* Give them separate rows!
*   **2NF (Second Normal Form):**
    *   **Rule:** Must be in 1NF **PLUS** all non-key columns must depend on the **ENTIRE** Primary Key (No Partial Dependency).
    *   *(Applies mostly if you have a Composite Primary Key made of 2 columns).*
*   **3NF (Third Normal Form):**
    *   **Rule:** Must be in 2NF **PLUS** there should be NO "Transitive Dependency." (A non-key column shouldn't depend on another non-key column).
    *   *Bad:* Table has `EmpID`, `DeptID`, `DeptLocation`. (`DeptLocation` depends on `DeptID`, not `EmpID`).
    *   *Fix:* Move `DeptID` and `DeptLocation` to a completely new `Departments` table!
*   **BCNF (Boyce-Codd Normal Form):**
    *   A stricter version of 3NF where every determinant must be a candidate key.

---

## 16. Indexing (How databases search instantly)

If you search for `Name = 'Arun'` in a table with 10 Million rows, the database normally checks every single row (Table Scan = Super slow).

**An Index** works exactly like the Index at the back of a textbook. It stores the column (sorted) and a pointer to exactly where the row lives on the hard drive.

```sql
CREATE INDEX idx_name ON Employees (Name);
```
**Pros:** Searching becomes blindingly fast (`O(log N)` using a B-Tree).
**Cons:** Every time you `INSERT`, `UPDATE`, or `DELETE`, the database has to update the Index too! This slows down write operations and consumes extra disk space. **Never index every column!**

---
*DBMS & SQL Master Guide | Prepared for TCS NQT, Product Companies & Technical Interviews*
