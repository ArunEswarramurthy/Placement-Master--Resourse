# 📝 C++ STRINGS — Complete Guide + Problems
### Learn Strings from Zero → Hero | Best Resource 🚀

---

## 📌 TABLE OF CONTENTS

### PART A — STRING BASICS (Learn First!)
1. [What is a String?](#1-what-is-a-string)
2. [Declaring & Initializing Strings](#2-declaring--initializing-strings)
3. [String Input & Output](#3-string-input--output)
4. [String Length & Access](#4-string-length--access)
5. [String Operations Cheatsheet](#5-string-operations-cheatsheet)
6. [String Traversal](#6-string-traversal)
7. [Character Functions](#7-character-functions)
8. [String Conversion Functions](#8-string-conversion-functions)
9. [String Comparison](#9-string-comparison)
10. [String Searching & Substrings](#10-string-searching--substrings)
11. [String Modification](#11-string-modification)
12. [String Splitting & Joining](#12-string-splitting--joining)

### PART B — STRING PROBLEMS
13. [Reverse a String](#13-reverse-a-string)
14. [Check Palindrome String](#14-check-palindrome-string)
15. [Anagram Check](#15-anagram-check)
16. [Count Vowels and Consonants](#16-count-vowels-and-consonants)
17. [Remove Duplicates from String](#17-remove-duplicates-from-string)
18. [Frequency of Each Character](#18-frequency-of-each-character)
19. [Longest Common Prefix](#19-longest-common-prefix)
20. [Check Pangram](#20-check-pangram)
21. [First Non-Repeating Character](#21-first-non-repeating-character)
22. [Longest Substring Without Repeating Characters](#22-longest-substring-without-repeating-characters)
23. [Count Words in a Sentence](#23-count-words-in-a-sentence)
24. [String Rotation Check](#24-string-rotation-check)
25. [Caesar Cipher (Encode/Decode)](#25-caesar-cipher-encodedecode)

---

# ═══════════════════════════════════
# PART A — STRING BASICS (LEARN FIRST!)
# ═══════════════════════════════════

## 1. What is a String?

A **string** is a sequence of characters. In C++ there are two ways to handle strings:

| Type | Style | Recommendation |
|---|---|---|
| `char arr[]` | C-style, null-terminated | Avoid — old style |
| `std::string` | C++ class with rich methods | ✅ Always use this |

```cpp
// C-style (avoid)
char name[] = "Hello";
char name2[10] = "World";

// C++ string (use this!)
#include <string>
string name = "Hello World";
```

> **Why prefer `std::string`?**
> ✅ Dynamic size (grows automatically)
> ✅ Rich built-in methods (.length, .find, .substr, etc.)
> ✅ Safe — no buffer overflow issues
> ✅ Easy to compare, copy, concatenate

---

## 2. Declaring & Initializing Strings

```cpp
#include <string>
using namespace std;

string s1;                      // Empty string ""
string s2 = "Hello";            // Initialize with value
string s3("World");             // Constructor style
string s4(5, 'x');              // "xxxxx" — 5 copies of 'x'
string s5 = s2;                 // Copy of s2
string s6 = s2 + " " + s3;     // Concatenation → "Hello World"
string s7(s2, 1, 3);            // Substring from index 1, length 3 → "ell"
```

---

## 3. String Input & Output

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s1, s2;

    // Single word (stops at space)
    cin >> s1;

    // Full line including spaces ← use this for sentences!
    getline(cin, s2);

    // ⚠️ COMMON PITFALL: cin leaves '\n' in buffer!
    // If mixing cin >> and getline, flush first:
    cin >> s1;
    cin.ignore();          // Discard leftover newline
    getline(cin, s2);      // Now works correctly

    cout << s1 << endl;
    cout << s2 << endl;
    return 0;
}
```

---

## 4. String Length & Access

```cpp
string s = "Hello World";

// Length
cout << s.length();          // 11
cout << s.size();            // 11  (same as length)
cout << s.empty();           // 0   (false — not empty)

// Access individual characters
cout << s[0];                // 'H'  (no bounds check)
cout << s.at(0);             // 'H'  (with bounds check — safer)
cout << s.front();           // 'H'  (first character)
cout << s.back();            // 'd'  (last character)

// Modify a character
s[0] = 'J';                  // s = "Jello World"
s.front() = 'H';             // s = "Hello World"

// Check empty
string empty = "";
cout << empty.empty();       // 1 (true)
```

---

## 5. String Operations Cheatsheet

```cpp
string s = "Hello World";

// ─────────────────── ADDING ───────────────────
s += "!";                        // Append    → "Hello World!"
s.append(" How are you?");       // Append    → "Hello World! How are you?"
s.push_back('!');                // Add 1 char at end

// ─────────────────── REMOVING ───────────────────
s.pop_back();                    // Remove last character
s.erase(5, 6);                   // Erase 6 chars from index 5
s.clear();                       // Remove ALL → ""

// ─────────────────── FINDING ───────────────────
s = "Hello World Hello";
size_t pos = s.find("Hello");         // First occurrence → 0
size_t pos2 = s.rfind("Hello");       // Last occurrence  → 12
size_t pos3 = s.find("xyz");          // Not found → string::npos

if (pos3 == string::npos)
    cout << "Not found!" << endl;

// Find first of any char in set
pos = s.find_first_of("aeiou");       // First vowel position
pos = s.find_last_of("aeiou");        // Last vowel position
pos = s.find_first_not_of("Helo ");   // First char NOT in set

// ─────────────────── REPLACE ───────────────────
s.replace(6, 5, "C++");          // Replace 5 chars at pos 6 → "Hello C++ Hello"

// ─────────────────── SUBSTRING ───────────────────
string sub = s.substr(6, 3);     // Start=6, length=3 → "C++"
string rest = s.substr(6);       // From index 6 to end

// ─────────────────── INSERT ───────────────────
s.insert(5, ",");                 // Insert at position 5

// ─────────────────── RESIZE ───────────────────
s.resize(5);                      // Truncate to 5 chars
s.resize(10, '*');                // Extend to 10 with '*'
```

---

## 6. String Traversal

```cpp
string s = "Hello";

// Method 1: Index-based
for (int i = 0; i < s.length(); i++)
    cout << s[i] << " ";

// Method 2: Range-based ← PREFER THIS
for (char c : s)
    cout << c << " ";

// Method 3: Reference (can modify!)
for (char &c : s)
    c = toupper(c);    // Modifies the string in-place

// Method 4: Iterator
for (auto it = s.begin(); it != s.end(); ++it)
    cout << *it;

// Method 5: Reverse traversal
for (auto it = s.rbegin(); it != s.rend(); ++it)
    cout << *it;              // Prints in reverse

// Method 6: Index traversal in reverse
for (int i = s.length()-1; i >= 0; i--)
    cout << s[i];
```

---

## 7. Character Functions

```cpp
#include <cctype>   // For character functions

char c = 'A';

// Check type
isalpha(c);    // Is letter?          → true
isdigit(c);    // Is digit?           → false
isalnum(c);    // Is letter or digit? → true
islower(c);    // Is lowercase?       → false
isupper(c);    // Is uppercase?       → true
isspace(c);    // Is whitespace?      → false

// Convert
tolower(c);    // 'a'  (lowercase)
toupper('a');  // 'A'  (uppercase)

// ASCII tricks
int ascii = 'A';          // 65
char ch = 65;             // 'A'
int digit = '5' - '0';   // 5  (char digit to int!)
char toChar = 5 + '0';   // '5' (int to char digit!)

// Alphabetic position (a=1, b=2, ...)
int pos = 'e' - 'a' + 1;   // 5
```

> **ASCII Quick Reference:**
>
> | Character | ASCII |
> |---|---|
> | '0'–'9' | 48–57 |
> | 'A'–'Z' | 65–90 |
> | 'a'–'z' | 97–122 |
> | Diff upper→lower | +32 |

---

## 8. String Conversion Functions

```cpp
#include <string>
#include <sstream>

// ── NUMBER → STRING ──
int n = 42;
string s1 = to_string(n);          // "42"
string s2 = to_string(3.14);       // "3.140000"

// ── STRING → NUMBER ──
string s = "123";
int i    = stoi(s);                // 123  (string to int)
long l   = stol(s);                // 123  (string to long)
long long ll = stoll(s);           // 123  (string to long long)
double d = stod("3.14");           // 3.14 (string to double)
float f  = stof("3.14");           // 3.14 (string to float)

// ── STRINGSTREAM (powerful!) ──
#include <sstream>
stringstream ss;
ss << "Hello " << 42 << " World";
string result = ss.str();           // "Hello 42 World"

// Parse numbers from string
string data = "10 20 30 40";
stringstream ss2(data);
int x;
while (ss2 >> x)
    cout << x << " ";              // 10 20 30 40

// ── C-STRING CONVERSION ──
string cpp_str = "Hello";
const char* c_str = cpp_str.c_str();   // Convert to C-style string
```

---

## 9. String Comparison

```cpp
string a = "apple";
string b = "banana";

// Comparison operators (lexicographic)
cout << (a == b);     // 0 (false)
cout << (a != b);     // 1 (true)
cout << (a < b);      // 1 (true — 'a' < 'b')
cout << (a > b);      // 0 (false)

// compare() method: returns 0, negative, or positive
int r = a.compare(b);
// r < 0: a comes before b
// r == 0: equal
// r > 0: a comes after b

// Case-insensitive compare (manual)
string s1 = "Hello", s2 = "hello";
bool caseInsensitive = equal(s1.begin(), s1.end(), s2.begin(),
    [](char a, char b){ return tolower(a) == tolower(b); });
cout << caseInsensitive;    // 1 (true)
```

---

## 10. String Searching & Substrings

```cpp
string s = "the quick brown fox jumps over the lazy dog";

// find() — returns position or string::npos
size_t pos = s.find("fox");        // 16
if (pos != string::npos)
    cout << "Found at " << pos;

// rfind() — find from right (last occurrence)
pos = s.rfind("the");              // 31

// substr() — extract portion
string word = s.substr(16, 3);    // "fox" (start=16, len=3)
string tail = s.substr(27);       // Everything from index 27

// Contains check (C++23 has s.contains(), before that:)
bool contains = s.find("fox") != string::npos;

// Count occurrences
int cnt = 0;
size_t p = 0;
while ((p = s.find("the", p)) != string::npos) {
    cnt++;
    p++;
}
cout << cnt;   // 2 (two "the"s)
```

---

## 11. String Modification

```cpp
#include <algorithm>
string s = "Hello World";

// Reverse
reverse(s.begin(), s.end());          // "dlroW olleH"

// Sort characters alphabetically
sort(s.begin(), s.end());             // " HWdellloor"

// To uppercase / lowercase
transform(s.begin(), s.end(), s.begin(), ::toupper);  // ALL UPPERCASE
transform(s.begin(), s.end(), s.begin(), ::tolower);  // all lowercase

// Remove specific character
s.erase(remove(s.begin(), s.end(), ' '), s.end());   // Remove all spaces

// Remove leading/trailing spaces (trim)
auto start = s.find_first_not_of(" \t\n\r");
auto end   = s.find_last_not_of(" \t\n\r");
s = s.substr(start, end - start + 1);

// Replace all occurrences
string replaceAll(string s, const string& from, const string& to) {
    size_t p = 0;
    while ((p = s.find(from, p)) != string::npos) {
        s.replace(p, from.size(), to);
        p += to.size();
    }
    return s;
}
```

---

## 12. String Splitting & Joining

```cpp
#include <sstream>
#include <vector>

// Split by space
string sentence = "the quick brown fox";
vector<string> words;
stringstream ss(sentence);
string word;
while (ss >> word)
    words.push_back(word);
// words = {"the", "quick", "brown", "fox"}

// Split by delimiter (e.g., comma)
string csv = "apple,banana,cherry";
stringstream ss2(csv);
string token;
vector<string> tokens;
while (getline(ss2, token, ','))
    tokens.push_back(token);
// tokens = {"apple", "banana", "cherry"}

// Join vector of strings
vector<string> v = {"Hello", "World", "C++"};
string joined = "";
for (int i = 0; i < v.size(); i++) {
    if (i > 0) joined += " ";
    joined += v[i];
}
// joined = "Hello World C++"
```

---

# ═══════════════════════════════════
# PART B — STRING PROBLEMS
# ═══════════════════════════════════

## 13. Reverse a String

### 📝 Problem
Reverse a string in-place.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `"hello"` | `"olleh"` |
| 2 | `"abcde"` | `"edcba"` |
| 3 | `"a"` | `"a"` |
| 4 | `"madam"` | `"madam"` |
| 5 | `"Hello World"` | `"dlroW olleH"` |

### ✅ Without STL
```cpp
void reverseStr(string &s) {
    int l = 0, r = s.size() - 1;
    while (l < r) {
        char temp = s[l];
        s[l] = s[r];
        s[r] = temp;
        l++; r--;
    }
}
```

### ✅ With STL
```cpp
reverse(s.begin(), s.end());
// OR: string rev(s.rbegin(), s.rend());
```

---

## 14. Check Palindrome String

### 📝 Problem
Check if a string reads the same forwards and backwards. Ignore case.

### 🧪 Test Cases
| # | Input | Palindrome? |
|---|---|---|
| 1 | `"racecar"` | Yes ✅ |
| 2 | `"hello"` | No ❌ |
| 3 | `"madam"` | Yes ✅ |
| 4 | `"A man a plan a canal Panama"` | Yes ✅ (ignore spaces/case) |
| 5 | `"abba"` | Yes ✅ |

### ✅ Without STL
```cpp
bool isPalindrome(string s) {
    int l = 0, r = s.size() - 1;
    while (l < r) {
        if (tolower(s[l]) != tolower(s[r])) return false;
        l++; r--;
    }
    return true;
}
```

### ✅ With STL
```cpp
bool isPalindrome(string s) {
    transform(s.begin(), s.end(), s.begin(), ::tolower);
    // Remove non-alphanumeric (for "A man..." style)
    s.erase(remove_if(s.begin(), s.end(), [](char c){ return !isalnum(c); }), s.end());
    string rev(s.rbegin(), s.rend());
    return s == rev;
}
```

---

## 15. Anagram Check

### 📝 Problem
Two strings are **anagrams** if they contain the same characters with the same frequency.

### 🧪 Test Cases
| # | s1 | s2 | Anagram? |
|---|---|---|---|
| 1 | `"listen"` | `"silent"` | Yes ✅ |
| 2 | `"hello"` | `"world"` | No ❌ |
| 3 | `"triangle"` | `"integral"` | Yes ✅ |
| 4 | `"abc"` | `"cab"` | Yes ✅ |
| 5 | `"rat"` | `"car"` | No ❌ |

### ✅ Without STL
```cpp
bool isAnagram(string a, string b) {
    if (a.size() != b.size()) return false;
    int freq[26] = {0};
    for (char c : a) freq[c - 'a']++;
    for (char c : b) freq[c - 'a']--;
    for (int i = 0; i < 26; i++)
        if (freq[i] != 0) return false;
    return true;
}
```

### ✅ With STL
```cpp
bool isAnagram(string a, string b) {
    sort(a.begin(), a.end());
    sort(b.begin(), b.end());
    return a == b;
    // OR: return (map<char,int>(a.begin(),a.end()) ==
    //             map<char,int>(b.begin(),b.end()));
}
```

> 💡 **Key Insight:** Frequency array [26] is O(1) space & O(n) time. Sort method is O(n log n). For lowercase only, use freq[c-'a'].

---

## 16. Count Vowels and Consonants

### 📝 Problem
Count vowels (a,e,i,o,u) and consonants in a string.

### 🧪 Test Cases
| # | Input | Vowels | Consonants |
|---|---|---|---|
| 1 | `"hello"` | 2 | 3 |
| 2 | `"programming"` | 4 | 7 |
| 3 | `"aeiou"` | 5 | 0 |
| 4 | `"rhythm"` | 0 | 6 |
| 5 | `"Hello World"` | 3 | 7 (space excluded) |

### ✅ Without STL
```cpp
void countVowelsCons(string s) {
    int vowels = 0, consonants = 0;
    string vowelSet = "aeiouAEIOU";
    for (char c : s) {
        if (isalpha(c)) {
            bool isVowel = false;
            for (char v : vowelSet)
                if (c == v) { isVowel = true; break; }
            isVowel ? vowels++ : consonants++;
        }
    }
    cout << "Vowels: " << vowels << ", Consonants: " << consonants;
}
```

### ✅ With STL
```cpp
void countVowelsCons(string s) {
    string vowels = "aeiouAEIOU";
    int v = count_if(s.begin(), s.end(), [&](char c){
        return isalpha(c) && vowels.find(c) != string::npos;
    });
    int cons = count_if(s.begin(), s.end(), [&](char c){
        return isalpha(c) && vowels.find(c) == string::npos;
    });
    cout << "Vowels: " << v << ", Consonants: " << cons;
}
```

---

## 17. Remove Duplicates from String

### 📝 Problem
Keep only the **first occurrence** of each character (preserve order).

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `"programming"` | `"progamin"` |
| 2 | `"aabbcc"` | `"abc"` |
| 3 | `"abcabc"` | `"abc"` |
| 4 | `"hello"` | `"helo"` |
| 5 | `"mississippi"` | `"misp"` |

### ✅ Without STL
```cpp
string removeDups(string s) {
    bool seen[256] = {false};
    string result = "";
    for (char c : s) {
        if (!seen[(int)c]) {
            seen[(int)c] = true;
            result += c;
        }
    }
    return result;
}
```

### ✅ With STL
```cpp
string removeDups(string s) {
    unordered_set<char> seen;
    string result = "";
    for (char c : s)
        if (seen.insert(c).second)    // insert returns {iter, bool}
            result += c;
    return result;
}
```

> 💡 **Key Insight:** `seen.insert(c).second` returns `true` if the element was newly inserted (not a duplicate).

---

## 18. Frequency of Each Character

### 📝 Problem
Count how many times each character appears in a string.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `"hello"` | h:1, e:1, l:2, o:1 |
| 2 | `"aabbcc"` | a:2, b:2, c:2 |
| 3 | `"programming"` | p:1, r:2, o:1, g:2, a:1, m:2, i:1, n:1 |
| 4 | `"aaaa"` | a:4 |
| 5 | `"abcde"` | a:1, b:1, c:1, d:1, e:1 |

### ✅ Without STL
```cpp
void charFrequency(string s) {
    int freq[256] = {0};
    for (char c : s) freq[(int)c]++;
    for (int i = 0; i < 256; i++)
        if (freq[i] > 0)
            cout << (char)i << ": " << freq[i] << "\n";
}
```

### ✅ With STL
```cpp
void charFrequency(string s) {
    map<char, int> freq;
    for (char c : s) freq[c]++;

    for (auto &[ch, cnt] : freq)
        cout << ch << ": " << cnt << "\n";

    // Find max frequency character
    auto maxIt = max_element(freq.begin(), freq.end(),
        [](auto &a, auto &b){ return a.second < b.second; });
    cout << "Most frequent: " << maxIt->first << " (" << maxIt->second << " times)\n";
}
```

---

## 19. Longest Common Prefix

### 📝 Problem
Find the longest common prefix string among an array of strings.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `["flower","flow","flight"]` | `"fl"` |
| 2 | `["dog","racecar","car"]` | `""` |
| 3 | `["abc","abcd","ab"]` | `"ab"` |
| 4 | `["same","same","same"]` | `"same"` |
| 5 | `["a"]` | `"a"` |

### ✅ Without STL
```cpp
string longestCommonPrefix(string words[], int n) {
    string prefix = words[0];
    for (int i = 1; i < n; i++) {
        int j = 0;
        while (j < prefix.size() && j < words[i].size()
               && prefix[j] == words[i][j]) j++;
        prefix = prefix.substr(0, j);
        if (prefix.empty()) return "";
    }
    return prefix;
}
```

### ✅ With STL
```cpp
string longestCommonPrefix(vector<string>& words) {
    if (words.empty()) return "";
    sort(words.begin(), words.end());         // Sort lexicographically
    string &first = words.front();
    string &last  = words.back();             // Most different pair
    int i = 0;
    while (i < first.size() && first[i] == last[i]) i++;
    return first.substr(0, i);
}
```

---

## 20. Check Pangram

### 📝 Problem
A **pangram** contains every letter of the alphabet at least once.

### 🧪 Test Cases
| # | Input | Pangram? |
|---|---|---|
| 1 | `"The quick brown fox jumps over the lazy dog"` | Yes ✅ |
| 2 | `"Hello World"` | No ❌ |
| 3 | `"Pack my box with five dozen liquor jugs"` | Yes ✅ |
| 4 | `"abcdefghijklmnopqrstuvwxyz"` | Yes ✅ |
| 5 | `"The five boxing wizards jump quickly"` | Yes ✅ |

### ✅ Without STL
```cpp
bool isPangram(string s) {
    bool seen[26] = {false};
    for (char c : s)
        if (isalpha(c))
            seen[tolower(c) - 'a'] = true;
    for (int i = 0; i < 26; i++)
        if (!seen[i]) return false;
    return true;
}
```

### ✅ With STL
```cpp
bool isPangram(string s) {
    set<char> letters;
    for (char c : s)
        if (isalpha(c)) letters.insert(tolower(c));
    return letters.size() == 26;
    // OR: unordered_set for faster O(1) lookup
}
```

---

## 21. First Non-Repeating Character

### 📝 Problem
Find the **first character** that appears only once.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `"leetcode"` | `'l'` |
| 2 | `"loveleetcode"` | `'v'` |
| 3 | `"aabb"` | `'\0'` (none) |
| 4 | `"abcabc"` | `'\0'` (none) |
| 5 | `"hello"` | `'h'` |

### ✅ Without STL
```cpp
char firstNonRepeating(string s) {
    int freq[256] = {0};
    for (char c : s) freq[(int)c]++;
    for (char c : s)                     // Preserve order!
        if (freq[(int)c] == 1) return c;
    return '\0';
}
```

### ✅ With STL
```cpp
char firstNonRepeating(string s) {
    map<char, int> freq;
    for (char c : s) freq[c]++;
    for (char c : s)                     // Traverse in original order
        if (freq[c] == 1) return c;
    return '\0';
}
// Note: Use unordered_map for O(1) lookups
```

---

## 22. Longest Substring Without Repeating Characters

### 📝 Problem
Find the **length** of the longest substring with all unique characters.

### 🧪 Test Cases
| # | Input | Length | Substring |
|---|---|---|---|
| 1 | `"abcabcbb"` | 3 | `"abc"` |
| 2 | `"bbbbb"` | 1 | `"b"` |
| 3 | `"pwwkew"` | 3 | `"wke"` |
| 4 | `"abcdef"` | 6 | `"abcdef"` |
| 5 | `"dvdf"` | 3 | `"vdf"` |

### ✅ Without STL
```cpp
int longestUniqueSubstr(string s) {
    bool inWindow[256] = {false};
    int left = 0, maxLen = 0;
    for (int right = 0; right < s.size(); right++) {
        while (inWindow[(int)s[right]]) {
            inWindow[(int)s[left]] = false;
            left++;
        }
        inWindow[(int)s[right]] = true;
        maxLen = max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

### ✅ With STL (Sliding Window + unordered_map)
```cpp
int longestUniqueSubstr(string s) {
    unordered_map<char, int> lastSeen;   // char → last index seen
    int left = 0, maxLen = 0;
    for (int right = 0; right < s.size(); right++) {
        if (lastSeen.count(s[right]) && lastSeen[s[right]] >= left)
            left = lastSeen[s[right]] + 1;    // Shrink window
        lastSeen[s[right]] = right;
        maxLen = max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

> 💡 **Key Insight:** Sliding window is O(n). Store last seen index to jump left pointer directly instead of moving one step at a time.

---

## 23. Count Words in a Sentence

### 📝 Problem
Count the number of words (separated by spaces) in a sentence.

### 🧪 Test Cases
| # | Input | Count |
|---|---|---|
| 1 | `"Hello World"` | 2 |
| 2 | `"  spaces  between  words  "` | 3 |
| 3 | `"oneword"` | 1 |
| 4 | `""` | 0 |
| 5 | `"TCS NQT is easy to crack"` | 6 |

### ✅ Without STL
```cpp
int countWords(string s) {
    int count = 0;
    bool inWord = false;
    for (char c : s) {
        if (c != ' ' && !inWord) { inWord = true; count++; }
        else if (c == ' ') inWord = false;
    }
    return count;
}
```

### ✅ With STL
```cpp
int countWords(string s) {
    stringstream ss(s);
    string word;
    int count = 0;
    while (ss >> word) count++;   // >> skips whitespace automatically
    return count;
}
```

---

## 24. String Rotation Check

### 📝 Problem
Check if string B is a **rotation** of string A.
Example: "abcde" rotated by 2 → "cdeab"

### 🧪 Test Cases
| # | A | B | Rotation? |
|---|---|---|---|
| 1 | `"abcde"` | `"cdeab"` | Yes ✅ |
| 2 | `"hello"` | `"llohe"` | Yes ✅ |
| 3 | `"abc"` | `"bca"` | Yes ✅ |
| 4 | `"abc"` | `"acb"` | No ❌ |
| 5 | `"aab"` | `"aba"` | No ❌ |

### ✅ Without STL
```cpp
bool isRotation(string a, string b) {
    if (a.size() != b.size()) return false;
    string doubled = a + a;             // "abcdeabcde"
    // Check if b is a substring of doubled
    int n = a.size(), m = b.size();
    for (int i = 0; i <= n; i++) {
        if (doubled.substr(i, m) == b) return true;
    }
    return false;
}
```

### ✅ With STL
```cpp
bool isRotation(string a, string b) {
    if (a.size() != b.size()) return false;
    string doubled = a + a;
    return doubled.find(b) != string::npos;   // One line!
}
```

> 💡 **Key Insight:** If B is a rotation of A, then B must be a **substring of A+A**. Brilliant trick!

---

## 25. Caesar Cipher (Encode/Decode)

### 📝 Problem
Shift each letter by K positions (wraps around z→a).

### 🧪 Test Cases
| # | Input | Shift K | Encoded |
|---|---|---|---|
| 1 | `"hello"` | 3 | `"khoor"` |
| 2 | `"xyz"` | 3 | `"abc"` (wraps!) |
| 3 | `"Hello World"` | 13 | `"Uryyb Jbeyq"` |
| 4 | `"abc"` | 26 | `"abc"` (full cycle) |
| 5 | `"TCS NQT"` | 5 | `"YHX SVY"` |

### ✅ Without STL
```cpp
string caesarEncode(string s, int k) {
    k = k % 26;           // Handle k > 26
    for (char &c : s) {
        if (isupper(c))
            c = (c - 'A' + k) % 26 + 'A';
        else if (islower(c))
            c = (c - 'a' + k) % 26 + 'a';
        // Non-alphabetic characters unchanged
    }
    return s;
}

string caesarDecode(string s, int k) {
    return caesarEncode(s, 26 - k % 26);   // Decode = encode backwards
}
```

### ✅ With STL
```cpp
string caesarEncode(string s, int k) {
    k %= 26;
    transform(s.begin(), s.end(), s.begin(), [k](char c) -> char {
        if (isupper(c)) return (c - 'A' + k) % 26 + 'A';
        if (islower(c)) return (c - 'a' + k) % 26 + 'a';
        return c;
    });
    return s;
}

int main() {
    cout << caesarEncode("hello", 3) << "\n";   // khoor
    cout << caesarDecode("khoor", 3) << "\n";   // hello
}
```

---

## 📘 All Operations Quick Summary

```cpp
// ── DECLARE ──────────────────
string s = "Hello";

// ── SIZE ─────────────────────
s.length()  s.size()  s.empty()

// ── ACCESS ───────────────────
s[i]  s.at(i)  s.front()  s.back()

// ── ADD ──────────────────────
s += "!"         s.append("!")     s.push_back('!')
s.insert(i, "x")

// ── REMOVE ───────────────────
s.pop_back()     s.erase(i, n)     s.clear()

// ── SEARCH ───────────────────
s.find("x")      s.rfind("x")      string::npos
s.substr(i, n)   s.substr(i)

// ── MODIFY ───────────────────
s.replace(i, n, "new")    reverse(s.begin(), s.end())
sort(s.begin(), s.end())  transform(...)

// ── COMPARE ──────────────────
s1 == s2   s1 < s2   s1.compare(s2)

// ── CONVERT ──────────────────
to_string(42)  stoi("42")  stod("3.14")  s.c_str()

// ── CHAR FUNCTIONS ───────────
isalpha(c)  isdigit(c)  islower(c)  isupper(c)
tolower(c)  toupper(c)  c-'0'  c-'a'
```

---

## 🚨 Common String Mistakes to AVOID

| Mistake ❌ | Correct ✅ |
|---|---|
| `cin >> s` for sentences | Use `getline(cin, s)` |
| Forgetting `cin.ignore()` after `cin >>` | Always `cin.ignore()` before `getline` |
| Using `s.find()` result in `if` directly | Check `!= string::npos` |
| `s[s.length()]` access | Last valid index is `s.length()-1` |
| Comparing with `==` case-sensitively | `tolower()` both before comparing |
| `char - 'a'` on uppercase | Check `islower/isupper` first |
| Modifying string while iterating by iterator | Use index-based or make a copy |

---
*String Complete Guide | TCS NQT & Competitive Programming | With & Without STL*
