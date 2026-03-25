# 🔥 PART 3: DBMS & SQL Placement Strategy & Practice
### Prioritized Topics, Interview Strategies, and 100+ Practice Prompts 🚀

---

## 📌 TABLE OF CONTENTS
1. [Most Important Topics for Placement (Priority List)](#1-most-important-topics-for-placement-priority-list)
2. [Practice Strategy for TCS NQT & Product Companies](#2-practice-strategy-for-tcs-nqt--product-companies)
3. [Pro-Level Topics (Optional but Powerful)](#3-pro-level-topics-optional-but-powerful)
4. [TCS NQT Style Practice Questions (Phase 1)](#4-tcs-nqt-style-practice-questions-phase-1)

---

## 1. Most Important Topics for Placement (Priority List)

If you are short on time before an interview, focus strictly on this order:

1.  **SQL `SELECT` + `WHERE` + `JOIN`** (The absolute baseline expected of everyone).
2.  **`GROUP BY` + `HAVING`** (The most common interview logic trap).
3.  **Subqueries** (Nested vs Correlated).
4.  **Normalization (1NF → 3NF)** (You will invariably be asked to define these and spot anomalies).
5.  **Keys + ER Diagram** (Know your Primary vs Candidate vs Super keys).
6.  **ACID Properties** (Atomicity, Consistency, Isolation, Durability).
7.  **Transactions & Concurrency** (Dirty reads, locks).
8.  **Indexing Basics** (How databases search quickly using B-Trees).

> ⚡ **FINAL SUMMARY:** 
> 👉 **DBMS** = Theory (Design + Concepts + Architecture)
> 👉 **SQL** = Practical (Queries + Problem Solving + Math)
> Both are equally important. You cannot pass an interview knowing only one.

---

## 2. Practice Strategy for TCS NQT & Product Companies

### Step 1: Learn → Execute immediately
For every concept you just learned in Parts 1 and 2, immediately solve 5 problems regarding that concept to cement the logic.

### Step 2: Practice Platforms
1.  **HackerRank (SQL Section):** Perfect for building baseline syntax speed and confidence.
2.  **LeetCode (Database Section):** The absolute gold standard for FAANG and top-tier product companies. Focus on Easy and Medium problems.

### Step 3: Core Focus Areas for Queries
*   **Joins:** "Find employees who do NOT have a manager."
*   **Aggregation:** "Find the 2nd highest salary in the IT department." (Classic Interview Question!)
*   **Real-world queries:** "List all users who purchased item X but not item Y."

---

## 3. Pro-Level Topics (Optional but Powerful)

If you have extra time or are aiming for a highly specialized Database role:
1.  **Query Optimization:** How to rewrite a slow query into a fast one.
2.  **Execution Plan (`EXPLAIN`):** Reading exactly how the DBMS plans to execute your query internally.
3.  **NoSQL Basics:** Learn the architecture of MongoDB or Cassandra.
4.  **Database Design Case Studies:** How would you design the database for Uber or Twitter? (Which tables? How do they connect?)

---

## 4. TCS NQT Style Practice Questions (Phase 1)

Here are 5 classic interview screening questions to start your practice.

**Q1: The "2nd Highest" Pattern**
Write a SQL query to find the 2nd highest salary from an `Employee` table.
```sql
-- Solution (MySQL specific using LIMIT):
SELECT Salary FROM Employee ORDER BY Salary DESC LIMIT 1 OFFSET 1;

-- Solution (Generic using Subquery):
SELECT MAX(Salary) FROM Employee WHERE Salary < (SELECT MAX(Salary) FROM Employee);
```

**Q2: The "Duplicate Values" Pattern**
Write a SQL query to find all duplicate emails in a table named `Person`.
```sql
SELECT Email 
FROM Person 
GROUP BY Email 
HAVING COUNT(Email) > 1;
```

**Q3: The "Anti-Join" Pattern**
Write a SQL query to find all customers who never ordered anything. (Tables: `Customers` and `Orders`).
```sql
SELECT C.Name AS Customers
FROM Customers C
LEFT JOIN Orders O ON C.Id = O.CustomerId
WHERE O.Id IS NULL;
```

**Q4: The "Self Join" Pattern**
Given an `Employee` table containing an `Id`, `Name`, `Salary`, and `ManagerId`. Write a query to find employees who earn more than their managers.
```sql
SELECT E1.Name AS Employee
FROM Employee E1
JOIN Employee E2 ON E1.ManagerId = E2.Id
WHERE E1.Salary > E2.Salary;
```

**Q5: Theory Definition**
"What is a Dirty Read, and which transaction isolation level prevents it?"
> *Answer:* A Dirty Read occurs when a transaction reads data that has been modified by another concurrent transaction but has not yet been committed. The `READ COMMITTED` isolation level prevents dirty reads.

---
*DBMS & SQL Practice Strategy | Master Queries & Logic | Prepared for Technical Placements*
