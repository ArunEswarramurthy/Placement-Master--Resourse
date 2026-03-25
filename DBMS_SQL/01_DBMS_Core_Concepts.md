# 🗄️ PART 1: DBMS (Database Management System) – Core Concepts
### Complete Placement Preparation | Theory, Design & Architecture 🚀

---

## 📌 TABLE OF CONTENTS
1. [Introduction to DBMS](#1-introduction-to-dbms)
2. [Data Models](#2-data-models)
3. [ER Diagram (VERY IMPORTANT)](#3-er-diagram-very-important)
4. [Keys (CRITICAL FOR INTERVIEWS)](#4-keys-critical-for-interviews)
5. [Normalization (MOST ASKED)](#5-normalization-most-asked)
6. [Functional Dependency](#6-functional-dependency)
7. [Transactions & ACID Properties](#7-transactions--acid-properties)
8. [Concurrency Control](#8-concurrency-control)
9. [Indexing](#9-indexing)
10. [Joins (Conceptual)](#10-joins-conceptual)
11. [DBMS Architecture (3-Level)](#11-dbms-architecture-3-level)
12. [SQL vs DBMS vs RDBMS](#12-sql-vs-dbms-vs-rdbms)

---

## 1. Introduction to DBMS

### What is DBMS?
A **Database Management System (DBMS)** is software that allows users to create, define, manipulate, and manage databases. It sits between the user and the raw data, ensuring data is organized and easily retrievable.

### File System vs DBMS
| Feature | File System (e.g., .txt / .csv) | DBMS (e.g., MySQL, Oracle) |
|---|---|---|
| **Redundancy** | High (Duplicate data everywhere) | Controlled (Centralized data) |
| **Search Speed** | Very Slow (Must scan whole file) | Very Fast (Uses Indexing) |
| **Concurrency** | Weak (Two people can't edit it at once) | Strong (Transactions prevent collisions) |
| **Security** | Low (Anyone with the file can read it) | High (User roles and passwords) |

### Advantages of DBMS
*   **Data Integrity:** Enforces rules (e.g., Age cannot be negative).
*   **Data Security:** Restricts unauthorized access.
*   **Provides Backup & Recovery:** Doesn't lose data if the system crashes.

### Types of DBMS
1.  **Hierarchical:** Tree-like structure (Parent-Child). Example: Windows Registry.
2.  **Network:** Graph structure (Many-to-Many).
3.  **Relational (RDBMS) - MOST IMPORTANT:** Data stored in 2D Tables (Rows & Columns) linked by Keys. Example: MySQL, Oracle.
4.  **NoSQL:** Stores data in Documents (JSON) or Key-Value pairs. Example: MongoDB, Redis.

---

## 2. Data Models
Data models define how data is structured logically.

1.  **Entity-Relationship (ER) Model:** Used for conceptual design. Uses real-world entities (e.g., Student, Teacher) and relationships (e.g., Enrolled In).
2.  **Relational Model:** Represents the ER Model as 2D Tables (Relations).
3.  **Object-Oriented Model:** Stores data as objects (similar to Java/C++).

---

## 3. ER Diagram (VERY IMPORTANT)

An ER (Entity-Relationship) Diagram is the blueprint of a database.

1.  **Entity (Rectangle ▭):** A real-world object. *e.g., Student, Car, Employee.*
2.  **Attribute (Oval ⬭):** A property of an Entity. *e.g., Age, Name, Salary.*
    *   **Simple:** Cannot be divided (e.g., Age).
    *   **Composite:** Can be divided into smaller sub-parts (e.g., Name -> First Name, Last Name).
    *   **Derived (Dashed Oval):** Calculated from another attribute (e.g., Age is derived from Date of Birth).
    *   **Multivalued (Double Oval Ⓞ):** Can have multiple values (e.g., Phone Numbers, Skills).
3.  **Relationship (Diamond ♢):** How entities are linked. *e.g., Student (Entity) `Enrolls In` (Relationship) Course (Entity).*

### Cardinality (Mapping Constraints)
*   **1:1 (One-to-One):** One person has one Passport.
*   **1:M (One-to-Many):** One Department has many Employees.
*   **M:N (Many-to-Many):** Many Students enroll in many Courses.

### Participation Constraints
*   **Total (Double Line):** EVERY entity must participate. (Every Employee MUST belong to a Department).
*   **Partial (Single Line):** Not every entity participates. (Not every Employee manages a Department).

### Weak Entity (Double Rectangle)
An entity that cannot exist without its Parent entity. (e.g., A `Bank Account` is strong. An `ATM Transaction` is weak; if you delete the Account, the Transactions must also be deleted).

---

## 4. Keys (CRITICAL FOR INTERVIEWS)

Keys uniquely identify a tuple (row) in a table and establish relationships.

1.  **Super Key:** ANY combination of columns that can uniquely identify a row. *(e.g., `{EmpID}`, `{EmpID, Name}`, `{Email, Phone}`)*
2.  **Candidate Key:** A Super Key with NO unnecessary columns. The minimal Super Key. *(e.g., `{EmpID}`, `{Email}`)*
3.  **Primary Key (PK):** The specific Candidate Key chosen by the database designer to be the main identifier. **Rules: Cannot be NULL, Cannot have duplicates.**
4.  **Alternate Key:** All the Candidate Keys that were NOT chosen to be the Primary Key. (If PK = `EmpID`, then `Email` is the Alternate Key).
5.  **Foreign Key (FK):** A column in Table B that refers to the Primary Key in Table A. Used to link tables.
6.  **Composite Key:** A Primary Key made of TWO OR MORE columns. (e.g., `{StudentID, CourseID}` in an Enrollment table).

---

## 5. Normalization (MOST ASKED)

**Purpose:** To organize tables to remove **Redundancy** (duplicate data) and **Anomalies** (Insertion, Updation, Deletion errors).

| Form | Rule | Example Strategy |
|---|---|---|
| **1NF** | No repeating groups. Every cell must be **Atomic** (Single value). | You cannot have `Skills: Java, C++` in one cell. Make new rows! |
| **2NF** | Must be in 1NF + **No Partial Dependency**. | If PK is composite `{StudentID, CourseID}`, a non-key column like `CourseName` should not depend ONLY on `CourseID`. Move it to a new table! |
| **3NF** | Must be in 2NF + **No Transitive Dependency**. | `EmpID -> DeptID -> DeptLocation`. `Location` depends on `DeptID`, not `EmpID`. Move `DeptID` and `Location` to a totally new `Departments` table! |
| **BCNF** | Must be in 3NF + For every dependency `A -> B`, `A` MUST be a Candidate Key. | A stronger, stricter version of 3NF. |

---

## 6. Functional Dependency

**Definition:** A relationship where one attribute uniquely determines another. Denoted as `X -> Y` (X determines Y).
(e.g., `Aadhar_Number -> Name`. If you know the Aadhar Number, you definitely know the Name).

*   **Trivial Dependency:** `X -> Y` is trivial if Y is a subset of X. (e.g., `{EmpID, Name} -> EmpID`).
*   **Non-Trivial Dependency:** X and Y share no common attributes. (e.g., `EmpID -> Phone`).
*   **Closure of Attributes ($X^+$):** Finding all attributes that can be uniquely determined by an attribute X using given dependencies.

---

## 7. Transactions & ACID Properties

A **Transaction** is a logical unit of work (e.g., Transferring money from A to B requires two steps: Deduct A, Add B).

The 4 ACID Properties guarantee database reliability during transactions:
1.  **Atomicity:** "All or Nothing." If the system crashes after deducting A but before adding to B, the transaction is **rolled back** completely.
2.  **Consistency:** The database must remain in a valid state. (If a rule says A+B must = $1000 before the transfer, A+B must still = $1000 after).
3.  **Isolation:** If 10 people transfer money simultaneously, their transactions execute invisibly to each other to prevent chaos.
4.  **Durability:** Once a transaction is `COMMIT`ted, it is permanently saved. Even if the server explodes one second later, the data is safe on the hard drive.

---

## 8. Concurrency Control

When multiple transactions run at the same time, massive problems occur:

### Concurrency Problems:
1.  **Dirty Read:** Transaction 1 updates a value but hasn't committed. Transaction 2 reads that uncommitted (dirty) value. T1 rolls back! Now T2 has completely fake data!
2.  **Non-repeatable Read:** T1 reads a value. T2 aggressively updates the value and commits. T1 reads the exact same row again and gets a completely different number!
3.  **Phantom Read:** T1 counts the number of employees. T2 suddenly inserts 5 new employees. T1 counts again and the number magically changed!

### Solutions (Locking):
*   **Shared Lock (Read Lock):** Multiple transactions can read the data, but NO ONE can write/update it.
*   **Exclusive Lock (Write Lock):** Only ONE transaction can read AND write. Everyone else is locked out.
*   **Deadlock:** T1 has Lock A, waiting for Lock B. T2 has Lock B, waiting for Lock A. Both freeze forever!

---

## 9. Indexing

**What is it?** A data structure technique to efficiently retrieve rows from a table. It works exactly like the Index at the back of a book. Without an index, the DBMS must perform a **Full Table Scan** (O(N) time).

*   **Primary Index:** Created automatically on the Primary Key. Sorted and incredibly fast.
*   **Secondary Index:** Created on non-key columns (like `Name` or `Salary`).
*   **Clustered Index:** Physically sorts the actual rows on the hard drive. A table can only have ONE Clustered Index (usually the Primary Key).
*   **Non-Clustered Index:** The rows remain unsorted. The index is a separate map of pointers to the rows. A table can have MANY Non-Clustered Indexes.

---

## 10. Joins (Conceptual)

Combining rows from 2 or more tables using related columns (Foreign Keys).
1.  **Inner Join:** Intersection. Returns ONLY rows that match in BOTH tables.
2.  **Outer Join:**
    *   **Left:** ALL of table 1 + Matches from table 2. (Unmatched get NULLs).
    *   **Right:** ALL of table 2 + Matches from table 1.
    *   **Full:** ALL of table 1 AND table 2. (MySQL uses UNION left and right).
3.  **Natural Join:** Automatically joins tables based on columns with the EXACT SAME NAME. No `ON` clause required.

---

## 11. DBMS Architecture

Databases use a **3-Level (ANSI-SPARC)** architecture to achieve Data Independence.

1.  **Internal Level (Physical):** Describes how the data is physically stored on the hard drive (bytes, blocks). Only network admins care about this.
2.  **Conceptual Level (Logical):** Describes WHAT data is stored (The Tables, ER Diagram, Constraints). DB Designers care about this.
3.  **External Level (View):** Describes the part of the database a specific user sees. The HR Manager sees a view with Salaries. The End User sees a view with Names, but the Salaries are hidden.

---

## 12. SQL vs DBMS vs RDBMS

| Term | Definition |
|---|---|
| **DBMS** | The overarching concept/software of managing ANY type of database (e.g., XML files, JSON). |
| **RDBMS** | A strict specific TYPE of DBMS based on the Relational Model (Tables). Strict rules on Primary/Foreign Keys and Normalization. |
| **SQL** | The **Language** you type to talk to the RDBMS software. (DBMS is the car, SQL is the steering wheel). |

---
*DBMS Core Concepts | Zero to Hero Curriculum | Prepared for Technical Placements*
