# ⚙️ C++ FUNCTIONS — Complete Guide + Problems
### Master Functions, Recursion & Advanced Concepts | Zero → Hero 🚀

---

## 📌 TABLE OF CONTENTS

### PART A — FUNCTION BASICS & CONCEPTS
1. [What is a Function? (Syntax & Structure)](#1-what-is-a-function-syntax--structure)
2. [Function Prototypes (Declaration vs Definition)](#2-function-prototypes-declaration-vs-definition)
3. [Pass by Value vs Pass by Reference](#3-pass-by-value-vs-pass-by-reference)
4. [Passing Arrays & Vectors to Functions](#4-passing-arrays--vectors-to-functions)
5. [Default Arguments](#5-default-arguments)
6. [Function Overloading](#6-function-overloading)
7. [Inline Functions](#7-inline-functions)
8. [Lambda Functions (C++11)](#8-lambda-functions-c11)
9. [Recursion Basics (How it works)](#9-recursion-basics-how-it-works)

### PART B — FUNCTION & RECURSION PROBLEMS
10. [Swap Two Numbers (3 ways)](#10-swap-two-numbers-3-ways)
11. [Find Maximum of N Numbers (Variadic / Vector)](#11-find-maximum-of-n-numbers-variadic--vector)
12. [Factorial using Recursion](#12-factorial-using-recursion)
13. [Fibonacci using Recursion](#13-fibonacci-using-recursion)
14. [Sum of Digits using Recursion](#14-sum-of-digits-using-recursion)
15. [Reverse a String using Recursion](#15-reverse-a-string-using-recursion)
16. [Check Palindrome using Recursion](#16-check-palindrome-using-recursion)
17. [Tower of Hanoi (Classic Recursion)](#17-tower-of-hanoi-classic-recursion)
18. [Binary Search using Recursion](#18-binary-search-using-recursion)
19. [Custom Sort with Lambda Function](#19-custom-sort-with-lambda-function)

---

# ═══════════════════════════════════
# PART A — FUNCTION BASICS
# ═══════════════════════════════════

## 1. What is a Function? (Syntax & Structure)

A function is a reusable block of code that performs a specific task.

### Syntax:
```cpp
return_type function_name(parameter_list) {
    // block of code
    return value;  // (if return_type is not void)
}
```

### Example:
```cpp
#include <iostream>
using namespace std;

// Function Definition
int add(int a, int b) {
    return a + b;
}

// Void function (no return value)
void greet(string name) {
    cout << "Hello, " << name << "!\n";
}

int main() {
    int sum = add(5, 10);     // Function Call
    cout << "Sum: " << sum << "\n";
    greet("Arjun");
    return 0;
}
```

---

## 2. Function Prototypes (Declaration vs Definition)

C++ reads code top-to-bottom. If you call a function before defining it, you get an error.
**Solution:** Use a Function Prototype!

```cpp
#include <iostream>
using namespace std;

// 1. Function Declaration (Prototype)
int multiply(int a, int b);

int main() {
    // 2. Function Call
    cout << multiply(4, 5);
    return 0;
}

// 3. Function Definition (Implementation)
int multiply(int a, int b) {
    return a * b;
}
```

---

## 3. Pass by Value vs Pass by Reference

This is the most asked interview concept in C++!

### ❌ Pass by Value (Makes a COPY)
Changes inside the function do **NOT** affect the original variable.
```cpp
void modifyValue(int x) {
    x = 100;    // Changes only local copy
}

int main() {
    int a = 10;
    modifyValue(a);
    cout << a;  // Output: 10 (unchanged)
}
```

### ✅ Pass by Reference (`&`) (Shares memory)
Changes inside the function **DO** affect the original variable.
```cpp
void modifyReference(int &x) {
    x = 100;    // Changes the original variable!
}

int main() {
    int a = 10;
    modifyReference(a);
    cout << a;  // Output: 100 (Changed!)
}
```

> 💡 **Best Practice:** Pass large objects (like `string`, `vector`) by reference to save memory and time. Use `const &` if you don't want to modify it.
> `void printVector(const vector<int> &v)`

---

## 4. Passing Arrays & Vectors to Functions

### Passing C-Style Arrays (Passes a Pointer)
Arrays are ALWAYS passed by reference (technically, a pointer to the first element). You **must** pass the size manually.

```cpp
// arr[] is actually int* arr
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++)
        cout << arr[i] << " ";
}

int main() {
    int A[] = {1, 2, 3};
    printArray(A, 3);
}
```

### Passing STL Vectors (Pass by Value by default!)
Vectors are passed by value (copied). **Always pass vectors by reference (`&`).**

```cpp
#include <vector>

// BAD: Copies entire vector (Slow, O(N))
void slowPrint(vector<int> v) { ... }

// GOOD: Passes reference (Fast, O(1))
void fastPrint(const vector<int> &v) {
    for(int x : v) cout << x << " ";
}
```

---

## 5. Default Arguments

You can provide default values for parameters.
⚠️ **Rule:** Default arguments must be from **right to left**.

```cpp
// Valid: defaults are at the end
int volume(int length, int width = 5, int height = 10) {
    return length * width * height;
}

// INVALID: int volume(int l = 5, int w, int h) // Error!

int main() {
    cout << volume(2);          // 2 * 5 * 10 = 100
    cout << volume(2, 3);       // 2 * 3 * 10 = 60
    cout << volume(2, 3, 4);    // 2 * 3 * 4 = 24
}
```

---

## 6. Function Overloading

Multiple functions can have the **same name** if their **parameter lists (types or count) are different**.

```cpp
#include <iostream>
using namespace std;

// 1. Two int parameters
int add(int a, int b) { return a + b; }

// 2. Three int parameters
int add(int a, int b, int c) { return a + b + c; }

// 3. Two double parameters
double add(double a, double b) { return a + b; }

int main() {
    cout << add(5, 10) << "\n";          // Calls #1
    cout << add(5, 10, 15) << "\n";      // Calls #2
    cout << add(5.5, 2.2) << "\n";       // Calls #3
}
```
> ⚠️ Return type alone is NOT enough to overload a function!

---

## 7. Inline Functions

For very short functions (1-2 lines), calling the function takes more time than executing it.
`inline` asks the compiler to replace the function call directly with the code.

```cpp
inline int square(int x) {
    return x * x;
}

int main() {
    int ans = square(5);  // Compiler replaces this with: int ans = 5 * 5;
}
```
> Note: It's just a request. Compilers may ignore `inline` for complex functions.

---

## 8. Lambda Functions (C++11)

Anonymous (unnamed) functions used for short, one-time tasks (like sorting).

### Syntax: `[capture](parameters) -> return_type { body }`

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    // Simple Lambda
    auto greet = []() { cout << "Hello Lambda!\n"; };
    greet();

    // Lambda with parameters
    auto add = [](int a, int b) { return a + b; };
    cout << add(5, 3) << "\n";

    // Capturing outside variables
    int factor = 10;
    auto multiply = [factor](int x) { return x * factor; };
    cout << multiply(5) << "\n";  // 50

    return 0;
}
```

---

## 9. Recursion Basics (How it works)

A function that calls itself is recursive.
Must have two parts:
1. **Base Case:** When to stop (to prevent infinite loop).
2. **Recursive Step:** Calling itself with a smaller problem.

```cpp
void countSubmarine(int n) {
    if (n == 0) {                 // 1. Base Case
        cout << "Liftoff!\n";
        return;
    }
    cout << n << "...\n";
    countSubmarine(n - 1);        // 2. Recursive Call
}
// Outputs: 3... 2... 1... Liftoff!
```

---

# ═══════════════════════════════════
# PART B — FUNCTION & RECURSION PROBLEMS
# ═══════════════════════════════════

## 10. Swap Two Numbers (3 ways)

### 📝 Problem
Swap two variables using a function.

### ✅ Solution
```cpp
#include <iostream>
using namespace std;

// 1. Using Pass by Reference (&) -> BEST METHOD
void swapRef(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}

// 2. Using Pointers (*) -> C-style
void swapPtr(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// 3. No Temp Variable (Math Trick)
void swapNoTemp(int &a, int &b) {
    a = a + b;
    b = a - b;
    a = a - b;
}

int main() {
    int x = 5, y = 10;
    swapRef(x, y);       // x=10, y=5

    int p = 50, q = 60;
    swapPtr(&p, &q);     // p=60, q=50 (Pass memory addresses!)

    return 0;
}
```

---

## 11. Find Maximum of N Numbers (Variadic / Vector)

### 📝 Problem
Write a function that can take *any amount* of numbers and return the maximum.

### ✅ Solution (Using Vector)
```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

// Pass vector by const reference
int findMax(const vector<int>& nums) {
    if (nums.empty()) return INT_MIN;
    int maxVal = nums[0];
    for (int x : nums) {
        if (x > maxVal) maxVal = x;
    }
    return maxVal;
}

int main() {
    cout << "Max: " << findMax({10, 5, 25, 8, 30, 2}) << "\n"; // 30
    return 0;
}
```

---

## 12. Factorial using Recursion

### 📝 Problem
Find n! using recursion. `n! = n * (n-1)!`

### 🧪 Test Cases
| Input | Output |
|---|---|
| 5 | 120 |
| 0 | 1 |

### ✅ Solution
```cpp
#include <iostream>
using namespace std;

long long factorial(int n) {
    // Base case
    if (n == 0 || n == 1) return 1;

    // Recursive step
    return n * factorial(n - 1);
}

int main() {
    cout << "5! = " << factorial(5) << "\n";
    return 0;
}
```
> **Memory trace for factorial(3):**
> return 3 * factorial(2)
> → return 2 * factorial(1)
> → → return 1
> → return 2 * 1 = 2
> return 3 * 2 = 6

---

## 13. Fibonacci using Recursion

### 📝 Problem
Find the Nth Fibonacci number. `F(n) = F(n-1) + F(n-2)`

### 🧪 Test Cases
| Input (N) | Output (Nth term) | (Series: 0, 1, 1, 2, 3, 5, 8...) |
|---|---|---|
| 6 | 8 |

### ✅ Solution
```cpp
#include <iostream>
using namespace std;

int fibonacci(int n) {
    // Base cases (0th term = 0, 1st term = 1)
    if (n <= 1) return n;

    // Recursive step
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    cout << "6th Fibonacci: " << fibonacci(6) << "\n"; // 8
    return 0;
}
```
> ⚠️ **Warning:** Pure recursive Fibonacci is **extremely slow** `O(2^N)` because it calculates the same branches multiple times. Real-world uses Dynamic Programming (Memoization).

---

## 14. Sum of Digits using Recursion

### 📝 Problem
Sum the digits of a number. (e.g., 123 → 1+2+3 = 6)

### ✅ Solution
```cpp
#include <iostream>
using namespace std;

int sumOfDigits(int n) {
    // Base case: 1 digit left
    if (n < 10) return n;

    // Last digit + recursion on rest of number
    return (n % 10) + sumOfDigits(n / 10);
}

int main() {
    cout << "Sum(123) = " << sumOfDigits(123) << "\n";
    cout << "Sum(9876) = " << sumOfDigits(9876) << "\n";
    return 0;
}
```

---

## 15. Reverse a String using Recursion

### 📝 Problem
Reverse a string in-place using recursion.

### ✅ Solution
```cpp
#include <iostream>
#include <string>
using namespace std;

void reverseString(string &s, int left, int right) {
    // Base case: pointers crossed or met
    if (left >= right) return;

    // Swap outer characters
    swap(s[left], s[right]);

    // Recursive call moving inwards
    reverseString(s, left + 1, right - 1);
}

// Wrapper function to make calling simple
void reverseStr(string &s) {
    reverseString(s, 0, s.length() - 1);
}

int main() {
    string str = "hello";
    reverseStr(str);
    cout << str << "\n";  // olleh
    return 0;
}
```

---

## 16. Check Palindrome using Recursion

### 📝 Problem
Check if a string is a palindrome.

### ✅ Solution
```cpp
#include <iostream>
#include <string>
using namespace std;

bool isPalindrome(string &s, int left, int right) {
    if (left >= right) return true;            // Base case: fully matched
    if (s[left] != s[right]) return false;     // Mismatch found

    // Move inwards
    return isPalindrome(s, left + 1, right - 1);
}

bool checkPalin(string s) {
    return isPalindrome(s, 0, s.length() - 1);
}

int main() {
    cout << (checkPalin("racecar") ? "Yes" : "No") << "\n";
    cout << (checkPalin("hello") ? "Yes" : "No") << "\n";
    return 0;
}
```

---

## 17. Tower of Hanoi (Classic Recursion)

### 📝 Problem
Move `n` disks from Rod A to Rod C using Rod B.
Rules: Move 1 disk at a time, large disk cannot sit on small disk.

### ✅ Solution
```cpp
#include <iostream>
using namespace std;

// n = number of disks
void towerOfHanoi(int n, char source, char destination, char auxiliary) {
    // Base case: 1 disk
    if (n == 1) {
        cout << "Move disk 1 from " << source << " to " << destination << "\n";
        return;
    }

    // Step 1: Move n-1 disks from Source -> Aux (using Dest as temp)
    towerOfHanoi(n - 1, source, auxiliary, destination);

    // Step 2: Move the largest (nth) disk from Source -> Dest
    cout << "Move disk " << n << " from " << source << " to " << destination << "\n";

    // Step 3: Move n-1 disks from Aux -> Dest (using Source as temp)
    towerOfHanoi(n - 1, auxiliary, destination, source);
}

int main() {
    int disks = 3;
    towerOfHanoi(disks, 'A', 'C', 'B');
    return 0;
}
```
> **Time Complexity:** O(2^N) - It takes 2^N - 1 moves to solve Tower of Hanoi!

---

## 18. Binary Search using Recursion

### 📝 Problem
Search for a target in a sorted array using divide & conquer recursion.

### ✅ Solution
```cpp
#include <iostream>
#include <vector>
using namespace std;

int binarySearch(const vector<int>& v, int left, int right, int target) {
    if (left > right) return -1;  // Not found

    int mid = left + (right - left) / 2;

    if (v[mid] == target) return mid;                 // Found it!
    if (target < v[mid])
        return binarySearch(v, left, mid - 1, target);  // Search Left Half
    else
        return binarySearch(v, mid + 1, right, target); // Search Right Half
}

int main() {
    vector<int> sortedArray = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91};
    int target = 23;

    int index = binarySearch(sortedArray, 0, sortedArray.size() - 1, target);
    cout << "Target " << target << " found at index: " << index << "\n";
    return 0;
}
```

---

## 19. Custom Sort with Lambda Function

### 📝 Problem
Sort an array based on **absolute difference from a target number**, using a Lambda function.

### ✅ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>
using namespace std;

int main() {
    vector<int> v = {10, 5, 20, 2, 8};
    int target = 8;

    // Lambda function used directly inside std::sort
    // We capture 'target' using [&target] or [target]
    sort(v.begin(), v.end(), [target](int a, int b) {
        return abs(a - target) < abs(b - target);
    });

    cout << "Sorted by distance from 8:\n";
    for(int x : v) cout << x << " ";
    // Output: 8 10 5 2 20
    // (Distances: 0, 2, 3, 6, 12)

    return 0;
}
```
> 💡 **Lambda Functions** are incredibly powerful for competitive programming and STL algorithms like `sort()`, `count_if()`, `find_if()`.

---

## 🚨 Final Checklist & Best Practices
1. **Pass objects by `const reference`** `(const string& s)` to avoid copying.
2. Use **Function Prototypes** if writing definitions below `main()`.
3. In recursion, **ALWAYS write the Base Case first**.
4. Use **Lambda functions** for one-off custom sorting/filtering.
5. Default arguments must go **at the end** of the parameter list.

---
*Functions & Recursion Guide | TCS NQT & Competitive Programming*
