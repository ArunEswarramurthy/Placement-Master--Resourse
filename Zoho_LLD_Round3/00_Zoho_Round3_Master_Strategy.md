# 🏢 ZOHO ROUND 3: Advanced Programming Mastery Strategy
### The "No Database" Rule, OOP HashMaps, and How to Clear LLD 🚀

---

## 📌 TABLE OF CONTENTS
1. [What happens in Zoho Round 3?](#1-what-happens-in-zoho-round-3)
2. [The "No Database" Rule (Using memory structures)](#2-the-no-database-rule-using-memory-structures)
3. [The Golden Blueprint: How to structure any system](#3-the-golden-blueprint-how-to-structure-any-system)
4. [Mastering the `Map` and `List` combination](#4-mastering-the-map-and-list-combination)
5. [The Top 20 Most Asked Questions](#5-the-top-20-most-asked-questions)

---

## 1. What happens in Zoho Round 3? (Advanced Programming)

Zoho Round 3 is a **Low-Level Design (LLD)** or **Advanced Application Building** round.
You will be given a real-world scenario (e.g., "Build an ATM Simulator", "Build IRCTC"). You will have **2 to 3 hours** to code the entire backend logic from scratch.

### 🛑 What the Interviewer is looking for:
1.  **Modularity:** Is your code broken down into proper Classes? (No giant 500-line `main` functions!).
2.  **Encapsulation:** Are your variables `private` with safe `public` getters/setters?
3.  **Data Structures:** Can you choose the right Data Structure (`ArrayList`, `HashMap`, `Queue`) to store and retrieve data efficiently?
4.  **Edge Cases:** If a user tries to book a train ticket, but there are 0 seats, does your system gracefully say "Waitlisted" or does it crash?

---

## 2. The "No Database" Rule (Using memory structures)

**You are NOT allowed to use MySQL, MongoDB, or any external database!**
All data must be stored in the RAM while the program runs.

If you need a "Users" Table, in Zoho Round 3, you create a `HashMap<Integer, User>`!

| Database Concept | Zoho Round 3 Java Equivalent |
|---|---|
| A "Table" or "Database" | A `class Database` or `class System` |
| A "Row" in a table | An Object (`User user1 = new User()`) |
| An "Index" for fast searching | A `HashMap<Key, Object>` |
| A "List of all Transactions" | An `ArrayList<Transaction>` |
| A "Primary Key" | A static counter variable `static int idCounter = 1;` |

---

## 3. The Golden Blueprint: How to structure any system

EVERY single Zoho question can be broken down into 4 physical files/classes. **Do not write everything in one file during the interview if you are using an IDE!** (If they force HackerRank, use multiple classes in one file).

1.  **The POJO (Plain Old Java Object) Classes:**
    *   *Examples:* `class Passenger`, `class Ticket`, `class Train`.
    *   *Role:* Holds data. Contains variables, constructors, and getters/setters.
2.  **The Manager / Controller Class:**
    *   *Examples:* `class BookingManager`, `class ParkingController`.
    *   *Role:* Holds the `HashMaps` and `ArrayLists`. Contains the core logic (`bookTicket()`, `cancelTicket()`).
3.  **The Enum / Constants:**
    *   *Examples:* `enum TicketStatus { CONFIRMED, WAITLISTED, CANCELLED }`.
4.  **The Main Driver Class:**
    *   *Role:* Contains the `Scanner` setup, an infinite `while(true)` loop, and a `switch` statement for the User Interface.

---

## 4. Mastering the `Map` and `List` combination

If you master this single concept, you can solve 90% of Zoho questions:

```java
// How to store Users so you can look them up instantly by ID (O(1) time):
Map<Integer, User> userDB = new HashMap<>();
userDB.put(user.getId(), user);

// How to store ALL tickets a specific user has booked (1:Many Relationship!):
Map<Integer, List<Ticket>> userTicketsDB = new HashMap<>();

// When a user books a ticket:
userTicketsDB.putIfAbsent(userId, new ArrayList<>()); // Create empty list if first time
userTicketsDB.get(userId).add(newTicket);             // Add the ticket to their list
```

---

## 5. The Top 20 Most Asked Questions

We will solve all 20 of these in this repository. Ensure you understand the underlying logic of the first 5 completely, as the remaining 15 are simply variations!

1.  **Railway Reservation (IRCTC)** - *The #1 most asked.*
2.  **Taxi Booking / Uber** - *Requires calculating nearest distance.*
3.  **Parking Lot Simulator** - *Requires tracking different vehicle sizes (Car/Bike/Bus).*
4.  **ATM Simulator** - *Requires tracking denomination counts (100rs, 500rs notes).*
5.  **Flight Ticket Booking** - *Requires dynamic pricing (Price goes up as seats fill).*
6.  Library Management
7.  Food Delivery (Zomato)
8.  Expense Sharing (Splitwise)
9.  E-Commerce (Amazon)
10. Invoice/Billing System
11. Hotel Room Booking
12. Movie Ticket Booking (BookMyShow)
13. Vending Machine
14. Snake & Ladder Game Engine
15. LRU Cache
16. Cricket Scoreboard
17. Bus Reservation (RedBus)
18. Toll Gate Management
19. Chess Framework
20. Elevator Control System

---
*Zoho Advanced Programming Mastery | Zero to Hero Curriculum | Placement Preparation*
