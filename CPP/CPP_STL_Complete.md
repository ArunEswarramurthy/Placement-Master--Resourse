# 📚 C++ STL — Complete Guide: Basics to Advanced
### Standard Template Library | From Zero to Expert 🚀

---

## 📌 TABLE OF CONTENTS

### BASICS
1. [What is STL? Why Use It?](#1-what-is-stl-why-use-it)
2. [STL Components Overview](#2-stl-components-overview)

### CONTAINERS
3. [vector — Dynamic Array](#3-vector--dynamic-array)
4. [array — Fixed-size Array](#4-array--fixed-size-array)
5. [list — Doubly Linked List](#5-list--doubly-linked-list)
6. [deque — Double-Ended Queue](#6-deque--double-ended-queue)
7. [stack — LIFO](#7-stack--lifo)
8. [queue — FIFO](#8-queue--fifo)
9. [priority_queue — Heap](#9-priority_queue--heap)
10. [set & multiset — Sorted Unique/Multi Values](#10-set--multiset--sorted-uniquemulti-values)
11. [map & multimap — Key-Value Sorted](#11-map--multimap--key-value-sorted)
12. [unordered_set — Hash Set](#12-unordered_set--hash-set)
13. [unordered_map — Hash Map](#13-unordered_map--hash-map)
14. [pair & tuple](#14-pair--tuple)

### ITERATORS
15. [Iterators — Moving Through Containers](#15-iterators--moving-through-containers)

### ALGORITHMS
16. [Sorting & Searching](#16-sorting--searching)
17. [Min, Max & Count](#17-min-max--count)
18. [Permutation & Combination Algorithms](#18-permutation--combination-algorithms)
19. [Numeric Algorithms](#19-numeric-algorithms)
20. [Modifying Algorithms (copy, fill, replace, remove)](#20-modifying-algorithms-copy-fill-replace-remove)

### ADVANCED
21. [Custom Comparators & Lambda](#21-custom-comparators--lambda)
22. [STL with Strings](#22-stl-with-strings)
23. [Advanced: Policy-Based Data Structures](#23-advanced-policy-based-data-structures)
24. [Competitive Programming Cheatsheet](#24-competitive-programming-cheatsheet)

---

## 1. What is STL? Why Use It?

**STL (Standard Template Library)** is a collection of **ready-to-use, generic** data structures and algorithms built into C++.

### Without STL vs With STL
```cpp
// WITHOUT STL — Manual linked list (50+ lines)
struct Node { int data; Node* next; };
// ... complex insert/delete code

// WITH STL — One line!
#include <list>
list<int> myList = {1, 2, 3, 4, 5};
myList.push_back(6);
```

### Why STL?
| Benefit | Detail |
|---|---|
| **Ready to use** | No need to implement data structures from scratch |
| **Optimized** | Industry-grade performance |
| **Generic** | Works with any data type using templates |
| **Consistent** | Same interface across all containers |
| **Saves time** | 10× faster coding in interviews |

---

## 2. STL Components Overview

```
STL
├── CONTAINERS  (store data)
│   ├── Sequence:    vector, array, list, deque
│   ├── Stack/Queue: stack, queue, priority_queue
│   └── Associative: set, map, multiset, multimap
│                    unordered_set, unordered_map
│
├── ITERATORS   (traverse containers like pointers)
│   ├── begin() / end()
│   ├── rbegin() / rend()  (reverse)
│   └── Types: input, output, forward, bidirectional, random access
│
└── ALGORITHMS  (operate on containers)
    ├── Sorting:  sort, stable_sort, partial_sort
    ├── Searching: find, binary_search, lower_bound, upper_bound
    ├── Counting: count, count_if
    ├── Numeric:  accumulate, partial_sum, iota
    └── Modifying: copy, fill, replace, remove, reverse
```

---

## 3. vector — Dynamic Array

📌 **Most used STL container!** Size changes dynamically.

```cpp
#include <vector>
using namespace std;
```

### Declaration & Initialization
```cpp
vector<int> v1;                        // Empty vector
vector<int> v2(5);                     // 5 elements, all 0
vector<int> v3(5, 10);                 // 5 elements, all 10
vector<int> v4 = {1, 2, 3, 4, 5};     // Initialized with values
vector<int> v5(v4);                    // Copy of v4
vector<vector<int>> matrix(3, vector<int>(3, 0));  // 2D vector 3×3
```

### Adding & Removing Elements
```cpp
vector<int> v = {1, 2, 3};

v.push_back(4);          // Add at END   → {1,2,3,4}
v.pop_back();             // Remove from END → {1,2,3}
v.insert(v.begin(), 0);  // Insert at position → {0,1,2,3}
v.insert(v.begin()+2, 99); // Insert at index 2 → {0,1,99,2,3}
v.erase(v.begin());       // Remove first element → {1,99,2,3}
v.erase(v.begin()+1, v.begin()+3);  // Remove range [1,3)
v.clear();                // Remove ALL elements → {}
```

### Accessing Elements
```cpp
vector<int> v = {10, 20, 30, 40, 50};

cout << v[2];        // 30 (no bounds check)
cout << v.at(2);     // 30 (with bounds check — safer)
cout << v.front();   // 10 (first element)
cout << v.back();    // 50 (last element)
int* ptr = v.data(); // Raw pointer to array
```

### Size & Capacity
```cpp
cout << v.size();       // Number of elements: 5
cout << v.capacity();   // Allocated memory (≥ size)
cout << v.empty();      // 0 (not empty)
v.resize(8);            // Resize to 8 (fills with 0)
v.resize(8, 99);        // Resize to 8 (fills with 99)
v.reserve(100);         // Reserve memory for 100 (avoids reallocation)
v.shrink_to_fit();      // Release unused memory
```

### Traversal
```cpp
vector<int> v = {1, 2, 3, 4, 5};

// 1. Index-based (classic)
for (int i = 0; i < v.size(); i++) cout << v[i] << " ";

// 2. Range-based (modern C++11) ← Prefer this!
for (int x : v) cout << x << " ";

// 3. Iterator
for (auto it = v.begin(); it != v.end(); it++) cout << *it << " ";

// 4. Reverse traversal
for (auto it = v.rbegin(); it != v.rend(); it++) cout << *it << " ";
```

### Sorting & Searching
```cpp
vector<int> v = {5, 3, 8, 1, 9, 2};

sort(v.begin(), v.end());               // Ascending: 1 2 3 5 8 9
sort(v.begin(), v.end(), greater<int>()); // Descending: 9 8 5 3 2 1

bool found = binary_search(v.begin(), v.end(), 5);  // true (if sorted)
auto it = find(v.begin(), v.end(), 8);               // iterator to 8
int idx = it - v.begin();                            // index = 4
```

### 2D Vector (Matrix)
```cpp
int rows = 3, cols = 4;
vector<vector<int>> mat(rows, vector<int>(cols, 0));

mat[1][2] = 5;

for (auto &row : mat) {
    for (int x : row) cout << x << " ";
    cout << endl;
}
```

---

## 4. array — Fixed-size Array

📌 Like C-array but with STL features. Size is known at compile time.

```cpp
#include <array>

array<int, 5> arr = {3, 1, 4, 1, 5};

cout << arr.size();     // 5 (compile-time constant)
cout << arr[0];         // 3
cout << arr.front();    // 3
cout << arr.back();     // 5

sort(arr.begin(), arr.end());   // 1 1 3 4 5
arr.fill(0);                    // Set all to 0
```

---

## 5. list — Doubly Linked List

📌 Fast insert/delete at any position. Slow random access.

```cpp
#include <list>

list<int> l = {3, 1, 4, 1, 5};

l.push_back(9);        // Add at end
l.push_front(0);       // Add at beginning
l.pop_back();          // Remove from end
l.pop_front();         // Remove from beginning

l.insert(l.begin(), 99);    // Insert at position
l.erase(l.begin());          // Remove at position

l.sort();              // Sort in place
l.reverse();           // Reverse in place
l.remove(1);           // Remove ALL elements equal to 1
l.unique();            // Remove consecutive duplicates

cout << l.size();
cout << l.front();
cout << l.back();
```

---

## 6. deque — Double-Ended Queue

📌 Fast insert/delete at **both** front and back. Supports random access.

```cpp
#include <deque>

deque<int> dq = {3, 1, 4};

dq.push_back(5);       // Add at back
dq.push_front(0);      // Add at front
dq.pop_back();         // Remove from back
dq.pop_front();        // Remove from front

cout << dq[1];         // Random access
cout << dq.at(1);      // With bounds check
cout << dq.front();
cout << dq.back();
cout << dq.size();
```

---

## 7. stack — LIFO

📌 **Last In, First Out**. Like a stack of plates.

```cpp
#include <stack>

stack<int> st;

st.push(10);    // Add on top
st.push(20);
st.push(30);

cout << st.top();    // 30 (peek top, don't remove)
st.pop();            // Remove top (30)
cout << st.top();    // 20

cout << st.size();   // 2
cout << st.empty();  // 0 (not empty)
```

### Classic Stack Uses
```cpp
// Check balanced brackets
bool isBalanced(string s) {
    stack<char> st;
    for (char c : s) {
        if (c=='(' || c=='[' || c=='{') st.push(c);
        else {
            if (st.empty()) return false;
            char top = st.top(); st.pop();
            if ((c==')' && top!='(') ||
                (c==']' && top!='[') ||
                (c=='}' && top!='{')) return false;
        }
    }
    return st.empty();
}
```

---

## 8. queue — FIFO

📌 **First In, First Out**. Like a real queue / line.

```cpp
#include <queue>

queue<int> q;

q.push(10);     // Add at back
q.push(20);
q.push(30);

cout << q.front();   // 10 (peek front)
cout << q.back();    // 30 (peek back)
q.pop();             // Remove front (10)
cout << q.front();   // 20

cout << q.size();    // 2
cout << q.empty();   // 0
```

---

## 9. priority_queue — Heap

📌 Always gives you the **maximum (or minimum)** element first.

```cpp
#include <queue>

// MAX HEAP (default) — largest element on top
priority_queue<int> pq;
pq.push(5); pq.push(1); pq.push(8); pq.push(3);

cout << pq.top();   // 8 (maximum!)
pq.pop();
cout << pq.top();   // 5

// MIN HEAP — smallest element on top
priority_queue<int, vector<int>, greater<int>> minpq;
minpq.push(5); minpq.push(1); minpq.push(8);
cout << minpq.top();   // 1 (minimum!)
```

### Priority Queue with pairs
```cpp
// Max heap by first element of pair
priority_queue<pair<int,int>> pq;
pq.push({3, "a"});
pq.push({1, "b"});
pq.push({5, "c"});
cout << pq.top().first;    // 5
```

---

## 10. set & multiset — Sorted Unique/Multi Values

### set — Unique sorted elements
```cpp
#include <set>

set<int> s = {5, 3, 1, 4, 1, 2};  // Duplicates removed!
// s = {1, 2, 3, 4, 5}  ← auto sorted!

s.insert(6);           // {1,2,3,4,5,6}
s.insert(3);           // No effect (already exists)
s.erase(4);            // {1,2,3,5,6}

cout << s.count(3);    // 1 (exists) or 0 (not exists)
cout << s.size();      // 5

// Find
auto it = s.find(3);
if (it != s.end()) cout << "Found!";

// lower_bound: first element ≥ x
auto lb = s.lower_bound(3);   // points to 3
// upper_bound: first element > x
auto ub = s.upper_bound(3);   // points to 5

// Traverse (always sorted order!)
for (int x : s) cout << x << " ";    // 1 2 3 5 6
```

### multiset — Allows duplicates, sorted
```cpp
#include <set>

multiset<int> ms = {3, 1, 3, 2, 1, 3};
// ms = {1, 1, 2, 3, 3, 3}

ms.insert(4);
ms.erase(ms.find(3));    // Remove ONLY ONE 3
ms.erase(3);             // Remove ALL 3s

cout << ms.count(3);     // Count occurrences
```

---

## 11. map & multimap — Key-Value Sorted

### map — Unique keys, sorted by key
```cpp
#include <map>

map<string, int> marks;
marks["Arjun"] = 95;
marks["Priya"] = 88;
marks["Ravi"]  = 76;
marks["Priya"] = 90;    // Overwrites (key must be unique!)

// Access
cout << marks["Arjun"];       // 95
cout << marks.at("Priya");    // 90 (with bounds check)

// Check if key exists
if (marks.count("Ravi")) cout << "Ravi exists!";
if (marks.find("Ravi") != marks.end()) cout << "Found!";

// Insert
marks.insert({"Kiran", 85});
marks.insert(make_pair("Anjali", 92));

// Delete
marks.erase("Priya");

// Size
cout << marks.size();    // 3

// Traverse (always sorted by key!)
for (auto &p : marks) {
    cout << p.first << " → " << p.second << endl;
}

// Using structured bindings (C++17)
for (auto &[name, score] : marks) {
    cout << name << " → " << score << endl;
}
```

### Frequency Count (Most Common Pattern!)
```cpp
string s = "programming";
map<char, int> freq;
for (char c : s) freq[c]++;    // Count each character

for (auto &[ch, cnt] : freq)
    cout << ch << ": " << cnt << endl;
```

### multimap — Multiple values for same key
```cpp
#include <map>

multimap<int, string> mm;
mm.insert({1, "Apple"});
mm.insert({2, "Banana"});
mm.insert({1, "Avocado"});   // Key 1 again!

// Find all values for key 1
auto range = mm.equal_range(1);
for (auto it = range.first; it != range.second; it++)
    cout << it->second << endl;   // Apple, Avocado
```

---

## 12. unordered_set — Hash Set

📌 Like `set` but **NOT sorted** → faster (O(1) average lookup vs O(log n) for set).

```cpp
#include <unordered_set>

unordered_set<int> us = {3, 1, 4, 1, 5};  // Duplicates removed, NOT sorted
// us = {5, 4, 1, 3} or any order — NOT guaranteed sorted!

us.insert(9);
us.erase(1);
cout << us.count(3);    // 1 (found) or 0 (not found)

// When to use unordered_set vs set?
// unordered_set → when order doesn't matter (faster)
// set → when sorted order is needed
```

---

## 13. unordered_map — Hash Map

📌 Like `map` but **NOT sorted by key** → faster O(1) average.

```cpp
#include <unordered_map>

unordered_map<string, int> um;
um["apple"] = 5;
um["banana"] = 3;
um["orange"] = 7;

cout << um["apple"];        // 5
cout << um.count("banana"); // 1 (exists)

um.erase("orange");
cout << um.size();          // 2

// Traverse (order NOT guaranteed)
for (auto &[key, val] : um)
    cout << key << ": " << val << endl;
```

### map vs unordered_map
| Feature | map | unordered_map |
|---|---|---|
| Order | Sorted by key | Not sorted |
| Lookup time | O(log n) | O(1) average |
| Insert time | O(log n) | O(1) average |
| Memory | Less | More |
| Use when | Need sorted keys | Need fast access |

---

## 14. pair & tuple

### pair — Store two values
```cpp
#include <utility>

pair<int, string> p = {1, "Hello"};
cout << p.first;     // 1
cout << p.second;    // Hello

// Using make_pair
auto p2 = make_pair(3.14, 'A');

// Swap
p.swap(p2);

// Sorting vector of pairs (sorts by first, then second)
vector<pair<int,string>> v = {{3,"c"},{1,"a"},{2,"b"}};
sort(v.begin(), v.end());
// Result: (1,a), (2,b), (3,c)
```

### tuple — Store multiple values (any count)
```cpp
#include <tuple>

tuple<int, string, double> t = {1, "Alice", 9.5};
cout << get<0>(t);    // 1
cout << get<1>(t);    // Alice
cout << get<2>(t);    // 9.5

// C++17 structured bindings
auto [id, name, score] = t;
cout << name;         // Alice

// make_tuple
auto t2 = make_tuple(42, "Bob", 7.8);
```

---

## 15. Iterators — Moving Through Containers

📌 Iterators are like **smart pointers** that traverse containers.

```cpp
vector<int> v = {10, 20, 30, 40, 50};

// begin() → points to first element
// end()   → points ONE PAST last element

auto it = v.begin();
cout << *it;      // 10 (dereference)
it++;
cout << *it;      // 20
it += 2;
cout << *it;      // 40

// Reverse iterators
for (auto it = v.rbegin(); it != v.rend(); it++)
    cout << *it << " ";    // 50 40 30 20 10
```

### Iterator Types

| Type | Supports | Examples |
|---|---|---|
| Input | Read only, forward | istream_iterator |
| Output | Write only, forward | ostream_iterator |
| Forward | Read/Write, forward | forward_list |
| Bidirectional | Read/Write, both directions | list, set, map |
| Random Access | Direct access (+ − []) | vector, deque, array |

```cpp
// auto keyword for iterators (cleaner)
for (auto it = v.begin(); it != v.end(); ++it)
    cout << *it;

// Even cleaner: range-based for loop
for (auto &x : v)
    cout << x;
```

---

## 16. Sorting & Searching

```cpp
#include <algorithm>
#include <vector>
```

### Sorting
```cpp
vector<int> v = {5, 2, 8, 1, 9, 3, 7};

// Ascending (default)
sort(v.begin(), v.end());                          // 1 2 3 5 7 8 9

// Descending
sort(v.begin(), v.end(), greater<int>());          // 9 8 7 5 3 2 1

// Sort partial range (first 4 elements)
sort(v.begin(), v.begin() + 4);

// Stable sort (preserves relative order of equal elements)
stable_sort(v.begin(), v.end());

// Partial sort (smallest 3 at front)
partial_sort(v.begin(), v.begin() + 3, v.end());

// Check if sorted
bool sorted = is_sorted(v.begin(), v.end());       // true or false
```

### Searching
```cpp
vector<int> v = {1, 2, 3, 5, 7, 8, 9};  // Must be sorted for binary search!

// Linear search
auto it = find(v.begin(), v.end(), 5);
if (it != v.end()) cout << "Found at: " << (it - v.begin());

// Binary search (returns bool)
bool found = binary_search(v.begin(), v.end(), 5);   // true

// lower_bound: first position where value ≥ x
auto lb = lower_bound(v.begin(), v.end(), 5);   // points to 5 (index 3)

// upper_bound: first position where value > x
auto ub = upper_bound(v.begin(), v.end(), 5);   // points to 7 (index 4)

// Count elements in range [3, 7)
int cnt = upper_bound(v.begin(),v.end(),7) - lower_bound(v.begin(),v.end(),3);
```

---

## 17. Min, Max & Count

```cpp
vector<int> v = {5, 2, 8, 1, 9, 3};

// Min and Max values
int mx = *max_element(v.begin(), v.end());    // 9
int mn = *min_element(v.begin(), v.end());    // 1

// Min and Max of two values
int a = max(3, 7);        // 7
int b = min(3, 7);        // 3
auto [lo, hi] = minmax(3, 7);   // lo=3, hi=7

// Position of min/max
auto maxIt = max_element(v.begin(), v.end());
cout << maxIt - v.begin();   // Index of max = 4

// Count occurrences
int cnt = count(v.begin(), v.end(), 5);         // 1

// Count with condition
int evenCnt = count_if(v.begin(), v.end(), [](int x){ return x%2==0; });
```

---

## 18. Permutation & Combination Algorithms

```cpp
vector<int> v = {1, 2, 3};

// Generate next permutation
do {
    for (int x : v) cout << x << " ";
    cout << endl;
} while (next_permutation(v.begin(), v.end()));
// Output: all 6 permutations of {1,2,3}

// Previous permutation
prev_permutation(v.begin(), v.end());

// Check if permutation
vector<int> a = {1,2,3}, b = {3,1,2};
bool isPerm = is_permutation(a.begin(), a.end(), b.begin());  // true
```

---

## 19. Numeric Algorithms

```cpp
#include <numeric>

vector<int> v = {1, 2, 3, 4, 5};

// Sum (accumulate)
int sum = accumulate(v.begin(), v.end(), 0);      // 0+1+2+3+4+5 = 15

// Product
int prod = accumulate(v.begin(), v.end(), 1, multiplies<int>());  // 120

// Partial sum
vector<int> ps(v.size());
partial_sum(v.begin(), v.end(), ps.begin());   // ps = {1,3,6,10,15}

// Fill with sequence (iota)
vector<int> seq(5);
iota(seq.begin(), seq.end(), 1);   // seq = {1,2,3,4,5}
iota(seq.begin(), seq.end(), 0);   // seq = {0,1,2,3,4}

// GCD and LCM (C++17)
#include <numeric>
cout << gcd(12, 18);    // 6
cout << lcm(4, 6);      // 12

// Inner product (dot product)
vector<int> a={1,2,3}, b={4,5,6};
int dot = inner_product(a.begin(), a.end(), b.begin(), 0);   // 1*4+2*5+3*6 = 32
```

---

## 20. Modifying Algorithms (copy, fill, replace, remove)

```cpp
vector<int> v = {1, 2, 3, 4, 5};
vector<int> dest(5);

// Copy
copy(v.begin(), v.end(), dest.begin());    // Copy entire vector
copy(v.begin(), v.begin()+3, dest.begin()); // Copy first 3

// Fill
fill(v.begin(), v.end(), 0);              // {0,0,0,0,0}
fill_n(v.begin(), 3, 9);                  // {9,9,9,0,0}

// Replace
replace(v.begin(), v.end(), 9, 1);        // Replace all 9s with 1
replace_if(v.begin(), v.end(), [](int x){ return x%2==0; }, 0);  // Replace evens with 0

// Remove (doesn't actually erase — use with erase!)
auto it = remove(v.begin(), v.end(), 3);  // Remove all 3s (logical)
v.erase(it, v.end());                      // Actually erase them

// Remove duplicates (must be sorted first!)
sort(v.begin(), v.end());
auto last = unique(v.begin(), v.end());
v.erase(last, v.end());

// Reverse
reverse(v.begin(), v.end());

// Rotate
rotate(v.begin(), v.begin()+2, v.end());   // Move first 2 to end

// Shuffle (random)
#include <algorithm>
#include <random>
auto rng = default_random_engine{};
shuffle(v.begin(), v.end(), rng);

// Transform (apply function to each element)
transform(v.begin(), v.end(), v.begin(), [](int x){ return x*2; }); // Double each
```

---

## 21. Custom Comparators & Lambda

### Lambda basics
```cpp
// [capture](params) -> return_type { body }
auto square = [](int x) { return x * x; };
cout << square(5);    // 25

// Capture variable from scope
int factor = 3;
auto multiply = [factor](int x) { return x * factor; };
cout << multiply(4);   // 12

// Capture all by value [=] or by reference [&]
auto addFactor = [&factor](int x) { return x + factor; };
```

### Custom Sort with Lambda
```cpp
vector<pair<int,string>> v = {{3,"c"},{1,"a"},{2,"b"}};

// Sort by second element (alphabetically)
sort(v.begin(), v.end(), [](auto &a, auto &b){
    return a.second < b.second;
});

// Sort descending by first element
sort(v.begin(), v.end(), [](auto &a, auto &b){
    return a.first > b.first;
});
```

### Custom Comparator for set/map
```cpp
// Custom comparator struct
struct Descending {
    bool operator()(int a, int b) const { return a > b; }
};

set<int, Descending> s = {3, 1, 5, 2};
// s = {5, 3, 2, 1}  ← sorted descending!

// Map with custom key comparator
map<int, string, Descending> m;
m[3] = "three"; m[1] = "one"; m[5] = "five";
// Iterates in descending key order
```

---

## 22. STL with Strings

```cpp
#include <string>
#include <algorithm>
#include <sstream>

string s = "hello world";

// Sort characters
sort(s.begin(), s.end());                  // " dehllloorw"

// Reverse
reverse(s.begin(), s.end());

// Count specific char
int cnt = count(s.begin(), s.end(), 'l'); // 3

// Convert all to uppercase
transform(s.begin(), s.end(), s.begin(), ::toupper);

// Check if palindrome
bool isPalin = equal(s.begin(), s.begin() + s.size()/2, s.rbegin());

// Split string by delimiter using stringstream
string line = "10 20 30 40";
stringstream ss(line);
int num;
vector<int> nums;
while (ss >> num) nums.push_back(num);   // nums = {10,20,30,40}

// Join vector to string
vector<string> words = {"Hello", "World"};
string result = "";
for (int i=0; i<words.size(); i++) {
    result += words[i];
    if (i < words.size()-1) result += " ";
}

// Find and replace
string str = "Hello World";
size_t pos = str.find("World");
if (pos != string::npos) str.replace(pos, 5, "C++");
// Result: "Hello C++"
```

---

## 23. Advanced: Policy-Based Data Structures

📌 **Order Statistics Tree** — Built using GCC extension. Supports O(log n) rank queries.

```cpp
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;

typedef tree<int, null_type, less<int>, rb_tree_tag,
             tree_order_statistics_node_update> ordered_set;

ordered_set os;
os.insert(5); os.insert(1); os.insert(3); os.insert(7);

// Find k-th smallest (0-indexed)
cout << *os.find_by_order(0);    // 1 (smallest)
cout << *os.find_by_order(2);    // 5 (3rd smallest)

// Find rank of element (0-indexed)
cout << os.order_of_key(3);      // 1 (rank of 3)
cout << os.order_of_key(6);      // 3 (how many elements < 6)
```

---

## 24. Competitive Programming Cheatsheet

### Must-Know Patterns

#### Pattern 1 — Sliding Window Max using deque
```cpp
// Maximum in every window of size k
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq;  // stores indices
    vector<int> result;
    for (int i = 0; i < nums.size(); i++) {
        while (!dq.empty() && dq.front() <= i - k) dq.pop_front();
        while (!dq.empty() && nums[dq.back()] <= nums[i]) dq.pop_back();
        dq.push_back(i);
        if (i >= k-1) result.push_back(nums[dq.front()]);
    }
    return result;
}
```

#### Pattern 2 — Two Pointers / Frequency using map
```cpp
// Longest substring without repeating characters
int maxLen(string s) {
    unordered_map<char, int> freq;
    int left = 0, maxL = 0;
    for (int right = 0; right < s.size(); right++) {
        freq[s[right]]++;
        while (freq[s[right]] > 1) { freq[s[left]]--; left++; }
        maxL = max(maxL, right - left + 1);
    }
    return maxL;
}
```

#### Pattern 3 — Top K elements using priority_queue
```cpp
vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int,int> freq;
    for (int x : nums) freq[x]++;
    priority_queue<pair<int,int>> pq;
    for (auto &[val, cnt] : freq) pq.push({cnt, val});
    vector<int> result;
    for (int i = 0; i < k; i++) { result.push_back(pq.top().second); pq.pop(); }
    return result;
}
```

#### Pattern 4 — Coordinate Compression using map/set
```cpp
vector<int> v = {100, 500, 200, 300};
// Compress to ranks 0,1,2,3
sort(v.begin(), v.end());
v.erase(unique(v.begin(), v.end()), v.end());
map<int,int> compress;
for (int i = 0; i < v.size(); i++) compress[v[i]] = i;
```

#### Pattern 5 — BFS using queue
```cpp
void bfs(int start, vector<vector<int>>& adj) {
    queue<int> q;
    vector<bool> visited(adj.size(), false);
    q.push(start);
    visited[start] = true;
    while (!q.empty()) {
        int node = q.front(); q.pop();
        cout << node << " ";
        for (int nbr : adj[node]) {
            if (!visited[nbr]) { visited[nbr]=true; q.push(nbr); }
        }
    }
}
```

---

### Quick Reference Table

| Container | Header | Access | Insert | Delete | Search |
|---|---|---|---|---|---|
| vector | `<vector>` | O(1) | O(1) end | O(n) | O(n) |
| list | `<list>` | O(n) | O(1) | O(1) | O(n) |
| deque | `<deque>` | O(1) | O(1) both ends | O(n) mid | O(n) |
| stack | `<stack>` | O(1) top | O(1) | O(1) | — |
| queue | `<queue>` | O(1) front | O(1) | O(1) | — |
| priority_queue | `<queue>` | O(1) top | O(log n) | O(log n) | — |
| set | `<set>` | O(log n) | O(log n) | O(log n) | O(log n) |
| map | `<map>` | O(log n) | O(log n) | O(log n) | O(log n) |
| unordered_set | `<unordered_set>` | O(1) avg | O(1) avg | O(1) avg | O(1) avg |
| unordered_map | `<unordered_map>` | O(1) avg | O(1) avg | O(1) avg | O(1) avg |

---

### All Required Headers

```cpp
#include <vector>
#include <list>
#include <deque>
#include <array>
#include <stack>
#include <queue>        // queue, priority_queue
#include <set>          // set, multiset
#include <map>          // map, multimap
#include <unordered_set>
#include <unordered_map>
#include <algorithm>    // sort, find, reverse, binary_search, etc.
#include <numeric>      // accumulate, gcd, lcm, iota
#include <utility>      // pair, make_pair, swap
#include <tuple>        // tuple, make_tuple, get
#include <string>       // string operations
#include <sstream>      // stringstream
#include <functional>   // greater<>, less<>, multiplies<>
#include <iterator>     // iterators
#include <climits>      // INT_MAX, INT_MIN, LLONG_MAX
```

### Or just use:
```cpp
#include <bits/stdc++.h>   // Includes EVERYTHING (use in CP only!)
using namespace std;
```

---

### Complexity Quick Reference

```
sort()          → O(n log n)
binary_search() → O(log n)   [must be sorted]
lower_bound()   → O(log n)   [must be sorted]
find()          → O(n)
count()         → O(n)
accumulate()    → O(n)
max_element()   → O(n)
next_permutation() → O(n)
```

---

> **✅ You now know C++ STL from Basics to Advanced!**
>
> **Practice Order:**
> 1. vector → map → set (master these 3 first)
> 2. priority_queue → stack → queue
> 3. unordered_map → unordered_set (for speed)
> 4. Algorithms: sort, lower_bound, accumulate
> 5. Custom comparators + Lambda
> 6. Competitive patterns

---
*C++ STL Complete Guide | Made for TCS NQT & Competitive Programming*
