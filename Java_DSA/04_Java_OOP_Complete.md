# 🏗️ JAVA OOP: The Ultimate Object-Oriented Guide
### Master the 4 Pillars, Interfaces, and Memory Rules in Java 🚀

---

## 📌 TABLE OF CONTENTS

### PART A — CLASSES & OBJECTS
1. [Classes, Objects, and the `new` keyword](#1-classes-objects-and-the-new-keyword)
2. [Constructors (Default, Parameterized, Copy)](#2-constructors-default-parameterized-copy)
3. [The `this` Keyword (Preventing Shadowing)](#3-the-this-keyword-preventing-shadowing)
4. [Access Modifiers (`public`, `private`, `protected`, `default`)](#4-access-modifiers-public-private-protected-default)

### PART B — THE "STATIC" & "FINAL" KEYWORDS
5. [The `static` Keyword (Variables, Methods, Blocks)](#5-the-static-keyword-variables-methods-blocks)
6. [The `final` Keyword (Variables, Methods, Classes)](#6-the-final-keyword-variables-methods-classes)

### PART C — THE 4 PILLARS OF OOP
7. [Encapsulation (Getters & Setters)](#7-encapsulation-getters--setters)
8. [Inheritance (`extends` and `super`)](#8-inheritance-extends-and-super)
9. [Polymorphism (Method Overloading vs Overriding)](#9-polymorphism-method-overloading-vs-overriding)
10. [Abstraction (Abstract Classes)](#10-abstraction-abstract-classes)

### PART D — ADVANCED JAVA SPECIFICS
11. [Interfaces (`implements` and Default Methods)](#11-interfaces-implements-and-default-methods)
12. [Abstract Class vs Interface (Interview Favorite)](#12-abstract-class-vs-interface-interview-favorite)
13. [Object Class (`toString()` and `equals()`)](#13-object-class-tostring-and-equals)

---

# ═══════════════════════════════════
# PART A — CLASSES & OBJECTS
# ═══════════════════════════════════

## 1. Classes, Objects, and the `new` keyword

In Java, *everything* revolves around Objects.
*   **Class:** A logical template/blueprint (Memory is NOT allocated).
*   **Object:** A physical reality of the class (Memory IS allocated dynamically in the **Heap**).

```java
class Car {
    String brand;  // Instance Variable
    int speed;     // Instance Variable

    void drive() { // Method
        System.out.println(brand + " is driving at " + speed + " mph.");
    }
}

public class Main {
    public static void main(String[] args) {
        // The 'new' keyword dynamically allocates memory in the Heap!
        Car myCar = new Car(); 
        
        myCar.brand = "Toyota";
        myCar.speed = 120;
        myCar.drive();
    }
}
```

---

## 2. Constructors (Default, Parameterized, Copy)

A Constructor is called **exactly once** when an object is created using `new`.
*   It has the **exact same name** as the class.
*   It has **NO return type** (not even `void`).

```java
class Student {
    String name;
    int roll;

    // 1. Default Constructor (Java provides an empty one if you don't write ANY constructors)
    Student() {
        name = "Unknown";
        roll = 0;
    }

    // 2. Parameterized Constructor
    Student(String name, int roll) {
        // We will fix the shadowing problem below!
        this.name = name;
        this.roll = roll;
    }

    // 3. Copy Constructor (Java does NOT have a default copy constructor like C++)
    Student(Student other) {
        this.name = other.name;
        this.roll = other.roll;
    }
}
```

---

## 3. The `this` Keyword (Preventing Shadowing)

`this` is a reference variable that refers to the **current object**.
The most common use is to solve **Variable Shadowing**: When a local variable/parameter has the exact same name as an instance variable.

```java
class Employee {
    String name;  // Instance variable

    Employee(String name) { // Local parameter
        // name = name; // BAD! Shadowing. The instance variable remains null.
        this.name = name; // GOOD! "this.name" specifically means the class's variable.
    }
    
    void printIntro() {
        // You can also use 'this' to call other methods in the same class
        this.doWork(); 
    }
    
    void doWork() { System.out.println("Working..."); }
}
```

---

## 4. Access Modifiers

Who is allowed to see your data?

| Modifier | Inside Class | Inside Package | Outside Package (Child Class) | Outside Package (Any Class) |
|---|---|---|---|---|
| `private` | ✅ Yes | ❌ No | ❌ No | ❌ No |
| `default` (no keyword) | ✅ Yes | ✅ Yes | ❌ No | ❌ No |
| `protected` | ✅ Yes | ✅ Yes | ✅ Yes (crucial!) | ❌ No |
| `public` | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |

> 💡 **Best Practice:** Keep variables `private`. Keep methods `public`. Do not use default unless specifically doing package-level development.

---

# ═══════════════════════════════════
# PART B — THE "STATIC" & "FINAL" KEYWORDS
# ═══════════════════════════════════

## 5. The `static` Keyword (Variables, Methods, Blocks)

If a member is `static`, it belongs to the **Class itself**, NOT the objects. All objects share the exact same `static` variable.

```java
class Counter {
    int instanceCount = 0;        // Every object gets its own copy (Starts at 0)
    static int globalCount = 0;   // Shared across ALL objects

    Counter() {
        instanceCount++;
        globalCount++;
    }
}

public class Main {
    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        
        System.out.println(c1.instanceCount); // 1
        System.out.println(c2.instanceCount); // 1
        
        // Static variables should be accessed via the Class name!
        System.out.println(Counter.globalCount); // 2
    }
}
```

### Static Methods Rule:
A `static` method can ONLY safely access other `static` variables/methods. It **cannot** use `this` or `super` because it does not belong to an object!

---

## 6. The `final` Keyword (Variables, Methods, Classes)

`final` means **"Cannot be Changed"**.

1.  **`final` Variable:** Creates a **Constant**. `final int MAX_SPEED = 120; // Cannot change this later`
2.  **`final` Method:** Prevents Method Overriding (Children cannot change what the parents wrote).
3.  **`final` Class:** Prevents Inheritance completely. `final class String { ... }` means you cannot write `class MyString extends String`.

---

# ═══════════════════════════════════
# PART C — THE 4 PILLARS OF OOP
# ═══════════════════════════════════

## 7. Encapsulation (Getters & Setters)

**Concept:** Hiding internal data (`private`) and exposing safe ways to modify it (`public` getters/setters). This prevents external classes from putting your object into an invalid state.

```java
class BankAccount {
    private double balance = 0; // HIDING DATA

    // GETTER (Read-only access)
    public double getBalance() {
        return balance;
    }

    // SETTER (Write access with RULES)
    public void deposit(double amount) {
        if (amount > 0) { // Validating data!
            balance += amount;
        }
    }
}
```

---

## 8. Inheritance (`extends` and `super`)

**Concept:** A Child class inherits fields and methods from a Parent class. Java supports Single & Multilevel inheritance, but **NOT** Multiple Inheritance (with classes).

*   Use **`extends`** to inherit.
*   Use **`super`** to call the parent's constructor or methods.

```java
// Parent / Superclass
class Animal {
    String name;
    
    Animal(String name) {
        this.name = name;
    }
    
    void eat() {
        System.out.println(name + " is eating.");
    }
}

// Child / Subclass
class Dog extends Animal {
    String breed;
    
    Dog(String name, String breed) {
        super(name); // MUST BE THE FIRST LINE: Calls Parent Constructor!
        this.breed = breed;
    }
    
    void bark() {
        // Can access inherited variables
        System.out.println(name + " barks loudly!"); 
    }
}
```

---

## 9. Polymorphism (Method Overloading vs Overriding)

**Concept:** Poly (Many) + Morph (Forms). Ability to perform a single action in different ways.

### A) Compile-Time (Overloading)
Same method name, different parameters. Solved at compile time.
`void add(int a, int b)` vs `void add(double a, double b)`.

### B) Run-Time (Overriding) - CRITICAL!
Child class provides a specific implementation of a method already in the Parent class.
You use `@Override` to tell the compiler to check it.

**Dynamic Method Dispatch:** When a Parent reference points to a Child object, Java waits until **runtime** to decide which overridden method to call!

```java
class Animal {
    void sound() { System.out.println("Animal makes a noise"); }
}

class Cat extends Animal {
    @Override // Good practice!
    void sound() { System.out.println("Meow!"); }
}

public class Main {
    public static void main(String[] args) {
        // Parent Reference -> Child Object
        Animal myPet = new Cat(); 
        
        // Java asks at runtime: "Is this actually a Cat in memory?"
        myPet.sound(); // Output: Meow!
    }
}
```

---

## 10. Abstraction (Abstract Classes)

**Concept:** Hiding implementation details and only showing functionality to the user.
An **Abstract Class** cannot be instantiated (you cannot `new` it). It exists strictly to be inherited from. It can have standard methods AND abstract methods (methods without a body!).

```java
abstract class Shape {
    String color;
    
    // Abstract method (No body! Child MUST implement this)
    abstract void draw();
    
    // Regular method
    void setColor(String c) { color = c; }
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing a circle...");
    }
}
```

---

# ═══════════════════════════════════
# PART D — ADVANCED JAVA SPECIFICS
# ═══════════════════════════════════

## 11. Interfaces (`implements` and Default Methods)

An Interface is a completely abstract "contract". Historically, all methods in an interface were abstract.
**Why do we need this?** Because Java doesn't support Multiple Inheritance for classes! However, a class can `implement` as many interfaces as it wants!

```java
interface Flyable {
    void fly(); // Automatically public and abstract!
}

interface Swimmable {
    void swim();
}

// Duck implements MULTIPLE interfaces!
class Duck implements Flyable, Swimmable {
    public void fly() { System.out.println("Duck flying"); }
    public void swim() { System.out.println("Duck swimming"); }
}
```

### Java 8 Default Methods
To add new methods to an ancient interface without breaking millions of classes that already implement it, Java 8 added `default` methods in interfaces. They HAVE a body!
```java
interface Vehicle {
    void start();
    
    default void honk() { // Has a body!
        System.out.println("Beep beep!");
    }
}
```

---

## 12. Abstract Class vs Interface (Interview Favorite)

| Feature | Abstract Class (`abstract`) | Interface (`interface`) |
|---|---|---|
| Multiple Inheritance | ❌ Class can only extend ONE. | ✅ Class can implement MULTIPLE. |
| Fields | Can have ANY variables (`final`, non-final, `static`, non-static). | Fields are ALWAYS `public static final` (Constants). |
| Methods | Can have both abstract and concrete methods. | Historically only abstract. (Now allows `default` and `static`). |
| Constructors | ✅ Yes, called when child is instantiated. | ❌ No constructors allowed. |
| When to use? | Core Identity ("A Dog IS AN Animal"). | Capabilities ("A Dog CAN Walkable"). |

---

## 13. Object Class (`toString()` and `equals()`)

In Java, **EVERY** class secretly inherits from the root `java.lang.Object` class.
This class gives you methods like `toString()` and `equals()`, which you should regularly `@Override`.

```java
class Person {
    String name;
    int id;

    Person(String name, int id) { this.name = name; this.id = id; }

    // Overriding toString() prevents printing memory hashes!
    @Override
    public String toString() {
        return "Person[Name: " + name + ", ID: " + id + "]";
    }
    
    // Overriding equals() to compare logical equality, rather than memory addresses
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true; // Same memory
        if (obj == null || this.getClass() != obj.getClass()) return false;
        
        Person other = (Person) obj; // Cast
        return this.id == other.id && this.name.equals(other.name);
    }
}
```

---
*Java OOP Mastery | Built for TCS NQT, Product Companies & Technical Interviews*
