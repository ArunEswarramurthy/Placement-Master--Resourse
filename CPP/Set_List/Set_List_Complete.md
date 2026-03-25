# 🎯 SET & LIST (Linked List) — Complete Guide + Problems
### Master Unique Collections & Linked Data Structures | Zero → Hero 🚀

---

## 📌 TABLE OF CONTENTS

### PART A — SET BASICS (Unique & Sorted)
1. [What is a Set? (set vs unordered_set vs multiset)](#1-what-is-a-set-set-vs-unordered_set-vs-multiset)
2. [Declaring & Initializing](#2-declaring--initializing)
3. [Insert, Delete, Check Exists](#3-insert-delete-check-exists)
4. [Lower / Upper Bound in Set](#4-lower--upper-bound-in-set)

### PART B — LIST BASICS (Doubly Linked List)
5. [What is an STL List?](#5-what-is-an-stl-list)
6. [Insert, Delete, Access Operations](#6-insert-delete-access-operations)
7. [List Iterators & Reversing](#7-list-iterators--reversing)
8. [Advanced List Operations (Merge, Splice, Sort, Unique)](#8-advanced-list-operations-merge-splice-sort-unique)

### PART C — SET & LIST PROBLEMS
9. [Remove Duplicates from Array (Using Set)](#9-remove-duplicates-from-array-using-set)
10. [Find Common Elements in 3 Arrays](#10-find-common-elements-in-3-arrays)
11. [Check if Array is Subset of Another Array](#11-check-if-array-is-subset-of-another-array)
12. [First Missing Positive Integer](#12-first-missing-positive-integer)
13. [Maintain Top K Elements (Using Set/Multiset)](#13-maintain-top-k-elements-using-setmultiset)
14. [Implement a Queue using List](#14-implement-a-queue-using-list)
15. [Reverse a Linked List (Manual & STL)](#15-reverse-a-linked-list-manual--stl)
16. [Detect Cycle in Linked List (Floyd's Algorithm)](#16-detect-cycle-in-linked-list-floyds-algorithm)
17. [Find Middle of Linked List (Slow/Fast Pointer)](#17-find-middle-of-linked-list-slowfast-pointer)
18. [Merge Two Sorted Lists](#18-merge-two-sorted-lists)

---

# ═══════════════════════════════════
# PART A — SET BASICS
# ═══════════════════════════════════

## 1. What is a Set? (set vs unordered_set vs multiset)

A Set is a collection that stores **only unique elements**.

| Type | Order | Duplicates Allowed? | Internal Structure | Time Complexity (Insert/Find) |
|---|---|---|---|---|
| `set` | **Sorted** (Ascending) | ❌ No | Binary Search Tree (Red-Black) | O(log N) |
| `unordered_set` | Random | ❌ No | Hash Table | **O(1) avg**, O(N) worst |
| `multiset` | **Sorted** (Ascending) | ✅ Yes | Binary Search Tree | O(log N) |

> **Golden Rule:**
> Need order / min / max? → Use `set`.
> Just need to check if an item exists fast? → Use `unordered_set`.

---

## 2. Declaring & Initializing

```cpp
#include <set>
#include <unordered_set>
using namespace std;

// Empty sets
set<int> s1;
unordered_set<string> us1;
multiset<int> ms1;

// Initialize with values (Automatically removes duplicates & sorts!)
set<int> mySet = {5, 2, 8, 2, 1, 5};
// Result in memory: {1, 2, 5, 8}

// Initialize descending order
set<int, greater<int>> descSet = {5, 2, 8, 1};
// Result: {8, 5, 2, 1}

// From Vector
vector<int> v = {10, 20, 10, 30};
set<int> s(v.begin(), v.end());  // Converts vector to unique set!
```

---

## 3. Insert, Delete, Check Exists

```cpp
set<int> s;

// ── INSERT ──
s.insert(10);
s.insert(20);
s.insert(10);  // Ignored (duplicates not allowed)

auto result = s.insert(30);
// result.second is true if inserted, false if already existed

// ── CHECK (SEARCH) ──
if (s.count(20)) cout << "Found!\n";         // Returns 1 (true) or 0 (false)
if (s.find(50) != s.end()) cout << "Found";  // Iterator fallback

// ── DELETE ──
s.erase(20);               // By value
s.erase(s.begin());        // By iterator (removes smallest item)

// Multiset deletion trap!
multiset<int> ms = {5, 5, 5};
ms.erase(5);               // Removes ALL 5s!
ms.erase(ms.find(5));      // Removes ONLY ONE 5.

// ── SIZE / CLEAR ──
cout << s.size();
s.clear();
```

---

## 4. Lower / Upper Bound in Set

Because `set` is sorted, it has built-in super-fast Binary Search methods!

*   `lower_bound(X)`: Iterator to first element **≥ X**
*   `upper_bound(X)`: Iterator to first element **> X**

```cpp
set<int> s = {10, 20, 30, 40, 50};

auto it1 = s.lower_bound(25);  // >= 25 → returns iterator to 30
auto it2 = s.lower_bound(30);  // >= 30 → returns iterator to 30

auto it3 = s.upper_bound(30);  // > 30  → returns iterator to 40
auto it4 = s.upper_bound(60);  // > 60  → returns s.end()

if (it1 != s.end()) cout << *it1; // 30
```

---

# ═══════════════════════════════════
# PART B — LIST BASICS (Doubly Linked List)
# ═══════════════════════════════════

## 5. What is an STL List?

In C++, `std::list` is a **Doubly Linked List**.
*   **Vector:** Elements in continuous memory (Fast access `v[i]`, slow insert at front).
*   **List:** Elements floating in memory linked by pointers (No `L[i]`, fast insert anywhere).

```cpp
#include <list>
list<int> L;
```
> **When to use List?**
> When you need to insert/delete elements frequently in the **middle** or **front**, and you don't need random access `[ i ]`.

---

## 6. Insert, Delete, Access Operations

```cpp
list<int> L = {10, 20, 30};

// ── INSERT FRONT / BACK (O(1)) ──
L.push_back(40);    // L = 10, 20, 30, 40
L.push_front(5);    // L = 5, 10, 20, 30, 40

// ── ACCESS ENDS ──
cout << L.front();  // 5
cout << L.back();   // 40
// cout << L[2];    // ERROR! Lists don't have random access!

// ── DELETE FRONT / BACK (O(1)) ──
L.pop_front();
L.pop_back();

// ── INSERT IN MIDDLE (O(1) once iterator is there) ──
auto it = L.begin();
advance(it, 2);           // Moves iterator forward 2 steps
L.insert(it, 99);         // Inserts 99 BEFORE iterator

// ── ERASE ──
it = L.begin();
L.erase(it);              // Erases first element
L.remove(20);             // Removes ALL occurrences of value 20 (O(N))
```

---

## 7. List Iterators & Reversing

```cpp
list<int> L = {1, 2, 3, 4, 5};

// Forward Traversal
for (auto it = L.begin(); it != L.end(); ++it) {
    cout << *it << " ";
}

// Reverse Traversal Built-in!
for (auto it = L.rbegin(); it != L.rend(); ++it) {
    cout << *it << " ";
}
```

---

## 8. Advanced List Operations (Merge, Splice, Sort, Unique)

```cpp
list<int> L1 = {4, 1, 3};
list<int> L2 = {2, 7, 5};

// SORTING A LIST
// (You CANNOT use std::sort(L1.begin(), L1.end()) because no random access)
L1.sort();  // Built-in sort (O(N log N)) -> 1, 3, 4
L2.sort();  // 2, 5, 7

// MERGING (Both must be sorted first)
L1.merge(L2); // L1 becomes {1, 2, 3, 4, 5, 7}, L2 becomes empty!

// REMOVE DUPLICATES (Must be sorted first)
list<int> L3 = {1, 1, 2, 2, 2, 3};
L3.unique();  // L3 = {1, 2, 3}

// SPLICE (Cut & Paste whole lists O(1))
list<int> A = {1, 2};
list<int> B = {9, 10};
A.splice(A.end(), B);  // Moves all B elements to end of A. B is now empty.
```

---

# ═══════════════════════════════════
# PART C — SET & LIST PROBLEMS
# ═══════════════════════════════════

## 9. Remove Duplicates from Array (Using Set)

### 📝 Problem
Given an array, print the unique elements in sorted order.

### ✅ Solution
```cpp
#include <iostream>
#include <vector>
#include <set>
using namespace std;

int main() {
    vector<int> v = {4, 2, 4, 8, 2, 1, 9, 1};

    // 1-Line Solution: Insert vector into Set
    set<int> uniqueSorted(v.begin(), v.end());

    for (int x : uniqueSorted) {
        cout << x << " ";   // Output: 1 2 4 8 9
    }
    return 0;
}
```
> **Speed Trick:** If order doesn't matter, use `unordered_set` (O(N) instead of O(N log N)).

---

## 10. Find Common Elements in 3 Arrays

### 📝 Problem
Given three arrays, find elements that appear in all three.

### ✅ Solution
```cpp
#include <iostream>
#include <vector>
#include <set>
using namespace std;

void findCommon(vector<int> A, vector<int> B, vector<int> C) {
    set<int> setA(A.begin(), A.end());
    set<int> setB(B.begin(), B.end());
    set<int> common;

    // Check C against A and B
    for(int x : C) {
        if(setA.count(x) && setB.count(x)) {
            common.insert(x); // Prevents duplicate answers
        }
    }

    for(int ans : common) cout << ans << " ";
}

int main() {
    findCommon({1, 5, 10, 20}, {5, 10, 30}, {1, 5, 10, 40});
    // Output: 5 10
    return 0;
}
```

---

## 11. Check if Array is Subset of Another Array

### 📝 Problem
Given A1 and A2, Check if all elements of A2 exist in A1.

### ✅ Solution
```cpp
bool isSubset(vector<int>& A1, vector<int>& A2) {
    unordered_set<int> s(A1.begin(), A1.end());

    for (int x : A2) {
        if (s.count(x) == 0) return false; // Found a missing element!
    }
    return true;
}
```

---

## 12. First Missing Positive Integer

### 📝 Problem
Find the smallest positive integer missing from the array. `[3, 4, -1, 1]` -> Ans: `2`

### ✅ Solution
```cpp
int firstMissingPositive(vector<int>& nums) {
    unordered_set<int> s(nums.begin(), nums.end());

    int missing = 1;
    while (s.count(missing)) {
        missing++;  // Keep counting up until we find one not in the set
    }
    return missing;
}
```

---

## 13. Maintain Top K Elements (Using Set/Multiset)

### 📝 Problem
You have a stream of numbers. Keep track of the largest K elements.
*(Normally solved with Min-Heap, but Multiset works elegantly!)*

### ✅ Solution
```cpp
#include <iostream>
#include <set>
using namespace std;

void processStream(vector<int>& stream, int K) {
    multiset<int> topK;

    for (int x : stream) {
        topK.insert(x);
        if (topK.size() > K) {
            topK.erase(topK.begin()); // Remove the smallest element
        }
    }

    cout << "Top " << K << " elements are: ";
    for (int x : topK) cout << x << " ";
}
```

---

## 14. Implement a Queue using List

### 📝 Problem
Implement basic Queue operations (Push, Pop, Front) using `std::list`.

### ✅ Solution
```cpp
#include <list>
using namespace std;

class MyQueue {
    list<int> L;
public:
    void push(int val) { L.push_back(val); }    // Enqueue at end
    void pop() { if(!L.empty()) L.pop_front(); }// Dequeue from front
    int front() { return L.empty() ? -1 : L.front(); }
    bool isEmpty() { return L.empty(); }
};
```

---

## 15. Reverse a Linked List (Manual & STL)

### 📝 Problem
Reverse the elements.

### ✅ Solution (STL List)
```cpp
list<int> L = {1, 2, 3, 4};
L.reverse();  // Modifies L to {4, 3, 2, 1}
```

### ✅ Solution (Manual Node-based logic - Crucial for Interviews!)
```cpp
struct Node {
    int data;
    Node* next;
};

Node* reverseLinkedList(Node* head) {
    Node* prev = nullptr;
    Node* current = head;
    Node* nextNode = nullptr;

    while (current != nullptr) {
        nextNode = current->next;  // Save next
        current->next = prev;      // Reverse the pointer
        prev = current;            // Move prev forward
        current = nextNode;        // Move current forward
    }
    return prev; // New head
}
```

---

## 16. Detect Cycle in Linked List (Floyd's Algorithm)

### 📝 Problem
Find if a Linked list routes back to itself infinitely.

### ✅ Solution (Tortoise & Hare Trick)
```cpp
bool hasCycle(Node *head) {
    if (!head || !head->next) return false;

    Node* slow = head;
    Node* fast = head;

    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;          // Moves 1 step
        fast = fast->next->next;    // Moves 2 steps

        if (slow == fast) return true; // They met!
    }
    return false;
}
```

---

## 17. Find Middle of Linked List (Slow/Fast Pointer)

### 📝 Problem
Find the exact middle node of a linked list in ONE pass.

### ✅ Solution
```cpp
Node* findMiddle(Node* head) {
    Node* slow = head;
    Node* fast = head;

    // Fast moves 2x speed. When fast hits the end, slow is exactly in the middle!
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}
```

---

## 18. Merge Two Sorted Lists

### ✅ STL Solution
```cpp
list<int> L1 = {1, 3, 5};
list<int> L2 = {2, 4, 6};
L1.merge(L2); // L1: {1,2,3,4,5,6}, L2: empty
```

### ✅ Manual Node Solution
```cpp
Node* mergeTwoLists(Node* l1, Node* l2) {
    if (!l1) return l2;
    if (!l2) return l1;

    if (l1->data < l2->data) {
        l1->next = mergeTwoLists(l1->next, l2);
        return l1;
    } else {
        l2->next = mergeTwoLists(l1, l2->next);
        return l2;
    }
}
```

---

## 🚨 Final Checklist & Gotchas
*   **Vector out-of-bounds:** Vectors have `[i]`. `std::list` does **NOT**. Use iterators to access middle elements.
*   `set` removes duplicates and sorts automatically (O(logN) inserts).
*   `unordered_set` is incredibly fast (O(1)) but orders randomly. Use this by default for `visited` tracking or subsets.
*   **Linked lists problems** almost always use *Slow & Fast pointers* (Tortoise & Hare algorithm).

---
*Set & List Complete Guide | C++ Data Structures Preparedness*
