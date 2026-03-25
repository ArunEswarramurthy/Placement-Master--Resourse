# 🖥️ C++ COMPLETE BASICS — From Zero to Hero
### Learn C++ Step by Step | Full Guide for Beginners

---

## 📌 TABLE OF CONTENTS
1. [Introduction to C++](#1-introduction-to-c)
2. [Setting Up & First Program](#2-setting-up--first-program)
3. [Variables & Data Types](#3-variables--data-types)
4. [Operators](#4-operators)
5. [Input & Output (cin / cout)](#5-input--output-cin--cout)
6. [Conditional Statements (if / else / switch)](#6-conditional-statements-if--else--switch)
7. [Loops (for / while / do-while)](#7-loops-for--while--do-while)
8. [Functions](#8-functions)
9. [Arrays](#9-arrays)
10. [Strings](#10-strings)
11. [Pointers](#11-pointers)
12. [References](#12-references)
13. [Structures (struct)](#13-structures-struct)
14. [Object-Oriented Programming (Classes & Objects)](#14-object-oriented-programming-classes--objects)
15. [Constructors & Destructors](#15-constructors--destructors)
16. [Inheritance](#16-inheritance)
17. [Polymorphism](#17-polymorphism)
18. [File Handling](#18-file-handling)
19. [STL — Standard Template Library](#19-stl--standard-template-library)
20. [Common Patterns & TCS NQT Tips](#20-common-patterns--tcs-nqt-tips)

---

## 1. Introduction to C++

C++ is a **general-purpose programming language** created by Bjarne Stroustrup as an extension of C.

| Feature | Description |
|---|---|
| **Compiled** | Code compiled to machine language → very fast |
| **Strongly Typed** | Every variable has a fixed type |
| **OOP Support** | Classes, Objects, Inheritance, Polymorphism |
| **Low-Level Access** | Pointers, memory management |
| **Standard Library** | STL with vectors, maps, queues, etc. |

> **Why C++ for TCS NQT?**
> C++ is the most popular language in coding rounds.
> Fast execution, rich STL, and full OOP support make it ideal.

---

## 2. Setting Up & First Program

### Install
- **Windows:** Install [MinGW GCC](https://sourceforge.net/projects/mingw/) or use VS Code + C++ extension
- **Online:** Use [repl.it](https://replit.com), [ideone.com](https://ideone.com), or [codeforces.com](https://codeforces.com)

### First Program

```cpp
#include <iostream>      // Include input-output library
using namespace std;     // Use standard namespace

int main() {             // Entry point of every C++ program
    cout << "Hello, World!" << endl;   // Print to screen
    return 0;            // Return 0 means success
}
```

**Output:**
```
Hello, World!
```

### Explanation Line by Line
| Line | Meaning |
|---|---|
| `#include <iostream>` | Include standard input-output library |
| `using namespace std;` | No need to write `std::cout`, just `cout` |
| `int main()` | Main function — program starts here |
| `cout <<` | Print something to screen |
| `endl` | End line (move to next line) = `\n` |
| `return 0;` | Tell OS: program ran successfully |

---

## 3. Variables & Data Types

### Data Types

```cpp
int    a = 10;          // Integer (whole number): -2B to +2B
float  b = 3.14f;       // Decimal (7 decimal places)
double c = 3.14159;     // Decimal (15 decimal places)
char   d = 'A';         // Single character
bool   e = true;        // true or false
long   f = 1234567890L; // Large integer
long long g = 9999999999LL; // Very large integer
string h = "Hello";    // Text (needs #include<string>)
```

### Variable Rules
- Must start with letter or underscore (`_`)
- No spaces, no special characters except `_`
- Case-sensitive: `age` ≠ `Age`

### Constants

```cpp
const int MAX = 100;      // Value cannot change
#define PI 3.14159        // Preprocessor constant (old style)
```

### Type Sizes (Typical)

| Type | Size | Range |
|---|---|---|
| `bool` | 1 byte | 0 or 1 |
| `char` | 1 byte | -128 to 127 |
| `int` | 4 bytes | -2,147,483,648 to 2,147,483,647 |
| `float` | 4 bytes | ~7 decimal digits |
| `double` | 8 bytes | ~15 decimal digits |
| `long long` | 8 bytes | ~9.2 × 10^18 |

```cpp
// Check size
cout << sizeof(int) << endl;     // Output: 4
cout << sizeof(double) << endl;  // Output: 8
```

---

## 4. Operators

### Arithmetic Operators

```cpp
int a = 10, b = 3;

cout << a + b;   // 13  (addition)
cout << a - b;   // 7   (subtraction)
cout << a * b;   // 30  (multiplication)
cout << a / b;   // 3   (integer division — no decimal!)
cout << a % b;   // 1   (modulus / remainder)
```

> ⚠️ **Integer Division:** `10/3 = 3` not `3.33`!
> For decimal: use `(double)a / b` → `10.0/3 = 3.33`

### Relational Operators (return true/false)

```cpp
cout << (a == b);  // Equal to          → 0 (false)
cout << (a != b);  // Not equal         → 1 (true)
cout << (a > b);   // Greater than      → 1 (true)
cout << (a < b);   // Less than         → 0 (false)
cout << (a >= b);  // Greater or equal  → 1 (true)
cout << (a <= b);  // Less or equal     → 0 (false)
```

### Logical Operators

```cpp
bool x = true, y = false;

cout << (x && y);   // AND → false (both must be true)
cout << (x || y);   // OR  → true  (at least one true)
cout << (!x);       // NOT → false (flips the value)
```

### Assignment & Shorthand

```cpp
int n = 5;
n += 3;   // n = n + 3 = 8
n -= 2;   // n = n - 2 = 6
n *= 4;   // n = n * 4 = 24
n /= 6;   // n = n / 6 = 4
n %= 3;   // n = n % 3 = 1
```

### Increment & Decrement

```cpp
int i = 5;
cout << i++;    // Prints 5, then i becomes 6  (post-increment)
cout << ++i;    // i becomes 7, then prints 7  (pre-increment)
cout << i--;    // Prints 7, then i becomes 6  (post-decrement)
cout << --i;    // i becomes 5, then prints 5  (pre-decrement)
```

---

## 5. Input & Output (cin / cout)

### Output with cout

```cpp
#include <iostream>
using namespace std;

int main() {
    int age = 20;
    string name = "Arjun";

    cout << "Name: " << name << endl;
    cout << "Age: " << age << "\n";
    cout << "Sum: " << 10 + 5 << endl;
    return 0;
}
```

### Input with cin

```cpp
int main() {
    int a, b;
    cout << "Enter two numbers: ";
    cin >> a >> b;                    // Read two values
    cout << "Sum = " << a + b << endl;
    return 0;
}
```

### Reading a Full Line

```cpp
string fullName;
cout << "Enter your name: ";
cin.ignore();                         // Clear leftover newline
getline(cin, fullName);               // Read full line with spaces
cout << "Hello, " << fullName << endl;
```

### Formatting Output

```cpp
#include <iomanip>   // For setw, setprecision

cout << fixed << setprecision(2) << 3.14159;  // Output: 3.14
cout << setw(10) << "Hello";                  // Right-aligned in 10 chars
```

---

## 6. Conditional Statements (if / else / switch)

### if / else if / else

```cpp
int marks = 75;

if (marks >= 90) {
    cout << "Grade A" << endl;
} else if (marks >= 75) {
    cout << "Grade B" << endl;    // ← This runs
} else if (marks >= 60) {
    cout << "Grade C" << endl;
} else {
    cout << "Grade F" << endl;
}
```

### Ternary Operator (short if-else)

```cpp
int a = 10, b = 20;
int max = (a > b) ? a : b;    // if a>b then max=a, else max=b
cout << "Max = " << max;       // Output: Max = 20
```

### switch Statement

```cpp
int day = 3;

switch (day) {
    case 1: cout << "Monday"; break;
    case 2: cout << "Tuesday"; break;
    case 3: cout << "Wednesday"; break;   // ← This runs
    case 4: cout << "Thursday"; break;
    case 5: cout << "Friday"; break;
    default: cout << "Weekend"; break;
}
```

> ⚠️ Always add `break;` — without it, execution "falls through" to the next case!

---

## 7. Loops (for / while / do-while)

### for Loop

```cpp
// Syntax: for(init; condition; update)
for (int i = 1; i <= 5; i++) {
    cout << i << " ";
}
// Output: 1 2 3 4 5
```

### while Loop

```cpp
int i = 1;
while (i <= 5) {
    cout << i << " ";
    i++;
}
// Output: 1 2 3 4 5
```

### do-while Loop (runs at least once!)

```cpp
int i = 1;
do {
    cout << i << " ";
    i++;
} while (i <= 5);
// Output: 1 2 3 4 5
```

### Loop Control: break & continue

```cpp
for (int i = 1; i <= 10; i++) {
    if (i == 6) break;        // Stop loop at 6
    if (i % 2 == 0) continue; // Skip even numbers
    cout << i << " ";
}
// Output: 1 3 5
```

### Nested Loops (Pattern Printing)

```cpp
// Print a 4×4 star pattern
for (int i = 1; i <= 4; i++) {
    for (int j = 1; j <= 4; j++) {
        cout << "* ";
    }
    cout << endl;
}
```

```
* * * *
* * * *
* * * *
* * * *
```

---

## 8. Functions

### What is a Function?
A reusable block of code that performs a task.

```cpp
// Syntax:
// return_type function_name(parameters) { body }

int add(int a, int b) {       // Function definition
    return a + b;
}

int main() {
    int result = add(5, 3);   // Function call
    cout << result;            // Output: 8
    return 0;
}
```

### Function Types

```cpp
// 1. No return, no parameter
void greet() {
    cout << "Hello!" << endl;
}

// 2. With return, no parameter
int getAge() {
    return 21;
}

// 3. With parameter, no return
void printName(string name) {
    cout << "Name: " << name << endl;
}

// 4. With parameter AND return
double multiply(double a, double b) {
    return a * b;
}
```

### Default Parameters

```cpp
void greet(string name = "User") {    // Default value
    cout << "Hello, " << name << endl;
}

int main() {
    greet();           // Output: Hello, User
    greet("Arjun");    // Output: Hello, Arjun
    return 0;
}
```

### Function Overloading (Same name, different params)

```cpp
int add(int a, int b)           { return a + b; }
double add(double a, double b)  { return a + b; }
int add(int a, int b, int c)    { return a + b + c; }

// Compiler picks correct version based on arguments!
```

### Recursion (Function calling itself)

```cpp
int factorial(int n) {
    if (n == 0 || n == 1) return 1;    // Base case
    return n * factorial(n - 1);        // Recursive call
}

// factorial(5) = 5 × 4 × 3 × 2 × 1 = 120
```

---

## 9. Arrays

### What is an Array?
A collection of elements of the **same type** stored in contiguous memory.

```cpp
// Declaration & Initialization
int arr[5] = {10, 20, 30, 40, 50};

// Access by index (0-based!)
cout << arr[0];    // 10
cout << arr[2];    // 30
cout << arr[4];    // 50

// Modify
arr[1] = 99;       // Now arr = {10, 99, 30, 40, 50}
```

### Traversing an Array

```cpp
int arr[] = {5, 10, 15, 20, 25};
int n = 5;

for (int i = 0; i < n; i++) {
    cout << arr[i] << " ";
}
// Output: 5 10 15 20 25
```

### 2D Array (Matrix)

```cpp
int matrix[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Access: matrix[row][col]
cout << matrix[1][2];    // Output: 6

// Print entire matrix
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        cout << matrix[i][j] << " ";
    }
    cout << endl;
}
```

### Passing Array to Function

```cpp
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++)
        cout << arr[i] << " ";
}

int main() {
    int a[] = {1, 2, 3, 4, 5};
    printArray(a, 5);    // Output: 1 2 3 4 5
    return 0;
}
```

---

## 10. Strings

### C-style vs C++ Strings

```cpp
// C-style (avoid for most use)
char name[] = "Arjun";

// C++ string (preferred!)
#include <string>
string name = "Arjun";
```

### String Operations

```cpp
string s = "Hello World";

cout << s.length();          // 11  (or s.size())
cout << s[0];                // H   (access character)
cout << s.substr(6, 5);      // World (start=6, length=5)
cout << s.find("World");     // 6   (position found)

s += "!";                    // Concatenate → "Hello World!"
s.replace(0, 5, "Hi");      // "Hi World!"
s.erase(2, 6);               // "Hid!" → erase 6 chars from pos 2

// Convert
cout << s.at(0);             // H (with bounds check)
cout << s.empty();           // 0 (false — not empty)

// Compare
string a = "apple", b = "banana";
cout << (a == b);            // 0 (false)
cout << (a < b);             // 1 (alphabetically a < b)
```

### String Input

```cpp
string name;
cin >> name;                  // Single word only
getline(cin, name);           // Full line with spaces
```

### Useful String Functions

```cpp
#include <algorithm>
string s = "hello";

// Convert to upper / lower
for (char &c : s) c = toupper(c);   // "HELLO"
for (char &c : s) c = tolower(c);   // "hello"

// Reverse
reverse(s.begin(), s.end());         // "olleh"

// Sort
sort(s.begin(), s.end());            // "ehllo"

// Count character
int cnt = count(s.begin(), s.end(), 'l');  // 2
```

---

## 11. Pointers

### What is a Pointer?
A variable that **stores the memory address** of another variable.

```cpp
int a = 10;
int *p = &a;      // p points to the address of a

cout << a;         // 10       (value of a)
cout << &a;        // address  (memory address of a)
cout << p;         // address  (same address, stored in p)
cout << *p;        // 10       (value AT the address = dereference)
```

### Pointer Operations

```cpp
int a = 10;
int *p = &a;

*p = 99;            // Change value through pointer
cout << a;          // 99  (a is changed!)

int b = 20;
p = &b;             // Pointer now points to b
cout << *p;         // 20
```

### Null Pointer

```cpp
int *p = nullptr;   // Modern C++ null pointer (use instead of NULL)
if (p == nullptr)
    cout << "Pointer is null";
```

### Pointer Arithmetic

```cpp
int arr[] = {10, 20, 30, 40, 50};
int *p = arr;        // p points to arr[0]

cout << *p;          // 10
cout << *(p+1);      // 20
cout << *(p+2);      // 30

p++;                 // p now points to arr[1]
cout << *p;          // 20
```

### Pointer to Function (Passing by reference via pointer)

```cpp
void increment(int *p) {
    (*p)++;           // Dereference and increment
}

int main() {
    int x = 5;
    increment(&x);    // Pass address of x
    cout << x;        // 6
    return 0;
}
```

---

## 12. References

### What is a Reference?
An **alias** (another name) for an existing variable.

```cpp
int a = 10;
int &ref = a;       // ref is an alias for a

cout << ref;        // 10
ref = 99;           // Modifies a!
cout << a;          // 99
```

### Pass by Reference in Functions

```cpp
void swap(int &x, int &y) {
    int temp = x;
    x = y;
    y = temp;
}

int main() {
    int a = 5, b = 10;
    swap(a, b);
    cout << a << " " << b;   // Output: 10 5
    return 0;
}
```

> **Reference vs Pointer:**
> - Reference MUST be initialized at creation → safer
> - Pointer can be null and can be reassigned
> - Use references when you don't need null or reassignment

---

## 13. Structures (struct)

### What is a Struct?
A **user-defined data type** that groups different types together.

```cpp
struct Student {
    string name;
    int age;
    float marks;
};

int main() {
    Student s1;                  // Create struct variable
    s1.name = "Arjun";
    s1.age = 20;
    s1.marks = 95.5;

    cout << s1.name << " | " << s1.age << " | " << s1.marks;
    return 0;
}
```

### Struct with Initialization

```cpp
Student s2 = {"Priya", 21, 88.0};    // Direct init
```

### Array of Structs

```cpp
Student class1[3] = {
    {"Arjun", 20, 95},
    {"Priya", 21, 88},
    {"Ravi",  19, 76}
};

for (int i = 0; i < 3; i++) {
    cout << class1[i].name << " : " << class1[i].marks << endl;
}
```

### Struct with Function

```cpp
struct Rectangle {
    int length, width;

    int area() {                    // Member function
        return length * width;
    }
};

Rectangle r = {5, 8};
cout << r.area();    // 40
```

---

## 14. Object-Oriented Programming (Classes & Objects)

### Class vs Struct
- **Struct**: members are public by default
- **Class**: members are private by default → use for OOP

### Class Basics

```cpp
class Car {
private:                      // Only accessible inside class
    string brand;
    int speed;

public:                       // Accessible from outside
    void setBrand(string b) { brand = b; }
    void setSpeed(int s)    { speed = s; }
    string getBrand()       { return brand; }
    int getSpeed()          { return speed; }

    void display() {
        cout << "Brand: " << brand << ", Speed: " << speed << endl;
    }
};

int main() {
    Car myCar;                    // Create object
    myCar.setBrand("Toyota");     // Use public methods
    myCar.setSpeed(120);
    myCar.display();              // Brand: Toyota, Speed: 120
    return 0;
}
```

### Access Specifiers

| Specifier | Accessible From |
|---|---|
| `private` | Inside the class only |
| `public` | Anywhere |
| `protected` | Inside class + subclasses |

### Getters & Setters (Encapsulation)

```cpp
class BankAccount {
private:
    double balance;

public:
    void deposit(double amount)  { balance += amount; }
    void withdraw(double amount) {
        if (amount <= balance) balance -= amount;
        else cout << "Insufficient funds!";
    }
    double getBalance()          { return balance; }
};
```

---

## 15. Constructors & Destructors

### Constructor
- **Special function** called automatically when object is created
- Same name as class, no return type

```cpp
class Student {
public:
    string name;
    int age;

    // Default Constructor
    Student() {
        name = "Unknown";
        age = 0;
        cout << "Student created!" << endl;
    }

    // Parameterized Constructor
    Student(string n, int a) {
        name = n;
        age = a;
    }

    // Copy Constructor
    Student(const Student &s) {
        name = s.name;
        age = s.age;
    }
};

int main() {
    Student s1;                    // Default constructor called
    Student s2("Arjun", 20);       // Parameterized
    Student s3 = s2;               // Copy constructor
    return 0;
}
```

### Constructor Initializer List

```cpp
class Point {
    int x, y;
public:
    Point(int a, int b) : x(a), y(b) {}   // Short and efficient!
    void show() { cout << x << ", " << y; }
};
```

### Destructor
- Called automatically when object is destroyed
- Used to free memory, close files, etc.

```cpp
class Demo {
public:
    Demo()  { cout << "Created" << endl; }
    ~Demo() { cout << "Destroyed" << endl; }
};

int main() {
    Demo d;    // Constructor called
    // ... code ...
    // Destructor called automatically at end of scope
    return 0;
}
```

---

## 16. Inheritance

### What is Inheritance?
A class (child) **inherits** properties and methods from another class (parent).

```cpp
// Parent (Base) class
class Animal {
public:
    string name;

    void eat() { cout << name << " is eating." << endl; }
    void sleep() { cout << name << " is sleeping." << endl; }
};

// Child (Derived) class
class Dog : public Animal {
public:
    void bark() { cout << name << " says: Woof!" << endl; }
};

int main() {
    Dog d;
    d.name = "Buddy";
    d.eat();     // Inherited from Animal
    d.sleep();   // Inherited from Animal
    d.bark();    // Own method
    return 0;
}
```

### Types of Inheritance

```cpp
class A {};
class B : public A    {};   // Public inheritance
class C : protected A {};   // Protected inheritance
class D : private A   {};   // Private inheritance
```

### Multi-level Inheritance

```cpp
class Animal  { public: void breathe() { cout << "Breathing"; } };
class Dog     : public Animal { public: void bark() { cout << "Bark"; } };
class Puppy   : public Dog    { public: void play() { cout << "Play"; } };

// Puppy inherits breathe() and bark() and has play()
```

### Multiple Inheritance

```cpp
class A { public: void funcA() { cout << "A"; } };
class B { public: void funcB() { cout << "B"; } };

class C : public A, public B {    // Inherits from both!
public:
    void funcC() { cout << "C"; }
};

C obj;
obj.funcA();   // A
obj.funcB();   // B
obj.funcC();   // C
```

---

## 17. Polymorphism

### Compile-time Polymorphism (Function Overloading)

```cpp
class Math {
public:
    int square(int n)       { return n * n; }
    double square(double n) { return n * n; }
};
```

### Runtime Polymorphism (Virtual Functions)

```cpp
class Shape {
public:
    virtual void draw() {       // virtual = can be overridden
        cout << "Drawing a shape" << endl;
    }
};

class Circle : public Shape {
public:
    void draw() override {      // Override parent method
        cout << "Drawing a Circle" << endl;
    }
};

class Square : public Shape {
public:
    void draw() override {
        cout << "Drawing a Square" << endl;
    }
};

int main() {
    Shape *s;

    Circle c;
    s = &c;
    s->draw();    // Drawing a Circle  ← Runtime decides!

    Square sq;
    s = &sq;
    s->draw();    // Drawing a Square
    return 0;
}
```

### Abstract Class (Pure Virtual)

```cpp
class Animal {
public:
    virtual void sound() = 0;   // Pure virtual → MUST be overridden
};

class Dog : public Animal {
public:
    void sound() override { cout << "Woof!"; }
};

class Cat : public Animal {
public:
    void sound() override { cout << "Meow!"; }
};
```

---

## 18. File Handling

### Write to File

```cpp
#include <fstream>
using namespace std;

int main() {
    ofstream file("data.txt");      // Open/create file for writing
    file << "Hello, File!" << endl;
    file << "Line 2" << endl;
    file.close();                    // Always close!
    return 0;
}
```

### Read from File

```cpp
#include <fstream>
#include <string>

int main() {
    ifstream file("data.txt");       // Open file for reading
    string line;

    while (getline(file, line)) {    // Read line by line
        cout << line << endl;
    }
    file.close();
    return 0;
}
```

### Append to File

```cpp
ofstream file("data.txt", ios::app);   // Open in append mode
file << "New line added!" << endl;
file.close();
```

---

## 19. STL — Standard Template Library

The STL provides ready-to-use **data structures and algorithms**.

### 📦 vector (Dynamic Array)

```cpp
#include <vector>
using namespace std;

int main() {
    vector<int> v = {3, 1, 4, 1, 5};

    v.push_back(9);           // Add at end
    v.pop_back();              // Remove from end
    v.insert(v.begin(), 0);   // Insert at beginning
    v.erase(v.begin());        // Remove from beginning

    cout << v.size();          // Size
    cout << v[0];              // Access by index
    cout << v.front();         // First element
    cout << v.back();          // Last element

    // Traverse
    for (int x : v) cout << x << " ";

    // Sort
    sort(v.begin(), v.end());
    return 0;
}
```

### 🗺️ map (Key-Value Pairs, Sorted)

```cpp
#include <map>

map<string, int> marks;
marks["Arjun"] = 95;
marks["Priya"] = 88;
marks["Ravi"]  = 76;

cout << marks["Arjun"];    // 95

// Traverse
for (auto &p : marks) {
    cout << p.first << ": " << p.second << endl;
}
```

### 📋 set (Unique Sorted Elements)

```cpp
#include <set>

set<int> s = {5, 3, 1, 4, 1, 2};   // Duplicates removed, sorted
// s = {1, 2, 3, 4, 5}

s.insert(6);
s.erase(3);

for (int x : s) cout << x << " ";  // 1 2 4 5 6
```

### 📬 queue & stack

```cpp
#include <queue>
#include <stack>

// Queue: FIFO
queue<int> q;
q.push(10); q.push(20); q.push(30);
cout << q.front();    // 10
q.pop();              // Remove 10
cout << q.size();     // 2

// Stack: LIFO
stack<int> st;
st.push(10); st.push(20); st.push(30);
cout << st.top();     // 30
st.pop();             // Remove 30
cout << st.top();     // 20
```

### 🔧 Useful Algorithms

```cpp
#include <algorithm>

vector<int> v = {5, 2, 8, 1, 9, 3};

sort(v.begin(), v.end());                          // 1 2 3 5 8 9
sort(v.begin(), v.end(), greater<int>());           // 9 8 5 3 2 1
reverse(v.begin(), v.end());                        // reverse
int mx = *max_element(v.begin(), v.end());          // max = 9
int mn = *min_element(v.begin(), v.end());          // min = 1
int sm = accumulate(v.begin(), v.end(), 0);         // sum
bool found = binary_search(v.begin(), v.end(), 5); // true/false
int cnt = count(v.begin(), v.end(), 5);             // count of 5
```

---

## 20. Common Patterns & TCS NQT Tips

### Pattern 1 — Swap Two Numbers

```cpp
// Method 1: Using temp
int temp = a; a = b; b = temp;

// Method 2: Without temp (XOR)
a = a ^ b; b = a ^ b; a = a ^ b;

// Method 3: STL
swap(a, b);
```

### Pattern 2 — Check Prime

```cpp
bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; i++) {   // Only check up to √n
        if (n % i == 0) return false;
    }
    return true;
}
```

### Pattern 3 — Fibonacci

```cpp
void fibonacci(int n) {
    int a = 0, b = 1;
    for (int i = 0; i < n; i++) {
        cout << a << " ";
        int c = a + b;
        a = b;
        b = c;
    }
}
// fibonacci(7) → 0 1 1 2 3 5 8
```

### Pattern 4 — Reverse a Number

```cpp
int reverseNum(int n) {
    int rev = 0;
    while (n > 0) {
        rev = rev * 10 + n % 10;
        n /= 10;
    }
    return rev;
}
// reverseNum(12345) → 54321
```

### Pattern 5 — Palindrome Check

```cpp
bool isPalindrome(string s) {
    int l = 0, r = s.size() - 1;
    while (l < r) {
        if (s[l] != s[r]) return false;
        l++; r--;
    }
    return true;
}
```

### Pattern 6 — GCD & LCM

```cpp
int gcd(int a, int b) {
    return b == 0 ? a : gcd(b, a % b);   // Euclidean algorithm
}
int lcm(int a, int b) {
    return (a / gcd(a, b)) * b;
}
```

### Pattern 7 — Count Digits

```cpp
int countDigits(int n) {
    int count = 0;
    while (n != 0) { n /= 10; count++; }
    return count;
}
// Or: count = to_string(n).size();
```

### Pattern 8 — Sum of Digits

```cpp
int digitSum(int n) {
    int sum = 0;
    while (n > 0) { sum += n % 10; n /= 10; }
    return sum;
}
```

### Pattern 9 — Sort Array & Find Median

```cpp
vector<int> v = {5, 1, 8, 3, 9};
sort(v.begin(), v.end());
int n = v.size();
double median = (n % 2 == 0) ? (v[n/2-1] + v[n/2]) / 2.0 : v[n/2];
```

### Pattern 10 — Frequency Count using Map

```cpp
string s = "programming";
map<char, int> freq;
for (char c : s) freq[c]++;
for (auto &p : freq) cout << p.first << ": " << p.second << endl;
```

---

## 🚨 Common C++ Mistakes to AVOID

| Mistake ❌ | Correct ✅ |
|---|---|
| `int/int` gives decimal | Use `(double)a/b` for exact division |
| Array index out of bounds | Always check `0 ≤ i < size` |
| Using `=` instead of `==` in if | `if (a == b)` NOT `if (a = b)` |
| Forgetting `break` in switch | Always add `break;` |
| Not initializing variables | Always initialize before use |
| Modifying string while iterating | Use index-based loop |
| Memory leak with `new` | Always `delete` after `new` |
| Not closing files | Always `file.close()` |

---

## 📘 Quick Revision Cheatsheet

```cpp
// BASICS
int a=5; float b=3.14; char c='A'; bool d=true; string s="Hi";

// I/O
cin >> a;  cout << a << endl;  getline(cin, s);

// CONTROL
if(cond){} else{}   for(;;){}   while(){}   do{}while();

// FUNCTIONS
returnType name(params){ return val; }

// ARRAY
int arr[5]={1,2,3,4,5};  arr[i];   int n=sizeof(arr)/sizeof(arr[0]);

// STRING
s.length()  s.substr(i,n)  s.find("x")  s+="more"  reverse(s.begin(),s.end())

// POINTER
int *p=&a;  *p=10;  p++;

// CLASS
class MyClass{ private: int x; public: void set(int v){x=v;} int get(){return x;} };

// STL VECTOR
vector<int> v;  v.push_back(x);  v.size();  sort(v.begin(),v.end());

// STL MAP
map<string,int> m;  m["key"]=val;  m.count("key");

// USEFUL
sort()  reverse()  max_element()  min_element()  binary_search()  accumulate()
```

---

> **✅ You now know C++ from Basics to OOP to STL!**
>
> **Next Steps:**
> 1. Practice each topic with small programs
> 2. Solve problems on HackerRank / LeetCode / CodeChef
> 3. Learn DSA (Data Structures & Algorithms) using C++
>
> **Practice Order:** Variables → Loops → Arrays → Functions → Strings → OOP → STL

---
*C++ Complete Guide | Made for TCS NQT & Competitive Programming*
