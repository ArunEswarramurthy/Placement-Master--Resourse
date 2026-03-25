# ☕ JAVA CORE: Absolute Basics & Syntax
### The Foundation of Java Mastery | Zero → Hero 🚀

---

## 📌 TABLE OF CONTENTS

1. [Why Java? (How it works under the hood)](#1-why-java-how-it-works-under-the-hood)
2. [Boilerplate Code (The "Hello World" Breakdown)](#2-boilerplate-code-the-hello-world-breakdown)
3. [Variables & Data Types (Primitives vs Objects)](#3-variables--data-types-primitives-vs-objects)
4. [Type Casting (Implicit vs Explicit)](#4-type-casting-implicit-vs-explicit)
5. [Input vs Output (`Scanner` & `System.out`)](#5-input-vs-output-scanner--systemout)
6. [Operators & Math Tricks](#6-operators--math-tricks)
7. [Control Flow (If/Else, Switch, Ternary)](#7-control-flow-ifelse-switch-ternary)
8. [Loops (For, While, Do-While, Enhanced For)](#8-loops-for-while-do-while-enhanced-for)

---

## 1. Why Java? (How it works under the hood)

Unlike C++ which compiles directly to machine code (.exe), Java uses a **Two-Step Process**. This makes Java **Platform Independent** ("Write Once, Run Anywhere").

1. **Compiler (`javac`):** Converts your `.java` code into `.class` files (Bytecode).
2. **JVM (Java Virtual Machine):** Reads the `.class` Bytecode and runs it on the specific OS (Windows, Mac, Linux).

*   **JDK (Java Development Kit):** Has everything you need to *write* and *run* Java.
*   **JRE (Java Runtime Environment):** Only has what you need to *run* Java.
*   **JVM:** The engine that actually runs the code.

---

## 2. Boilerplate Code (The "Hello World" Breakdown)

In Java, **EVERYTHING MUST BE INSIDE A CLASS.** Even the main function.
The file name MUST exactly match the `public class` name.

```java
// File: Main.java
public class Main {
    // The entry point of EVERY Java program
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

**Breakdown of `public static void main(String[] args)`:**
*   `public` - Anyone can run this method (needed for the JVM to find it).
*   `static` - We don't need to create an object of `Main` to run the method.
*   `void` - Does not return a value.
*   `main` - The name the JVM looks for.
*   `String[] args` - Array of strings used for command-line arguments.

---

## 3. Variables & Data Types (Primitives vs Objects)

### A) The 8 Primitive Types (Stored purely as values)
| Type | Size | Example | Default Value |
|---|---|---|---|
| `byte` | 1 byte | `120` | `0` |
| `short` | 2 bytes | `30000` | `0` |
| `int` | 4 bytes | `20000000` | `0` |
| `long` | 8 bytes | `9000000000L` | `0L` (Note the 'L') |
| `float` | 4 bytes | `3.14f` | `0.0f` (Note the 'f') |
| `double` | 8 bytes | `3.14159` | `0.0d` |
| `char` | 2 bytes | `'A'` | `\u0000` |
| `boolean`| 1 bit | `true` | `false` |

### B) Non-Primitive (Reference Types)
These refer to Objects in memory. They start with a **Capital Letter**.
Examples: `String`, `Arrays`, `Classes`, `Interfaces`. Default value is `null`.

```java
int myNum = 5;               // Primitive
String myText = "Hello";     // Reference Type
```

---

## 4. Type Casting (Implicit vs Explicit)

### Widening (Implicit / Automatic Casting)
Converting a smaller type to a larger type size. No data is lost.
`byte` → `short` → `char` → `int` → `long` → `float` → `double`
```java
int myInt = 9;
double myDouble = myInt; // Automatic casting: int to double
System.out.println(myDouble); // Outputs 9.0
```

### Narrowing (Explicit / Manual Casting)
Converting a larger type to a smaller size. MUST be done manually! Can lose data.
`double` → `float` → `long` → `int` → `char` → `short` → `byte`
```java
double myDouble = 9.78d;
int myInt = (int) myDouble; // Manual casting: double to int
System.out.println(myInt); // Outputs 9 (Decimal is chopped off!)
```

---

## 5. Input vs Output (`Scanner` & `System.out`)

### Output
```java
System.out.print("Hello");      // Prints on same line
System.out.println("Hello");    // Prints and moves to next line
System.out.printf("Num: %d", 5);// Formatted print (like C)
```

### Input (`Scanner`)
Always `import java.util.Scanner;`
```java
import java.util.Scanner;

public class InputExample {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in); // Open Scanner on Keyboard

        System.out.print("Enter your age: ");
        int age = sc.nextInt();

        // ⚠️ THE SCANNER PITFALL (Important for NQT!)
        sc.nextLine(); // Consume the leftover "\n" after reading a number!

        System.out.print("Enter your name: ");
        String name = sc.nextLine();

        System.out.println(name + " is " + age + " years old.");
        sc.close(); // Prevent memory leak!
    }
}
```

---

## 6. Operators & Math Tricks

Java operators act the same as C++.
*   `%` (Modulo) gets the remainder. `10 % 3 = 1`.
*   `/` (Division) of two `int`s chops off decimals! `5 / 2 = 2`. (To get 2.5, use `5.0 / 2`).

### `Math` Class Cheatsheet
```java
Math.max(5, 10);     // 10
Math.min(5, 10);     // 5
Math.sqrt(64);       // 8.0 (Returns double)
Math.abs(-4.7);      // 4.7
Math.pow(2, 3);      // 8.0 (2 to the power 3)
Math.random();       // Random double between 0.0 (inclusive) and 1.0 (exclusive)
```

---

## 7. Control Flow (If/Else, Switch, Ternary)

### If / Else
```java
int time = 20;
if (time < 18) {
    System.out.println("Good day.");
} else if (time == 20) {
    System.out.println("Good evening.");
} else {
    System.out.println("Good night.");
}
```

### Ternary Operator (Shorthand If)
Syntax: `condition ? true_value : false_value;`
```java
int time = 20;
String result = (time < 18) ? "Good day." : "Good evening.";
System.out.println(result);
```

### Switch Statement (with Java 14+ Enhanced Switch)
```java
int day = 4;
// Old way
switch(day) {
    case 1: System.out.println("Monday"); break;
    case 2: System.out.println("Tuesday"); break;
    default: System.out.println("Weekend");
}

// Java 14+ "Arrow" Switch (No breaks needed!)
switch (day) {
    case 1 -> System.out.println("Monday");
    case 2 -> System.out.println("Tuesday");
    default -> System.out.println("Weekend");
}
```

---

## 8. Loops (For, While, Do-While, Enhanced For)

### For Loop (When you know exactly how many times)
```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

### While Loop (When you don't know the exact count)
```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

### Do-While Loop (GUARANTEED to run at least ONCE)
Even if the condition is false immediately, the body runs once.
```java
int i = 100;
do {
    System.out.println(i); // Will print 100!
    i++;
}
while (i < 5);
```

### Enhanced For-Loop (For-Each) - Best for Arrays & Collections!
Reads literally as: "For each `fruit` in `fruits` array".
```java
String[] fruits = {"Apple", "Banana", "Cherry"};
for (String fruit : fruits) {
    System.out.println(fruit);
}
```

---
*Core Java Mastery | Part 1: Syntax & Basics | Prepared for TCS NQT & Technical Interviews*
