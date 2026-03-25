# 🏗️ C++ OOP — Complete Object-Oriented Programming Guide
### Master the 4 Pillars, Memory, and Advanced Concepts | Zero → Hero 🚀

---

## 📌 TABLE OF CONTENTS

### PART A — THE BASICS
1. [What is OOP? (Procedural vs OOP)](#1-what-is-oop-procedural-vs-oop)
2. [Classes & Objects (Syntax & Memory)](#2-classes--objects-syntax--memory)
3. [Access Modifiers (`public`, `private`, `protected`)](#3-access-modifiers-public-private-protected)

### PART B — CORE MECHANICS
4. [Constructors (Default, Parameterized, Copy)](#4-constructors-default-parameterized-copy)
5. [The `this` Keyword](#5-the-this-keyword)
6. [Destructors](#6-destructors)
7. [Static Members (Variables & Functions)](#7-static-members-variables--functions)

### PART C — THE 4 PILLARS OF OOP
8. [Encapsulation (Data Hiding)](#8-encapsulation-data-hiding)
9. [Inheritance (Types & Visibility)](#9-inheritance-types--visibility)
10. [Polymorphism (Compile-time vs Run-time)](#10-polymorphism-compile-time-vs-run-time)
11. [Abstraction (Abstract Classes & Pure Virtual Functions)](#11-abstraction-abstract-classes--pure-virtual-functions)

### PART D — ADVANCED CONCEPTS & INTERVIEW FAVORITES
12. [Friend Class & Friend Function](#12-friend-class--friend-function)
13. [Virtual Destructor (Memory Leak Prevention)](#13-virtual-destructor-memory-leak-prevention)
14. [Shallow Copy vs Deep Copy](#14-shallow-copy-vs-deep-copy)
15. [Struct vs Class](#15-struct-vs-class)

---

# ═══════════════════════════════════
# PART A — THE BASICS
# ═══════════════════════════════════

## 1. What is OOP? (Procedural vs OOP)

**Procedural Programming** (like C) focuses on *functions* (actions).
**Object-Oriented Programming** (like C++) focuses on *data* (objects) and tying functions to that data.

| Feature | Procedural (C) | Object-Oriented (C++/Java) |
|---|---|---|
| Focus | Logic / Functions | Data / Objects |
| Data Security | Poor (Global data is exposed) | High (Data is hidden via Encapsulation) |
| Code Reuse | Harder | Easy (via Inheritance) |
| Paradigm | Top-Down | Bottom-Up |

---

## 2. Classes & Objects (Syntax & Memory)

*   **Class:** A blueprint or template. It takes **0 bytes** of memory!
*   **Object:** A real-world entity created from the blueprint. It takes actual memory.

```cpp
#include <iostream>
#include <string>
using namespace std;

// 1. Define the Blueprint (Class)
class Car {
public: // Access modifier (more on this later)
    string brand;
    int speed;

    void drive() {
        cout << brand << " is driving at " << speed << " km/h.\n";
    }
}; // MUST end with semicolon!

int main() {
    // 2. Create an Object
    Car myCar;

    // 3. Access Members using Dot Operator (.)
    myCar.brand = "Toyota";
    myCar.speed = 120;
    myCar.drive();

    return 0;
}
```

---

## 3. Access Modifiers (`public`, `private`, `protected`)

They control WHO can access the class data.
*   **`private`**: Only the class itself can access. (Default in C++)
*   **`public`**: Anyone outside the class can access.
*   **`protected`**: Only the class and its *children* (Inheritance) can access.

```cpp
class BankAccount {
private:
    double balance; // Hidden from outside world

public:
    string ownerName;

    // Getter function
    double getBalance() {
        return balance;
    }

    // Setter function
    void deposit(double amount) {
        if (amount > 0) balance += amount;
    }
};

int main() {
    BankAccount acc;
    acc.ownerName = "Arjun";  // Allowed (Public)
    // acc.balance = 500;     // ERROR! (Private)

    acc.deposit(500);         // Allowed via public setter
    cout << acc.getBalance(); // Allowed via public getter
}
```

---

# ═══════════════════════════════════
# PART B — CORE MECHANICS
# ═══════════════════════════════════

## 4. Constructors (Default, Parameterized, Copy)

A Constructor is a special function automatically called **when an object is created**.
*   It has the **same name as the class**.
*   It has **no return type** (not even `void`).

```cpp
class Student {
public:
    string name;
    int age;

    // 1. Default Constructor
    Student() {
        name = "Unknown";
        age = 0;
        cout << "Default Constructor called!\n";
    }

    // 2. Parameterized Constructor
    Student(string n, int a) {
        name = n;
        age = a;
        cout << "Parameterized Constructor called!\n";
    }

    // 3. Copy Constructor (Creates object by copying another)
    Student(Student &obj) {
        name = obj.name;
        age = obj.age;
        cout << "Copy Constructor called!\n";
    }
};

int main() {
    Student s1;                  // Calls #1
    Student s2("Arjun", 22);     // Calls #2
    Student s3 = s2;             // Calls #3 (Copy)
    Student s4(s1);              // Calls #3 (Copy)
}
```

---

## 5. The `this` Keyword

`this` is a pointer that points to the object currently calling the member function.
It solves the **"shadowing"** problem when a parameter name is the same as a class property name.

```cpp
class Person {
public:
    int age;

    // Parameter name 'age' shadows class property 'age'
    Person(int age) {
        this->age = age;  // this->age represents the Object's age
    }
};
```

---

## 6. Destructors

A Destructor is called automatically when an object **goes out of scope / is destroyed**.
*   Name is `~ClassName`. No return type, no parameters.
*   Used to free dynamically allocated memory (memory leak prevention!).

```cpp
class FileHandler {
public:
    FileHandler() {
        cout << "File Opened\n";
    }

    ~FileHandler() {
        cout << "File Closed (Destructor called)\n";
    }
};

int main() {
    cout << "Start Main\n";
    if (true) {
        FileHandler f;  // Object created
    } // Object goes out of scope here -> Destructor called NOW!
    cout << "End Main\n";
}
// Output: Start Main -> File Opened -> File Closed -> End Main
```

---

## 7. Static Members (Variables & Functions)

*   **Static Variable:** Shared by ALL objects of the class. It belongs to the class, not individual objects.
*   **Static Function:** Can only access other static members. Called using Class Name (`ClassName::Function`).

```cpp
class Employee {
public:
    string name;
    static int totalCount; // Shared memory

    Employee(string n) {
        name = n;
        totalCount++;
    }

    static void printCount() {
        cout << "Total Employees: " << totalCount << "\n";
    }
};

// Must initialize static variable outside the class
int Employee::totalCount = 0;

int main() {
    Employee e1("Rahul");
    Employee e2("Priya");

    // Call using Class Name (no object needed)
    Employee::printCount(); // Output: 2
}
```

---

# ═══════════════════════════════════
# PART C — THE 4 PILLARS OF OOP
# ═══════════════════════════════════

## 8. Encapsulation (Data Hiding)

**Concept:** Wrapping data (variables) and code (functions) together in a single unit (class), protecting data from outside interference.
**How?** Make variables `private` and provide `public` getter/setter methods. (See Section 3).

---

## 9. Inheritance (Types & Visibility)

**Concept:** A new class (Child/Derived) acquires the properties of an existing class (Parent/Base). Avoids code duplication!

### Types of Inheritance
1. **Single:** A -> B
2. **Multilevel:** A -> B -> C
3. **Multiple:** (A, B) -> C
4. **Hierarchical:** A -> (B, C)

```cpp
// Base Class
class Animal {
public:
    void eat() { cout << "Eating...\n"; }
};

// Derived Class (Single Inheritance)
class Dog : public Animal {
public:
    void bark() { cout << "Barking...\n"; }
};

int main() {
    Dog d1;
    d1.eat();  // Inherited from Animal
    d1.bark(); // Own method
}
```

---

## 10. Polymorphism (Compile-time vs Run-time)

**Concept:** Poly (Many) + Morph (Forms). One name, multiple forms.

### A) Compile-Time (Static) Polymorphism
Achieved via **Function Overloading** or **Operator Overloading**.

```cpp
// Function Overloading
class Math {
public:
    void add(int a, int b) { cout << a + b << "\n"; }
    void add(double a, double b) { cout << a + b << "\n"; } // Same name, diff parameters
};
```

### B) Run-Time (Dynamic) Polymorphism (Crucial for Interviews!)
Achieved via **Virtual Functions** and **Function Overriding**.
*   A base class pointer points to a derived class object.
*   `virtual` tells the compiler: "Wait until runtime to decide which function to call based on the ACTUAL object."

```cpp
class Base {
public:
    // Virtual keyword enables dynamic binding
    virtual void show() { cout << "Base class logic\n"; }
};

class Derived : public Base {
public:
    void show() override { cout << "Derived class logic\n"; }
};

int main() {
    Base* ptr;          // Parent pointer
    Derived obj;        // Child object
    ptr = &obj;         // Valid! Parent can hold child

    ptr->show();        // Outputs: "Derived class logic" (Because of virtual!)
}
```

---

## 11. Abstraction (Abstract Classes & Pure Virtual Functions)

**Concept:** Hiding complex implementation details and showing only essential features.
**How?** An **Abstract Class** is a class containing at least one **Pure Virtual Function**. You CANNOT create objects of an abstract class.

```cpp
class Shape { // Abstract Class
public:
    // Pure Virtual Function (= 0)
    virtual void draw() = 0;
};

class Circle : public Shape {
public:
    // MUST override the pure virtual function, or Circle also becomes Abstract
    void draw() override {
        cout << "Drawing a Circle\n";
    }
};

int main() {
    // Shape s; // ERROR! Cannot instantiate abstract class
    Circle c;
    c.draw();
}
```

---

# ═══════════════════════════════════
# PART D — ADVANCED CONCEPTS & INTERVIEW FAVORITES
# ═══════════════════════════════════

## 12. Friend Class & Friend Function

Normally, private data is strictly hidden. A **friend** is given special access to the private and protected members of another class.

```cpp
class Box {
private:
    int width = 10;

    // Friend Function declaration
    friend void printWidth(Box b);
};

// Function definition (NOT a member function, no Box::)
void printWidth(Box b) {
    cout << "Width: " << b.width << "\n"; // Accessing private data!
}

int main() {
    Box box;
    printWidth(box);
}
```

---

## 13. Virtual Destructor (Memory Leak Prevention)

If you use inheritance and polymorphism (Base pointer to Derived object), you **MUST** make the Base class destructor `virtual`. Otherwise, deleting the pointer only calls the Base destructor, leaving the Derived memory un-deleted (Memory Leak!).

```cpp
class Base {
public:
    Base() { cout << "Base Created\n"; }

    // ALWAYS make Base destructors virtual!
    virtual ~Base() { cout << "Base Destroyed\n"; }
};

class Derived : public Base {
public:
    Derived() { cout << "Derived Created\n"; }
    ~Derived() { cout << "Derived Destroyed\n"; }
};

int main() {
    Base* ptr = new Derived();
    delete ptr;
}
/*
OUTPUT without virtual ~Base():
Base Created -> Derived Created -> Base Destroyed (LEAK!)

OUTPUT with virtual ~Base():
Base Created -> Derived Created -> Derived Destroyed -> Base Destroyed (CLEAN!)
*/
```

---

## 14. Shallow Copy vs Deep Copy

If your class has pointers (dynamic memory `new`), the default copy constructor does a **Shallow Copy** (copies the memory address, so both objects share the same memory pointer).
You must write a custom copy constructor to allocate new memory: a **Deep Copy**.

```cpp
class StringObj {
public:
    char* data;

    StringObj(const char* val) {
        data = new char[100];
        // strcpy(data, val);
    }

    // Custom Deep Copy Constructor
    StringObj(const StringObj& source) {
        data = new char[100]; // Allocate NEW memory
        // strcpy(data, source.data); // Copy the values, not the pointer Address
    }

    ~StringObj() {
        delete[] data;
    }
};
```

---

## 15. Struct vs Class

In C++, `struct` and `class` are almost identical!
**The ONLY difference:**
*   **Struct:** Members are `public` by default.
*   **Class:** Members are `private` by default.

```cpp
struct Node {
    int data;     // Public by default (Great for basic Linked Lists/Trees)
    Node* next;
};
```

---

## 🚨 Final OOP Checklist for Interviews
1. **Pillars:** Encapsulation, Abstraction, Inheritance, Polymorphism.
2. **Runtime Poly:** Requires `virtual` function, Parent Pointer, Child Object.
3. **Abstract Class:** Class with at least one `= 0` pure virtual function. Cannot be instantiated.
4. **Virtual Destructor:** Essential when deleting inherited objects through a base pointer.
5. **Static Members:** Belong to the class, not the object. Keep `static int count` in mind.

---
*Object-Oriented Programming (OOP) Complete Guide | Built for TCS NQT & Placements*
