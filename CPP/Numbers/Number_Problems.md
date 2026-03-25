# 🔢 NUMBER BASED PROBLEMS — Most Important Questions
### Each Problem: 5 Test Cases + Solution Without STL + Solution With STL

---

## 📌 TABLE OF CONTENTS
1. [Check Prime Number](#1-check-prime-number)
2. [Factorial of N](#2-factorial-of-n)
3. [Fibonacci Series](#3-fibonacci-series)
4. [Palindrome Number](#4-palindrome-number)
5. [Armstrong Number](#5-armstrong-number)
6. [Reverse a Number](#6-reverse-a-number)
7. [Count Digits](#7-count-digits)
8. [Sum of Digits](#8-sum-of-digits)
9. [GCD and LCM](#9-gcd-and-lcm)
10. [Power of a Number (Fast Exponentiation)](#10-power-of-a-number-fast-exponentiation)
11. [Check Perfect Number](#11-check-perfect-number)
12. [Find All Divisors](#12-find-all-divisors)
13. [Prime Factorization](#13-prime-factorization)
14. [Sieve of Eratosthenes (All Primes up to N)](#14-sieve-of-eratosthenes-all-primes-up-to-n)
15. [Number to Binary / Binary to Number](#15-number-to-binary--binary-to-number)

---

## 1. Check Prime Number

### 📝 Problem
A **prime number** is divisible only by 1 and itself. Check if a number is prime.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | 7 | Prime ✅ |
| 2 | 15 | Not Prime ❌ (3×5) |
| 3 | 1 | Not Prime ❌ (by definition) |
| 4 | 2 | Prime ✅ (smallest prime) |
| 5 | 97 | Prime ✅ |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

bool isPrime(int n) {
    if (n < 2) return false;       // 0, 1 are not prime
    if (n == 2) return true;       // 2 is prime
    if (n % 2 == 0) return false;  // Even numbers > 2 are not prime

    // Check odd divisors only up to sqrt(n) — KEY OPTIMIZATION!
    for (int i = 3; i * i <= n; i += 2) {
        if (n % i == 0) return false;
    }
    return true;
}

int main() {
    int n;
    cin >> n;
    cout << (isPrime(n) ? "Prime" : "Not Prime") << endl;

    // Test all cases
    int tests[] = {7, 15, 1, 2, 97};
    for (int t : tests)
        cout << t << " → " << (isPrime(t) ? "Prime" : "Not Prime") << endl;
    return 0;
}
```

```
Output:
7  → Prime
15 → Not Prime
1  → Not Prime
2  → Prime
97 → Prime
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

bool isPrime(int n) {
    if (n < 2) return false;
    if (n == 2) return true;
    if (n % 2 == 0) return false;

    // Use sqrt from <cmath>
    int sqrtN = (int)sqrt(n);
    for (int i = 3; i <= sqrtN; i += 2)
        if (n % i == 0) return false;
    return true;
}

int main() {
    vector<int> tests = {7, 15, 1, 2, 97};
    for (int n : tests)
        cout << n << " → " << (isPrime(n) ? "Prime" : "Not Prime") << "\n";
    return 0;
}
```

> 💡 **Key Insight:** Only check up to **√n** — if n has a factor larger than √n, it must also have one smaller. Skipping even numbers halves the iterations.

---

## 2. Factorial of N

### 📝 Problem
Find **n!** = 1 × 2 × 3 × ... × n. (`0! = 1` by definition)

### 🧪 Test Cases
| # | Input (n) | Output (n!) |
|---|---|---|
| 1 | 0 | 1 |
| 2 | 1 | 1 |
| 3 | 5 | 120 |
| 4 | 10 | 3628800 |
| 5 | 12 | 479001600 |

---

### ✅ Solution WITHOUT STL (Iterative)

```cpp
#include <iostream>
using namespace std;

long long factorialIterative(int n) {
    long long result = 1;
    for (int i = 2; i <= n; i++)
        result *= i;
    return result;
}

// Recursive version
long long factorialRecursive(int n) {
    if (n == 0 || n == 1) return 1;   // Base case
    return n * factorialRecursive(n - 1);
}

int main() {
    int tests[] = {0, 1, 5, 10, 12};
    for (int n : tests)
        cout << n << "! = " << factorialIterative(n) << endl;
    return 0;
}
```

```
Output:
0!  = 1
1!  = 1
5!  = 120
10! = 3628800
12! = 479001600
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <numeric>
#include <vector>
using namespace std;

int main() {
    int n = 5;

    vector<int> v(n);
    iota(v.begin(), v.end(), 1);   // Fill with 1,2,3,4,5

    // Multiply all elements together
    long long fact = accumulate(v.begin(), v.end(), 1LL, multiplies<long long>());

    cout << n << "! = " << fact << endl;   // 120
    return 0;
}
```

> 💡 **Key Insight:** Use `long long` — factorial grows very fast. For n=20: 2,432,902,008,176,640,000 (overflows `int`!).

---

## 3. Fibonacci Series

### 📝 Problem
Print the first **N Fibonacci numbers** (0, 1, 1, 2, 3, 5, 8, 13...).

### 🧪 Test Cases
| # | Input (N) | Output |
|---|---|---|
| 1 | 1 | `0` |
| 2 | 5 | `0 1 1 2 3` |
| 3 | 7 | `0 1 1 2 3 5 8` |
| 4 | 10 | `0 1 1 2 3 5 8 13 21 34` |
| 5 | 3 | `0 1 1` |

---

### ✅ Solution WITHOUT STL (Iterative — O(n))

```cpp
#include <iostream>
using namespace std;

void fibonacci(int n) {
    if (n <= 0) return;

    long long a = 0, b = 1;
    cout << a;                    // Print first term

    for (int i = 1; i < n; i++) {
        cout << " " << b;
        long long next = a + b;
        a = b;
        b = next;
    }
    cout << endl;
}

// Recursive version (slower — O(2^n) but elegant)
long long fibRecursive(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    return fibRecursive(n-1) + fibRecursive(n-2);
}

int main() {
    fibonacci(7);     // 0 1 1 2 3 5 8
    fibonacci(10);    // 0 1 1 2 3 5 8 13 21 34
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n = 10;
    vector<long long> fib(n);

    fib[0] = 0;
    if (n > 1) fib[1] = 1;

    for (int i = 2; i < n; i++)
        fib[i] = fib[i-1] + fib[i-2];

    for (long long x : fib) cout << x << " ";
    // Output: 0 1 1 2 3 5 8 13 21 34
    return 0;
}
```

> 💡 **Key Insight:** Iterative is O(n). Recursive is O(2^n) — very slow for large n. Use **Dynamic Programming** (store results in array) for efficiency.

---

## 4. Palindrome Number

### 📝 Problem
A number is a **palindrome** if it reads the same forwards and backwards (e.g., 121, 1221).

### 🧪 Test Cases
| # | Input | Palindrome? |
|---|---|---|
| 1 | 121 | Yes ✅ |
| 2 | 123 | No ❌ |
| 3 | -121 | No ❌ (negative: reversed is 121-) |
| 4 | 1221 | Yes ✅ |
| 5 | 10 | No ❌ (reversed: 01 = 1 ≠ 10) |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

bool isPalindrome(int n) {
    if (n < 0) return false;      // Negative numbers can't be palindromes

    int original = n;
    int reversed = 0;

    while (n > 0) {
        int digit = n % 10;          // Get last digit
        reversed = reversed * 10 + digit;  // Build reversed number
        n /= 10;                     // Remove last digit
    }

    return original == reversed;
}

int main() {
    int tests[] = {121, 123, -121, 1221, 10};
    for (int n : tests)
        cout << n << " → " << (isPalindrome(n) ? "Palindrome" : "Not Palindrome") << endl;
    return 0;
}
```

```
Output:
121  → Palindrome
123  → Not Palindrome
-121 → Not Palindrome
1221 → Palindrome
10   → Not Palindrome
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

bool isPalindrome(int n) {
    if (n < 0) return false;

    string s = to_string(n);              // Convert to string
    string rev = s;
    reverse(rev.begin(), rev.end());      // Reverse the string
    return s == rev;
}

int main() {
    vector<int> tests = {121, 123, -121, 1221, 10};
    for (int n : tests)
        cout << n << " → " << (isPalindrome(n) ? "Palindrome" : "Not Palindrome") << "\n";
    return 0;
}
```

> 💡 **Key Insight:** Both methods work. String approach is cleaner. Numeric approach avoids string conversion overhead.

---

## 5. Armstrong Number

### 📝 Problem
An **Armstrong number** (Narcissistic) equals the **sum of its digits each raised to the power of the number of digits**.
Example: 153 = 1³ + 5³ + 3³ = 1 + 125 + 27 = 153 ✅

### 🧪 Test Cases
| # | Input | Armstrong? | Calculation |
|---|---|---|---|
| 1 | 153 | Yes ✅ | 1³+5³+3³ = 153 |
| 2 | 370 | Yes ✅ | 3³+7³+0³ = 370 |
| 3 | 9474 | Yes ✅ | 9⁴+4⁴+7⁴+4⁴ = 9474 |
| 4 | 100 | No ❌ | 1³+0³+0³ = 1 ≠ 100 |
| 5 | 1634 | Yes ✅ | 1⁴+6⁴+3⁴+4⁴ = 1634 |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
#include <cmath>
using namespace std;

bool isArmstrong(int n) {
    int original = n;
    int digits = 0;
    int temp = n;

    // Count digits
    while (temp > 0) { digits++; temp /= 10; }

    // Sum of each digit raised to power of digit count
    long long sum = 0;
    temp = n;
    while (temp > 0) {
        int digit = temp % 10;
        sum += (long long)pow(digit, digits);
        temp /= 10;
    }

    return sum == original;
}

int main() {
    int tests[] = {153, 370, 9474, 100, 1634};
    for (int n : tests)
        cout << n << " → " << (isArmstrong(n) ? "Armstrong" : "Not Armstrong") << endl;
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <string>
#include <cmath>
using namespace std;

bool isArmstrong(int n) {
    string s = to_string(n);
    int d = s.size();            // Number of digits
    long long sum = 0;

    for (char c : s)
        sum += (long long)pow(c - '0', d);   // c-'0' converts char to int

    return sum == n;
}

int main() {
    vector<int> tests = {153, 370, 9474, 100, 1634};
    for (int n : tests)
        cout << n << " → " << (isArmstrong(n) ? "Armstrong" : "Not Armstrong") << "\n";
    return 0;
}
```

> 💡 **Key Insight:** `c - '0'` converts a char digit to integer. `'5' - '0' = 5`. Use `long long` for large powers.

---

## 6. Reverse a Number

### 📝 Problem
Reverse the digits of a number. Handle negatives and trailing zeros.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | 12345 | 54321 |
| 2 | -123 | -321 |
| 3 | 100 | 1 (leading zero dropped) |
| 4 | 7 | 7 |
| 5 | 1000000003 | 3000000001 |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

long long reverseNumber(long long n) {
    bool negative = (n < 0);
    if (negative) n = -n;        // Work with positive

    long long rev = 0;
    while (n > 0) {
        rev = rev * 10 + n % 10;   // Add last digit to front
        n /= 10;
    }

    return negative ? -rev : rev;
}

int main() {
    long long tests[] = {12345, -123, 100, 7, 1000000003};
    for (long long n : tests)
        cout << n << " → " << reverseNumber(n) << endl;
    return 0;
}
```

```
Output:
12345      → 54321
-123       → -321
100        → 1
7          → 7
1000000003 → 3000000001
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

long long reverseNumber(long long n) {
    bool negative = (n < 0);
    string s = to_string(negative ? -n : n);
    reverse(s.begin(), s.end());
    return (negative ? -1 : 1) * stoll(s);   // stoll: string to long long
}

int main() {
    vector<long long> tests = {12345, -123, 100, 7, 1000000003};
    for (long long n : tests)
        cout << n << " → " << reverseNumber(n) << "\n";
    return 0;
}
```

> 💡 **Key Insight:** `stoi()` = string to int, `stol()` = string to long, `stoll()` = string to long long.

---

## 7. Count Digits

### 📝 Problem
Count the **number of digits** in a number.

### 🧪 Test Cases
| # | Input | Digits |
|---|---|---|
| 1 | 0 | 1 |
| 2 | 7 | 1 |
| 3 | 123 | 3 |
| 4 | 100000 | 6 |
| 5 | -9999 | 4 (ignore sign) |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

int countDigits(long long n) {
    if (n == 0) return 1;
    if (n < 0) n = -n;          // Handle negatives

    int count = 0;
    while (n > 0) {
        count++;
        n /= 10;
    }
    return count;
}

int main() {
    long long tests[] = {0, 7, 123, 100000, -9999};
    for (long long n : tests)
        cout << n << " has " << countDigits(n) << " digit(s)" << endl;
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <string>
#include <cmath>
using namespace std;

int main() {
    vector<long long> tests = {0, 7, 123, 100000, -9999};
    for (long long n : tests) {
        // Method 1: Convert to string
        int cnt1 = to_string(abs(n)).size();

        // Method 2: log10 formula (only for n > 0)
        int cnt2 = (n == 0) ? 1 : (int)log10(abs(n)) + 1;

        cout << n << " → " << cnt1 << " digits\n";
    }
    return 0;
}
```

> 💡 **Key Insight:** `floor(log10(n)) + 1` gives digit count for n > 0. But string method is cleaner and safer.

---

## 8. Sum of Digits

### 📝 Problem
Find the **sum of all digits** of a number.

### 🧪 Test Cases
| # | Input | Digit Sum |
|---|---|---|
| 1 | 123 | 6 (1+2+3) |
| 2 | 9999 | 36 (9+9+9+9) |
| 3 | 0 | 0 |
| 4 | 100 | 1 (1+0+0) |
| 5 | -456 | 15 (4+5+6, ignore sign) |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

int digitSum(long long n) {
    if (n < 0) n = -n;       // Handle negative
    int sum = 0;
    while (n > 0) {
        sum += n % 10;        // Add last digit
        n /= 10;
    }
    return sum;
}

// Digital root: keep summing until single digit
int digitalRoot(int n) {
    while (n >= 10) n = digitSum(n);
    return n;
}

int main() {
    long long tests[] = {123, 9999, 0, 100, -456};
    for (long long n : tests)
        cout << n << " → digit sum = " << digitSum(n) << endl;

    cout << "Digital root of 9875 = " << digitalRoot(9875) << endl; // 9+8+7+5=29→2+9=11→1+1=2
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <string>
#include <numeric>
using namespace std;

int main() {
    vector<long long> tests = {123, 9999, 0, 100, -456};
    for (long long n : tests) {
        string s = to_string(abs(n));
        int sum = accumulate(s.begin(), s.end(), 0, [](int acc, char c){
            return acc + (c - '0');
        });
        cout << n << " → " << sum << "\n";
    }
    return 0;
}
```

> 💡 **Key Insight:** Digital root shortcut: `digitalRoot(n) = 1 + (n-1)%9` for n > 0. (Number theory trick!)

---

## 9. GCD and LCM

### 📝 Problem
Find **GCD** (Greatest Common Divisor) and **LCM** (Least Common Multiple).

### 🧪 Test Cases
| # | a | b | GCD | LCM |
|---|---|---|---|---|
| 1 | 12 | 18 | 6 | 36 |
| 2 | 7 | 13 | 1 | 91 |
| 3 | 100 | 75 | 25 | 300 |
| 4 | 0 | 5 | 5 | 0 |
| 5 | 48 | 36 | 12 | 144 |

---

### ✅ Solution WITHOUT STL (Euclidean Algorithm — O(log min(a,b)))

```cpp
#include <iostream>
using namespace std;

int gcd(int a, int b) {
    // Euclidean algorithm: gcd(a,b) = gcd(b, a%b)
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// Recursive version
int gcdRecursive(int a, int b) {
    return b == 0 ? a : gcdRecursive(b, a % b);
}

int lcm(int a, int b) {
    return (a / gcd(a, b)) * b;   // Avoid overflow: divide first!
}

int main() {
    int tests[][2] = {{12,18},{7,13},{100,75},{0,5},{48,36}};
    for (auto &t : tests) {
        int a = t[0], b = t[1];
        cout << "GCD(" << a << "," << b << ")=" << gcd(a,b)
             << "  LCM=" << lcm(a,b) << endl;
    }
    return 0;
}
```

---

### ✅ Solution WITH STL (C++17)

```cpp
#include <iostream>
#include <numeric>    // gcd and lcm available in C++17
using namespace std;

int main() {
    vector<pair<int,int>> tests = {{12,18},{7,13},{100,75},{5,5},{48,36}};
    for (auto &[a, b] : tests) {
        cout << "GCD(" << a << "," << b << ")=" << gcd(a,b)
             << "  LCM=" << lcm(a,b) << "\n";
    }
    return 0;
}
```

> 💡 **Key Insight:** Always compute LCM as `(a/gcd)*b` NOT `a*b/gcd` — avoids integer overflow!

---

## 10. Power of a Number (Fast Exponentiation)

### 📝 Problem
Compute **a^b** (a to the power b) efficiently.

### 🧪 Test Cases
| # | a | b | a^b |
|---|---|---|---|
| 1 | 2 | 10 | 1024 |
| 2 | 3 | 5 | 243 |
| 3 | 5 | 0 | 1 |
| 4 | 2 | 30 | 1073741824 |
| 5 | 7 | 3 | 343 |

---

### ✅ Solution WITHOUT STL (Binary Exponentiation — O(log b))

```cpp
#include <iostream>
using namespace std;

long long fastPow(long long base, long long exp) {
    long long result = 1;

    while (exp > 0) {
        if (exp % 2 == 1)             // If exp is odd
            result *= base;           // Multiply current base
        base *= base;                 // Square the base
        exp /= 2;                     // Halve the exponent
    }
    return result;
}

// With modulo (common in competitive programming)
long long fastPowMod(long long base, long long exp, long long mod) {
    long long result = 1;
    base %= mod;
    while (exp > 0) {
        if (exp & 1) result = result * base % mod;
        base = base * base % mod;
        exp >>= 1;
    }
    return result;
}

int main() {
    cout << fastPow(2, 10) << endl;   // 1024
    cout << fastPow(3, 5)  << endl;   // 243
    cout << fastPow(5, 0)  << endl;   // 1
    cout << fastPow(2, 30) << endl;   // 1073741824

    // With mod 1e9+7
    cout << fastPowMod(2, 30, 1000000007) << endl;
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    // Using pow() from <cmath>
    cout << (long long)pow(2, 10) << endl;   // 1024
    cout << (long long)pow(3, 5)  << endl;   // 243

    // WARNING: pow() uses floating point — cast carefully!
    // For exact results with large int, use fastPow() above
    return 0;
}
```

> 💡 **Key Insight:** Binary exponentiation is O(log b) vs O(b) naive. **Always use with modulo** in competitive programming!

---

## 11. Check Perfect Number

### 📝 Problem
A **perfect number** equals the sum of its proper divisors (all divisors except itself).
Example: 28 = 1+2+4+7+14 = 28 ✅

### 🧪 Test Cases
| # | Input | Perfect? | Divisors |
|---|---|---|---|
| 1 | 6 | Yes ✅ | 1+2+3=6 |
| 2 | 28 | Yes ✅ | 1+2+4+7+14=28 |
| 3 | 496 | Yes ✅ | Sum=496 |
| 4 | 12 | No ❌ | 1+2+3+4+6=16≠12 |
| 5 | 1 | No ❌ | No proper divisors |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

bool isPerfect(int n) {
    if (n <= 1) return false;

    int sum = 1;    // 1 is always a divisor
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            sum += i;
            if (i != n / i) sum += n / i;   // Add both divisors
        }
    }
    return sum == n;
}

int main() {
    int tests[] = {6, 28, 496, 12, 1};
    for (int n : tests)
        cout << n << " → " << (isPerfect(n) ? "Perfect" : "Not Perfect") << endl;
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <numeric>
using namespace std;

bool isPerfect(int n) {
    if (n <= 1) return false;
    vector<int> divisors;
    divisors.push_back(1);
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            divisors.push_back(i);
            if (i != n/i) divisors.push_back(n/i);
        }
    }
    return accumulate(divisors.begin(), divisors.end(), 0) == n;
}

int main() {
    for (int n : {6, 28, 496, 12, 1})
        cout << n << " → " << (isPerfect(n) ? "Perfect" : "Not Perfect") << "\n";
    return 0;
}
```

---

## 12. Find All Divisors

### 📝 Problem
Find and print all **divisors** of a number in sorted order.

### 🧪 Test Cases
| # | Input | Divisors |
|---|---|---|
| 1 | 12 | 1 2 3 4 6 12 |
| 2 | 28 | 1 2 4 7 14 28 |
| 3 | 7 | 1 7 |
| 4 | 36 | 1 2 3 4 6 9 12 18 36 |
| 5 | 1 | 1 |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

void findDivisors(int n) {
    cout << "Divisors of " << n << ": ";
    for (int i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            cout << i << " ";
            if (i != n / i) cout << n / i << " ";   // Pair divisor
        }
    }
    cout << endl;
}

int main() {
    findDivisors(12);   // 1 2 3 4 6 12 (unsorted)
    findDivisors(36);
    return 0;
}
```

---

### ✅ Solution WITH STL (Sorted Output)

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

vector<int> getDivisors(int n) {
    vector<int> divs;
    for (int i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            divs.push_back(i);
            if (i != n / i) divs.push_back(n / i);
        }
    }
    sort(divs.begin(), divs.end());   // Sort for clean output
    return divs;
}

int main() {
    for (int n : {12, 28, 7, 36, 1}) {
        cout << "Divisors of " << n << ": ";
        for (int d : getDivisors(n)) cout << d << " ";
        cout << "\n";
    }
    return 0;
}
```

> 💡 **Key Insight:** Loop only up to **√n** — for every divisor i, there's a pair n/i. This gives O(√n) instead of O(n).

---

## 13. Prime Factorization

### 📝 Problem
Express a number as a product of its **prime factors**.

### 🧪 Test Cases
| # | Input | Prime Factors |
|---|---|---|
| 1 | 12 | 2² × 3 |
| 2 | 36 | 2² × 3² |
| 3 | 100 | 2² × 5² |
| 4 | 13 | 13 (prime itself) |
| 5 | 360 | 2³ × 3² × 5 |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

void primeFactors(int n) {
    cout << n << " = ";
    bool first = true;

    // Divide by 2 first
    while (n % 2 == 0) {
        if (!first) cout << " × ";
        cout << 2;
        n /= 2;
        first = false;
    }

    // Then check odd factors from 3
    for (int i = 3; i * i <= n; i += 2) {
        while (n % i == 0) {
            if (!first) cout << " × ";
            cout << i;
            n /= i;
            first = false;
        }
    }

    // If n > 1, it's a prime factor
    if (n > 1) {
        if (!first) cout << " × ";
        cout << n;
    }
    cout << endl;
}

int main() {
    int tests[] = {12, 36, 100, 13, 360};
    for (int n : tests) primeFactors(n);
    return 0;
}
```

```
Output:
12  = 2 × 2 × 3
36  = 2 × 2 × 3 × 3
100 = 2 × 2 × 5 × 5
13  = 13
360 = 2 × 2 × 2 × 3 × 3 × 5
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <map>
using namespace std;

map<int,int> primeFactorization(int n) {
    map<int,int> factors;   // prime → exponent
    for (int i = 2; i * i <= n; i++) {
        while (n % i == 0) {
            factors[i]++;
            n /= i;
        }
    }
    if (n > 1) factors[n]++;
    return factors;
}

int main() {
    for (int n : {12, 36, 100, 13, 360}) {
        cout << n << " = ";
        auto f = primeFactorization(n);
        bool first = true;
        for (auto &[p, e] : f) {
            if (!first) cout << " × ";
            cout << p;
            if (e > 1) cout << "^" << e;
            first = false;
        }
        cout << "\n";
    }
    return 0;
}
```

```
Output:
12  = 2^2 × 3
36  = 2^2 × 3^2
100 = 2^2 × 5^2
13  = 13
360 = 2^3 × 3^2 × 5
```

---

## 14. Sieve of Eratosthenes (All Primes up to N)

### 📝 Problem
Find **all prime numbers up to N** efficiently.

### 🧪 Test Cases
| # | N | Primes |
|---|---|---|
| 1 | 10 | 2 3 5 7 |
| 2 | 20 | 2 3 5 7 11 13 17 19 |
| 3 | 2 | 2 |
| 4 | 50 | 2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 |
| 5 | 1 | (none) |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

void sieve(int n) {
    bool isPrime[n + 1];

    // Initialize all as true
    for (int i = 0; i <= n; i++) isPrime[i] = true;

    isPrime[0] = isPrime[1] = false;   // 0 and 1 are not prime

    for (int i = 2; i * i <= n; i++) {
        if (isPrime[i]) {
            // Mark all multiples of i as not prime
            for (int j = i * i; j <= n; j += i)
                isPrime[j] = false;
        }
    }

    cout << "Primes up to " << n << ": ";
    for (int i = 2; i <= n; i++)
        if (isPrime[i]) cout << i << " ";
    cout << endl;
}

int main() {
    sieve(50);
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> sieve(int n) {
    vector<bool> isPrime(n + 1, true);
    isPrime[0] = isPrime[1] = false;

    for (int i = 2; i * i <= n; i++) {
        if (isPrime[i]) {
            for (int j = i * i; j <= n; j += i)
                isPrime[j] = false;
        }
    }

    vector<int> primes;
    for (int i = 2; i <= n; i++)
        if (isPrime[i]) primes.push_back(i);

    return primes;
}

int main() {
    auto primes = sieve(50);
    for (int p : primes) cout << p << " ";
    // Output: 2 3 5 7 11 13 17 19 23 29 31 37 41 43 47
    return 0;
}
```

> 💡 **Key Insight:** Sieve is O(n log log n) — much faster than checking each number individually. Start marking from **i×i** (not 2×i) to avoid redundant work.

---

## 15. Number to Binary / Binary to Number

### 📝 Problem
Convert a **decimal number to binary** and vice versa.

### 🧪 Test Cases
| # | Decimal | Binary |
|---|---|---|
| 1 | 5 | 101 |
| 2 | 10 | 1010 |
| 3 | 255 | 11111111 |
| 4 | 0 | 0 |
| 5 | 1024 | 10000000000 |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

// Decimal → Binary
void decToBin(int n) {
    if (n == 0) { cout << "0"; return; }

    int binary[32];
    int idx = 0;

    while (n > 0) {
        binary[idx++] = n % 2;   // Get last bit
        n /= 2;
    }

    cout << "Binary: ";
    for (int i = idx - 1; i >= 0; i--)   // Print in reverse
        cout << binary[i];
    cout << endl;
}

// Binary → Decimal
int binToDec(long long binary) {
    int decimal = 0, base = 1;
    while (binary > 0) {
        int bit = binary % 10;
        decimal += bit * base;
        base *= 2;
        binary /= 10;
    }
    return decimal;
}

int main() {
    decToBin(5);     // 101
    decToBin(10);    // 1010
    decToBin(255);   // 11111111

    cout << binToDec(101)      << endl;    // 5
    cout << binToDec(1010)     << endl;    // 10
    cout << binToDec(11111111) << endl;    // 255
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <bitset>
#include <string>
using namespace std;

int main() {
    // Decimal → Binary using bitset
    int n = 10;
    cout << bitset<8>(n) << endl;   // 00001010 (8-bit)
    cout << bitset<4>(n) << endl;   // 1010 (4-bit)

    // Or use to_string approach
    n = 255;
    string bin = "";
    int temp = n;
    while (temp > 0) { bin = char('0' + temp%2) + bin; temp /= 2; }
    cout << bin << "\n";   // 11111111

    // Binary string → Decimal using stoi with base 2
    string binStr = "1010";
    int decimal = stoi(binStr, nullptr, 2);   // base 2
    cout << binStr << " → " << decimal << "\n";   // 10

    return 0;
}
```

> 💡 **Key Insight:** `bitset<N>(n)` — N is the bit width. `stoi(s, nullptr, base)` converts any base to decimal.

---

## 📘 Quick Reference — All Patterns

| Problem | Key Algorithm | Time | Space |
|---|---|---|---|
| Prime Check | Loop to √n | O(√n) | O(1) |
| Factorial | Iterative loop | O(n) | O(1) |
| Fibonacci | Iterative two-var | O(n) | O(1) |
| Palindrome | Reverse & compare | O(log n) | O(1) |
| Armstrong | Digit extraction | O(log n) | O(1) |
| Reverse Number | Digit extraction | O(log n) | O(1) |
| Count Digits | log10 or loop | O(log n) | O(1) |
| Digit Sum | Digit extraction | O(log n) | O(1) |
| GCD | Euclidean | O(log min) | O(1) |
| Power | Binary exponentiation | O(log b) | O(1) |
| Perfect Number | Divisor sum | O(√n) | O(1) |
| All Divisors | Loop to √n | O(√n) | O(√n) |
| Prime Factorization | Trial division | O(√n) | O(log n) |
| Sieve of Eratosthenes | Sieve | O(n log log n) | O(n) |
| Dec ↔ Binary | Bit extraction | O(log n) | O(log n) |

---

## 🚨 Common Mistakes to AVOID

| Mistake ❌ | Correct ✅ |
|---|---|
| `pow(i, n)` returns float | Cast: `(long long)pow(i,n)` or use `fastPow` |
| `int` overflow in factorial | Use **`long long`** for n > 12 |
| Checking prime with `i < n` | Only check **`i * i <= n`** |
| GCD: `a*b/gcd(a,b)` overflow | Use **`(a/gcd)*b`** |
| Sieve: marking from `2*i` | Start from **`i*i`** (optimization) |
| `1` is prime | **1 is NOT prime** by definition |

---
*Number Problems Guide | TCS NQT & Competitive Programming | With & Without STL*
