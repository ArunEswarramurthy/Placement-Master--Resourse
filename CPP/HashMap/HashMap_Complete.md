# 🗺️ HASHMAP — Complete Guide + Problems
### Learn HashMap from Zero → Hero | Basics + 13 Must-Know Problems 🚀

---

## 📌 TABLE OF CONTENTS

### PART A — HASHMAP BASICS
1. [What is a HashMap? How Does it Work?](#1-what-is-a-hashmap-how-does-it-work)
2. [map vs unordered_map vs multimap](#2-map-vs-unordered_map-vs-multimap)
3. [Declaring & Initializing](#3-declaring--initializing)
4. [Insert, Access, Update, Delete](#4-insert-access-update-delete)
5. [Traversal Techniques](#5-traversal-techniques)
6. [Searching & Checking](#6-searching--checking)
7. [HashMap with Custom Keys](#7-hashmap-with-custom-keys)
8. [HashMap Operations Cheatsheet](#8-hashmap-operations-cheatsheet)

### PART B — HASHMAP PROBLEMS
9. [Frequency Count of Array Elements](#9-frequency-count-of-array-elements)
10. [Two Sum](#10-two-sum)
11. [Find Subarrays with Zero Sum](#11-find-subarrays-with-zero-sum)
12. [Longest Consecutive Sequence](#12-longest-consecutive-sequence)
13. [Group Anagrams Together](#13-group-anagrams-together)
14. [First Non-Repeating Element](#14-first-non-repeating-element)
15. [Majority Element (> N/2 times)](#15-majority-element--n2-times)
16. [Subarray with Given Sum (Prefix Sum)](#16-subarray-with-given-sum-prefix-sum)
17. [Count Distinct Elements in Every Window](#17-count-distinct-elements-in-every-window)
18. [4Sum Count (4 Arrays)](#18-4sum-count-4-arrays)
19. [Clone a Linked List with Random Pointer](#19-clone-a-linked-list-with-random-pointer)
20. [Intersection of Two Arrays](#20-intersection-of-two-arrays)
21. [Word Frequency in a Sentence](#21-word-frequency-in-a-sentence)

---

# ═══════════════════════════════════
# PART A — HASHMAP BASICS
# ═══════════════════════════════════

## 1. What is a HashMap? How Does it Work?

A **HashMap** stores **key→value pairs** and allows O(1) average-time lookup, insert, and delete.

```
KEY       →   Hash Function   →   BUCKET INDEX   →   VALUE
"apple"   →   hash("apple")   →       3          →     5
"banana"  →   hash("banana")  →       7          →     3
```

### How Hashing Works Internally
```
1. Compute hash(key) → get bucket index
2. Store (key, value) in that bucket
3. If two keys map to same bucket → "collision" → handled via chaining or probing
```

### Why Use HashMap?
| Operation | Array | Sorted Array | HashMap |
|---|---|---|---|
| Search | O(n) | O(log n) | **O(1) avg** |
| Insert | O(1) | O(n) | **O(1) avg** |
| Delete | O(n) | O(n) | **O(1) avg** |

> **Golden Rule:** When you need fast lookup → **use HashMap!**
> When you need sorted order → **use map (BST-based)**

---

## 2. map vs unordered_map vs multimap

| Feature | `map` | `unordered_map` | `multimap` |
|---|---|---|---|
| Header | `<map>` | `<unordered_map>` | `<map>` |
| Key order | **Sorted** (BST) | Not sorted | **Sorted** |
| Duplicate keys | ❌ No | ❌ No | ✅ Yes |
| Lookup time | O(log n) | **O(1) avg** | O(log n) |
| Memory | Less | More | Less |
| Best for | Sorted keys needed | Fast lookup | Multiple values/key |

```cpp
map<string,int>           m;    // Sorted keys, unique
unordered_map<string,int> um;   // Unsorted, unique, FASTEST
multimap<string,int>      mm;   // Sorted keys, duplicates allowed
```

---

## 3. Declaring & Initializing

```cpp
#include <map>
#include <unordered_map>
using namespace std;

// map — sorted by key
map<string, int> marks;
map<int, string> idToName;
map<char, int>   charFreq;

// unordered_map — fastest, no order
unordered_map<string, int> wordCount;
unordered_map<int, bool>   visited;

// Initialize with values
map<string, int> m = {
    {"Alice", 95},
    {"Bob",   88},
    {"Carol", 92}
};

// Nested map
map<string, map<string, int>> grades;
grades["Alice"]["Math"] = 95;
grades["Alice"]["Science"] = 88;
```

---

## 4. Insert, Access, Update, Delete

```cpp
map<string, int> m;

// ─── INSERT ───────────────────────────────────
m["apple"] = 5;                         // Using []
m.insert({"banana", 3});                // Using insert()
m.insert(make_pair("cherry", 7));       // Using make_pair
m.emplace("date", 4);                   // Most efficient — constructs in-place

// ─── ACCESS ───────────────────────────────────
cout << m["apple"];                     // 5  (creates key if not found!)
cout << m.at("apple");                  // 5  (throws exception if not found)

// ─── UPDATE ───────────────────────────────────
m["apple"] = 10;                        // Direct reassignment
m["apple"]++;                           // Increment
m["apple"] += 5;                        // Add to existing

// ─── DELETE ───────────────────────────────────
m.erase("banana");                      // Remove by key
m.erase(m.begin());                     // Remove by iterator
m.erase(m.begin(), m.end());            // Remove range
m.clear();                              // Remove ALL

// ─── SIZE ─────────────────────────────────────
cout << m.size();                       // Number of key-value pairs
cout << m.empty();                      // True if empty
```

> ⚠️ **CRITICAL:** `m["key"]` **creates** the key with default value (0) if it doesn't exist!
> Use `m.count("key")` or `m.find("key")` to CHECK first.

---

## 5. Traversal Techniques

```cpp
map<string, int> m = {{"Alice",95}, {"Bob",88}, {"Carol",92}};

// ── Method 1: Range-based for with pair ──
for (auto &p : m)
    cout << p.first << " → " << p.second << "\n";

// ── Method 2: Structured bindings (C++17) ← BEST ──
for (auto &[name, score] : m)
    cout << name << " → " << score << "\n";

// ── Method 3: Iterator ──
for (auto it = m.begin(); it != m.end(); ++it)
    cout << it->first << " → " << it->second << "\n";

// ── Method 4: Reverse traversal ──
for (auto it = m.rbegin(); it != m.rend(); ++it)
    cout << it->first << " → " << it->second << "\n";

// ── Keys only ──
for (auto &[k, v] : m) cout << k << " ";

// ── Values only ──
for (auto &[k, v] : m) cout << v << " ";
```

---

## 6. Searching & Checking

```cpp
map<string, int> m = {{"Alice",95}, {"Bob",88}};

// ── CHECK IF KEY EXISTS ──────────────────────────
// Method 1: count() → 0 or 1 (always use this!)
if (m.count("Alice"))          cout << "Found!";
if (m.count("Charlie") == 0)   cout << "Not found!";

// Method 2: find() → returns iterator
auto it = m.find("Alice");
if (it != m.end()) {
    cout << "Found: " << it->second;    // Avoid second lookup!
} else {
    cout << "Not found!";
}

// Method 3: contains() — C++20 only
if (m.contains("Alice")) cout << "Found!";    // C++20

// ── BOUNDS (only for sorted map) ────────────────
auto lb = m.lower_bound("B");   // First key >= "B"
auto ub = m.upper_bound("B");   // First key >  "B"

// ── GET OR DEFAULT ──────────────────────────────
// Safe access with default (doesn't insert!)
int score = m.count("Dave") ? m["Dave"] : 0;
```

---

## 7. HashMap with Custom Keys

```cpp
// Using pair as key in unordered_map (needs custom hash)
struct PairHash {
    size_t operator()(const pair<int,int>& p) const {
        return hash<int>()(p.first) ^ (hash<int>()(p.second) << 1);
    }
};
unordered_map<pair<int,int>, int, PairHash> grid;
grid[{0, 0}] = 1;
grid[{1, 2}] = 5;

// Using string key (naturally hashable)
unordered_map<string, vector<int>> adjList;
adjList["A"] = {1, 2, 3};
adjList["B"].push_back(4);

// map with pair key (works naturally — pair has built-in <)
map<pair<int,int>, string> coords;
coords[{0, 0}] = "Origin";
coords[{1, 2}] = "Point A";
```

---

## 8. HashMap Operations Cheatsheet

```cpp
// DECLARE
map<K,V> m;            unordered_map<K,V> um;

// INSERT
m[key] = val;          m.insert({key,val});     m.emplace(key,val);

// ACCESS
m[key]                 m.at(key)               // [] creates if missing, at() throws

// CHECK
m.count(key)           m.find(key) != m.end()  m.contains(key) // C++20

// DELETE
m.erase(key)           m.erase(it)             m.clear()

// SIZE
m.size()               m.empty()

// TRAVERSE
for(auto &[k,v]:m){}   for(auto it=m.begin();it!=m.end();++it){}

// FREQUENCY PATTERN
for(auto x:arr) freq[x]++;

// MULTIMAP
mm.insert({key,val});
mm.equal_range(key);   // All values for a key
mm.count(key);         // How many entries for this key
```

---

# ═══════════════════════════════════
# PART B — HASHMAP PROBLEMS
# ═══════════════════════════════════

## 9. Frequency Count of Array Elements

### 📝 Problem
Count how many times each element appears in an array.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `{1,2,2,3,3,3}` | 1→1, 2→2, 3→3 |
| 2 | `{5,5,5,5}` | 5→4 |
| 3 | `{1,2,3,4}` | all→1 |
| 4 | `{7,7,3,3,7}` | 7→3, 3→2 |
| 5 | `{}` | (none) |

### ✅ Without STL
```cpp
void freqCount(int arr[], int n) {
    int freq[1001] = {0};           // Assuming values 0-1000
    for (int i = 0; i < n; i++) freq[arr[i]]++;
    for (int i = 0; i <= 1000; i++)
        if (freq[i] > 0) cout << i << " → " << freq[i] << "\n";
}
```

### ✅ With STL
```cpp
void freqCount(vector<int>& v) {
    unordered_map<int,int> freq;
    for (int x : v) freq[x]++;
    for (auto &[val, cnt] : freq)
        cout << val << " → " << cnt << "\n";
}
```

> 💡 **This is the most fundamental HashMap pattern — used in almost every problem!**

---

## 10. Two Sum

### 📝 Problem
Find indices of two numbers that add up to target.

### 🧪 Test Cases
| # | Array | Target | Answer |
|---|---|---|---|
| 1 | `{2,7,11,15}` | 9 | [0,1] |
| 2 | `{3,2,4}` | 6 | [1,2] |
| 3 | `{3,3}` | 6 | [0,1] |
| 4 | `{1,5,3,7}` | 8 | [1,2] |
| 5 | `{-3,4,1}` | 1 | [0,1] |

### ✅ Without STL (O(n²))
```cpp
pair<int,int> twoSum(int arr[], int n, int target) {
    for (int i = 0; i < n; i++)
        for (int j = i+1; j < n; j++)
            if (arr[i] + arr[j] == target)
                return {i, j};
    return {-1, -1};
}
```

### ✅ With STL HashMap (O(n))
```cpp
pair<int,int> twoSum(vector<int>& v, int target) {
    unordered_map<int,int> seen;   // value → index
    for (int i = 0; i < v.size(); i++) {
        int need = target - v[i];
        if (seen.count(need))
            return {seen[need], i};
        seen[v[i]] = i;
    }
    return {-1, -1};
}
```

> 💡 **Key:** For each element, ask "have I seen `target - element` before?" One-pass O(n)!

---

## 11. Find Subarrays with Zero Sum

### 📝 Problem
Find if there exists a subarray with sum = 0 (or count all such subarrays).

### 🧪 Test Cases
| # | Input | Has Zero-Sum Subarray? |
|---|---|---|
| 1 | `{4,2,-3,1,6}` | Yes ✅ (2,-3,1) |
| 2 | `{4,2,0,1,6}` | Yes ✅ (0 itself) |
| 3 | `{1,2,3}` | No ❌ |
| 4 | `{-1,2,-1}` | Yes ✅ |
| 5 | `{3,4,-7,1,2}` | Yes ✅ |

### ✅ Without STL (O(n²))
```cpp
bool hasZeroSum(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        int sum = 0;
        for (int j = i; j < n; j++) {
            sum += arr[j];
            if (sum == 0) return true;
        }
    }
    return false;
}
```

### ✅ With STL HashMap (Prefix Sum — O(n))
```cpp
bool hasZeroSum(vector<int>& v) {
    unordered_set<int> prefixSums;
    prefixSums.insert(0);    // Empty subarray prefix
    int sum = 0;
    for (int x : v) {
        sum += x;
        if (prefixSums.count(sum)) return true;   // Seen this prefix before!
        prefixSums.insert(sum);
    }
    return false;
}
// Count of subarrays with sum K:
int countSubarraysWithSumK(vector<int>& v, int k) {
    unordered_map<int,int> freq;
    freq[0] = 1;
    int sum = 0, count = 0;
    for (int x : v) {
        sum += x;
        count += freq[sum - k];   // How many prefixes give sum-k?
        freq[sum]++;
    }
    return count;
}
```

> 💡 **Prefix Sum + HashMap is one of the most powerful interview patterns!**
> If prefix[j] == prefix[i], then subarray [i+1..j] has sum = 0.

---

## 12. Longest Consecutive Sequence

### 📝 Problem
Find the length of the longest sequence of consecutive integers.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `{100,4,200,1,3,2}` | 4 (1,2,3,4) |
| 2 | `{0,3,7,2,5,8,4,6,0,1}` | 9 (0–8) |
| 3 | `{1}` | 1 |
| 4 | `{1,2,3,4,5}` | 5 |
| 5 | `{5,5,5}` | 1 |

### ✅ Without STL (Sort — O(n log n))
```cpp
int longestConsecutive(int arr[], int n) {
    sort(arr, arr+n);
    int maxLen = 1, curLen = 1;
    for (int i = 1; i < n; i++) {
        if (arr[i] == arr[i-1]) continue;   // Skip duplicates
        if (arr[i] == arr[i-1]+1) curLen++;
        else curLen = 1;
        maxLen = max(maxLen, curLen);
    }
    return maxLen;
}
```

### ✅ With STL HashMap (O(n))
```cpp
int longestConsecutive(vector<int>& v) {
    unordered_set<int> s(v.begin(), v.end());   // All elements in hash set
    int maxLen = 0;
    for (int n : s) {
        // Only start counting from the BEGINNING of a streak
        if (!s.count(n - 1)) {
            int cur = n, len = 1;
            while (s.count(cur + 1)) { cur++; len++; }
            maxLen = max(maxLen, len);
        }
    }
    return maxLen;
}
```

> 💡 **Key:** Only start counting from numbers where `n-1` is NOT in set (start of streak). O(n) guaranteed!

---

## 13. Group Anagrams Together

### 📝 Problem
Group words that are anagrams of each other.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `["eat","tea","tan","ate","nat","bat"]` | `[eat,tea,ate][tan,nat][bat]` |
| 2 | `[""]` | `[[""]]` |
| 3 | `["a"]` | `[["a"]]` |
| 4 | `["abc","bca","cab","xyz"]` | `[abc,bca,cab][xyz]` |
| 5 | `["ab","ba","cd","dc"]` | `[ab,ba][cd,dc]` |

### ✅ Without STL
```cpp
// Sort each word → same sorted form = anagram group
// Use a nested array approach (complex without map)
// Better done with STL below
```

### ✅ With STL HashMap
```cpp
vector<vector<string>> groupAnagrams(vector<string>& words) {
    unordered_map<string, vector<string>> groups;
    for (string& w : words) {
        string key = w;
        sort(key.begin(), key.end());   // Sorted form = anagram key
        groups[key].push_back(w);
    }
    vector<vector<string>> result;
    for (auto &[key, group] : groups)
        result.push_back(group);
    return result;
}

int main() {
    vector<string> words = {"eat","tea","tan","ate","nat","bat"};
    auto groups = groupAnagrams(words);
    for (auto &g : groups) {
        for (auto &w : g) cout << w << " ";
        cout << "\n";
    }
}
```

> 💡 **Key:** Sorted string → same for all anagrams → use as hash key!

---

## 14. First Non-Repeating Element

### 📝 Problem
Find the first element that appears only once in an array.

### 🧪 Test Cases
| # | Input | Answer |
|---|---|---|
| 1 | `{7,3,5,7,5,3,6}` | 6 |
| 2 | `{1,2,3,2,1}` | 3 |
| 3 | `{1,1,2}` | 2 |
| 4 | `{5,5,5}` | -1 (none) |
| 5 | `{9}` | 9 |

### ✅ Without STL
```cpp
int firstNonRepeating(int arr[], int n) {
    int freq[100001] = {0};
    for (int i = 0; i < n; i++) freq[arr[i]]++;
    for (int i = 0; i < n; i++)
        if (freq[arr[i]] == 1) return arr[i];
    return -1;
}
```

### ✅ With STL
```cpp
int firstNonRepeating(vector<int>& v) {
    map<int,int> freq;            // map preserves insertion order? No — use linked map trick
    for (int x : v) freq[x]++;
    for (int x : v)               // Traverse in ORIGINAL order
        if (freq[x] == 1) return x;
    return -1;
}
```

---

## 15. Majority Element (> N/2 times)

### 📝 Problem
Find element appearing more than N/2 times using HashMap.

### 🧪 Test Cases
| # | Input | Answer |
|---|---|---|
| 1 | `{3,2,3}` | 3 |
| 2 | `{2,2,1,1,1,2,2}` | 2 |
| 3 | `{1}` | 1 |
| 4 | `{6,6,6,3,3}` | 6 |
| 5 | `{1,2,3,4,4,4,4}` | 4 |

### ✅ Without STL (Moore's Voting)
```cpp
int majorityElement(int arr[], int n) {
    int candidate = arr[0], count = 1;
    for (int i = 1; i < n; i++) {
        count += (arr[i] == candidate) ? 1 : -1;
        if (count == 0) { candidate = arr[i]; count = 1; }
    }
    return candidate;   // Verify separately if not guaranteed
}
```

### ✅ With STL HashMap
```cpp
int majorityElement(vector<int>& v) {
    unordered_map<int,int> freq;
    int n = v.size();
    for (int x : v) {
        freq[x]++;
        if (freq[x] > n/2) return x;   // Early exit!
    }
    return -1;
}
```

---

## 16. Subarray with Given Sum (Prefix Sum + HashMap)

### 📝 Problem
Count number of subarrays with sum equal to K (handles negatives).

### 🧪 Test Cases
| # | Array | K | Count |
|---|---|---|---|
| 1 | `{1,1,1}` | 2 | 2 |
| 2 | `{1,2,3}` | 3 | 2 ([1,2] and [3]) |
| 3 | `{-1,-1,1}` | 0 | 1 |
| 4 | `{3,4,7,2,-3,1,4,2}` | 7 | 4 |
| 5 | `{1}` | 1 | 1 |

### ✅ Without STL (O(n²))
```cpp
int countSubarrays(int arr[], int n, int k) {
    int count = 0;
    for (int i = 0; i < n; i++) {
        int sum = 0;
        for (int j = i; j < n; j++) {
            sum += arr[j];
            if (sum == k) count++;
        }
    }
    return count;
}
```

### ✅ With STL (Prefix Sum + HashMap — O(n))
```cpp
int countSubarrays(vector<int>& v, int k) {
    unordered_map<int,int> prefixCount;
    prefixCount[0] = 1;   // Empty prefix
    int sum = 0, count = 0;
    for (int x : v) {
        sum += x;
        // If (sum - k) exists as a prefix, those subarrays sum to k
        count += prefixCount[sum - k];
        prefixCount[sum]++;
    }
    return count;
}
```

> 💡 **Master Pattern:**
> `count += prefixCount[currSum - k]`
> This is the Prefix Sum + HashMap trick — handles negatives, O(n)!

---

## 17. Count Distinct Elements in Every Window

### 📝 Problem
For a sliding window of size K, count distinct elements in each window.

### 🧪 Test Cases
| # | Array | K | Output |
|---|---|---|---|
| 1 | `{1,2,1,3,4,2,3}` | 4 | `{3,4,4,3}` |
| 2 | `{1,1,1,1}` | 2 | `{1,1,1}` |
| 3 | `{1,2,3}` | 2 | `{2,2}` |
| 4 | `{4,1,1}` | 2 | `{2,1}` |
| 5 | `{1,2,3,4,5}` | 3 | `{3,3,3}` |

### ✅ Without STL (O(n×K))
```cpp
void countDistinct(int arr[], int n, int k) {
    for (int i = 0; i <= n-k; i++) {
        int distinct = 0;
        bool counted[100001] = {false};
        for (int j = i; j < i+k; j++) {
            if (!counted[arr[j]]) { distinct++; counted[arr[j]] = true; }
        }
        cout << distinct << " ";
    }
}
```

### ✅ With STL HashMap Sliding Window (O(n))
```cpp
void countDistinct(vector<int>& v, int k) {
    unordered_map<int,int> window;
    // Build first window
    for (int i = 0; i < k; i++) window[v[i]]++;
    cout << window.size() << " ";

    // Slide the window
    for (int i = k; i < v.size(); i++) {
        window[v[i]]++;           // Add new element
        window[v[i-k]]--;         // Remove old element
        if (window[v[i-k]] == 0)
            window.erase(v[i-k]); // Remove if count drops to 0
        cout << window.size() << " ";
    }
}
```

---

## 18. 4Sum Count (4 Arrays)

### 📝 Problem
Count tuples (a,b,c,d) such that A[i]+B[j]+C[k]+D[l] = 0.

### 🧪 Test Cases
| # | A | B | C | D | Count |
|---|---|---|---|---|---|
| 1 | `[1,2]` | `[-2,-1]` | `[-1,2]` | `[0,2]` | 2 |
| 2 | `[0]` | `[0]` | `[0]` | `[0]` | 1 |

### ✅ With STL HashMap (O(n²))
```cpp
int fourSumCount(vector<int>& A, vector<int>& B,
                 vector<int>& C, vector<int>& D) {
    unordered_map<int,int> ab;
    for (int a : A)
        for (int b : B)
            ab[a+b]++;          // Store all sums of A+B

    int count = 0;
    for (int c : C)
        for (int d : D)
            count += ab[-(c+d)]; // How many A+B sums cancel C+D?
    return count;
}
```

> 💡 **Key:** Split into two pairs. Store A+B sums in map. Look for -(C+D). O(n²) is optimal here!

---

## 19. Clone a Linked List with Random Pointer

### 📝 Problem
Clone a linked list where each node has `next` and `random` pointer.

### ✅ With STL HashMap (Classic Solution)
```cpp
struct Node {
    int val;
    Node *next, *random;
    Node(int v) : val(v), next(nullptr), random(nullptr) {}
};

Node* clone(Node* head) {
    unordered_map<Node*, Node*> mp;  // original → clone

    // Pass 1: Create all clone nodes
    Node* curr = head;
    while (curr) {
        mp[curr] = new Node(curr->val);
        curr = curr->next;
    }

    // Pass 2: Connect next and random
    curr = head;
    while (curr) {
        mp[curr]->next   = mp[curr->next];
        mp[curr]->random = mp[curr->random];
        curr = curr->next;
    }
    return mp[head];
}
```

> 💡 **Key:** HashMap maps original → clone, so random pointers can be resolved O(1).

---

## 20. Intersection of Two Arrays

### 📝 Problem
Find common elements between two arrays (unique values only).

### 🧪 Test Cases
| # | A | B | Intersection |
|---|---|---|---|
| 1 | `{1,2,2,1}` | `{2,2}` | `{2}` |
| 2 | `{4,9,5}` | `{9,4,9,8,4}` | `{4,9}` |
| 3 | `{1,2,3}` | `{4,5,6}` | `{}` |
| 4 | `{1,1,1}` | `{1,1}` | `{1}` |
| 5 | `{1,2,3,4}` | `{2,4,6}` | `{2,4}` |

### ✅ Without STL (Sorting)
```cpp
vector<int> intersection(int a[], int m, int b[], int n) {
    sort(a, a+m); sort(b, b+n);
    vector<int> result;
    int i = 0, j = 0;
    while (i < m && j < n) {
        if (a[i] == b[j]) {
            if (result.empty() || result.back() != a[i])
                result.push_back(a[i]);
            i++; j++;
        } else if (a[i] < b[j]) i++;
        else j++;
    }
    return result;
}
```

### ✅ With STL HashMap
```cpp
vector<int> intersection(vector<int>& A, vector<int>& B) {
    unordered_set<int> setA(A.begin(), A.end());
    vector<int> result;
    unordered_set<int> seen;
    for (int b : B)
        if (setA.count(b) && !seen.count(b)) {
            result.push_back(b);
            seen.insert(b);
        }
    return result;
}
```

---

## 21. Word Frequency in a Sentence

### 📝 Problem
Count how many times each word appears in a sentence.

### 🧪 Test Cases
| # | Sentence | Top Word |
|---|---|---|
| 1 | `"the cat sat on the mat"` | `the` → 2 |
| 2 | `"to be or not to be"` | `to,be` → 2 each |
| 3 | `"hello world hello"` | `hello` → 2 |
| 4 | `"one"` | `one` → 1 |
| 5 | `"a a a b b c"` | `a` → 3 |

### ✅ Without STL
```cpp
// Manual approach complex — use STL version below
```

### ✅ With STL
```cpp
#include <sstream>
void wordFrequency(string sentence) {
    map<string,int> freq;
    stringstream ss(sentence);
    string word;
    while (ss >> word) freq[word]++;

    // Print sorted by word
    cout << "Word Frequencies:\n";
    for (auto &[w, cnt] : freq)
        cout << w << ": " << cnt << "\n";

    // Find most frequent word
    auto maxIt = max_element(freq.begin(), freq.end(),
        [](auto &a, auto &b){ return a.second < b.second; });
    cout << "Most frequent: " << maxIt->first << " (" << maxIt->second << "x)\n";
}
```

---

## 📘 HashMap Patterns Quick Reference

| Pattern | Code | Use When |
|---|---|---|
| Frequency count | `freq[x]++` | Count occurrences |
| Check exists | `map.count(key)` | Avoid creating key |
| Complement lookup | `seen[target-x]` | Two-sum style |
| Prefix sum | `prefixCount[sum-k]++` | Subarray sum = k |
| Group by key | `groups[sorted_key].push_back(x)` | Group anagrams |
| Sliding window | `window[new]++; window[out]--; if==0 erase` | Window distinct |
| Original→Clone | `map[original] = new Node(...)` | Clone with pointers |

---

## 🚨 Common Mistakes to AVOID

| Mistake ❌ | Correct ✅ |
|---|---|
| `m["key"]` to check existence | Use `m.count("key")` — `[]` **creates** the key! |
| Using `map` when order not needed | Use `unordered_map` for **O(1)** speed |
| Forgetting `prefixCount[0]=1` | Always initialize prefix sum base case |
| Erasing while iterating | Use `it = m.erase(it)` or iterate separately |
| `multimap[key]` direct access | Use `.equal_range(key)` for multimap |
| Hash collision worst case O(n) | Rare, customize hash or use `map` if worried |

---
*HashMap Complete Guide | TCS NQT & Competitive Programming | Basics + 13 Problems*
