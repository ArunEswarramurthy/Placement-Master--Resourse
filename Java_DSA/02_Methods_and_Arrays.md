# 🛠️ JAVA METHODS & ARRAYS
### Method Overloading, Pass-by-Value Traps, and N-Dimensional Arrays 🚀

---

## 📌 TABLE OF CONTENTS

1. [Understanding Methods (Syntax & Return Types)](#1-understanding-methods-syntax--return-types)
2. [Method Overloading (Compile-Time Polymorphism)](#2-method-overloading-compile-time-polymorphism)
3. [The "Pass by Value" Trap in Java ⚠️](#3-the-pass-by-value-trap-in-java-)
4. [Introduction to Arrays (1D)](#4-introduction-to-arrays-1d)
5. [Multi-Dimensional Arrays (2D)](#5-multi-dimensional-arrays-2d)
6. [The `Arrays` Utility Class (Sorting, Searching, Printing)](#6-the-arrays-utility-class-sorting-searching-printing)
7. [Variable Arguments (Varargs)](#7-variable-arguments-varargs)

---

## 1. Understanding Methods (Syntax & Return Types)

A method is a block of code which only runs when it is called.
Java methods **must** be declared within a class.

### Syntax:
```java
public class Main {
    // A method that returns an int
    static int addNumbers(int a, int b) {
        return a + b;
    }

    // A method that returns nothing (void)
    static void printGreeting(String name) {
        System.out.println("Hello, " + name + "!");
    }

    public static void main(String[] args) {
        int sum = addNumbers(5, 10);
        System.out.println("Sum: " + sum);
        printGreeting("Arjun");
    }
}
```
*   **`static`**: Means the method belongs to the `Main` class itself, not an object of the `Main` class. You can call it directly from `main()`.

---

## 2. Method Overloading (Compile-Time Polymorphism)

With method overloading, multiple methods can have the **same name with different parameters**.
Java distinguishes them by their **Method Signature** (Number, Type, or Order of parameters).

```java
public class MathUtil {
    // 1. Accepts two ints
    static int plusMethod(int x, int y) {
        return x + y;
    }

    // 2. Accepts two doubles
    static double plusMethod(double x, double y) {
        return x + y;
    }

    // 3. Accepts three ints
    static int plusMethod(int x, int y, int z) {
        return x + y + z;
    }

    public static void main(String[] args) {
        int myNum1 = plusMethod(8, 5);           // Calls #1
        double myNum2 = plusMethod(4.3, 6.26);   // Calls #2
        int myNum3 = plusMethod(1, 2, 3);        // Calls #3
    }
}
```
> ⚠️ **Note:** You cannot overload based on the **Return Type** alone!

---

## 3. The "Pass by Value" Trap in Java ⚠️

**CRITICAL INTERVIEW CONCEPT:**
Unlike C++, **Java is ALWAYS Pass-by-Value**. It NEVER passes by reference.
However, for objects/arrays, the *value* of the reference (pointer address) is passed!

### A) Passing Primitives (Copies)
Modifying the parameter does **not** affect the original variable.
```java
static void modifyPrimitive(int num) {
    num = 100; // Only changes local copy!
}
int x = 10;
modifyPrimitive(x); // x is still 10!
```

### B) Passing Objects/Arrays (Copies of References)
Modifying the *contents* of the array affects the original, but modifying the *variable itself* does not!
```java
static void modifyArrayContents(int[] arr) {
    arr[0] = 99; // THIS WORKS! Affects the original array.
}

static void reassignArray(int[] arr) {
    arr = new int[]{1, 2, 3}; // FAILS! Only reassigns local pointer copy.
}

public static void main(String[] args) {
    int[] nums = {10, 20};
    modifyArrayContents(nums); // nums becomes {99, 20}
    reassignArray(nums);       // nums is STILL {99, 20}!
}
```

---

## 4. Introduction to Arrays (1D)

Arrays are fixed in size once created. They store multiple values of the *same type*.
They are **Objects** in Java, so they use the `new` keyword implicitly or explicitly.

```java
// Declaration & Initialization
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
int[] myNum = {10, 20, 30, 40};

// Fixed Size Initialization (Default values: 0 for int, null for Objects)
int[] marks = new int[5]; // Creates an array of 5 zeros.

// Access & Modify
System.out.println(cars[0]); // Output: Volvo
cars[0] = "Opel";            // Change value

// Array Length Properties (NO PARENTHESES!)
System.out.println(cars.length); // 4

// Traversal (For-Each loop is best!)
for (String car : cars) {
    System.out.println(car);
}
```

---

## 5. Multi-Dimensional Arrays (2D)

A 2D array is an array of arrays. Useful for representing grids/matrices.

```java
public class Matrix {
    public static void main(String[] args) {
        // Initialization
        int[][] myNumbers = {
            {1, 2, 3, 4},
            {5, 6, 7}
        };

        // Access (Row 1, Column 2 -> Element 7)
        System.out.println(myNumbers[1][2]);

        // Creating an empty grid (e.g., 3 rows, 4 columns)
        int[][] dp = new int[3][4];

        // Traversal using Nested Loops
        for (int row = 0; row < myNumbers.length; ++row) {
            for (int col = 0; col < myNumbers[row].length; ++col) {
                System.out.print(myNumbers[row][col] + " ");
            }
            System.out.println();
        }
    }
}
```

---

## 6. The `Arrays` Utility Class (Sorting, Searching, Printing)

Java gives you a powerful utility class to handle generic array operations instantly.
**Always `import java.util.Arrays;`**

```java
import java.util.Arrays;

public class ArrayUtils {
    public static void main(String[] args) {
        int[] arr = {5, 2, 8, 1, 9};

        // 1. Print array quickly (Without loop!)
        // Important: Arrays.toString() is required, printing "arr" prints a memory hash!
        System.out.println(Arrays.toString(arr)); // Output: [5, 2, 8, 1, 9]

        // 2. Sorting (O(N log N) Dual-Pivot Quicksort)
        Arrays.sort(arr);
        System.out.println(Arrays.toString(arr)); // Output: [1, 2, 5, 8, 9]

        // 3. Binary Search (Must be sorted first!)
        int index = Arrays.binarySearch(arr, 8);
        System.out.println("Index of 8: " + index); // Output: 3

        // 4. Fill an array with a specific value
        int[] dp = new int[5];
        Arrays.fill(dp, -1);
        System.out.println(Arrays.toString(dp)); // Output: [-1, -1, -1, -1, -1]

        // 5. Check if two arrays are equal
        int[] arr1 = {1, 2, 3};
        int[] arr2 = {1, 2, 3};
        System.out.println(Arrays.equals(arr1, arr2)); // Output: true
    }
}
```

---

## 7. Variable Arguments (Varargs)

You can pass a varying number of arguments of the same type to a method.
It looks like an array to the method internally.

```java
public class Main {
    // '...' means Varargs. It MUST be the LAST parameter.
    static int sum(int... numbers) {
        int total = 0;
        // 'numbers' acts exactly like int[]
        for (int num : numbers) {
            total += num;
        }
        return total;
    }

    public static void main(String[] args) {
        System.out.println(sum(10, 20));          // 30
        System.out.println(sum(1, 2, 3, 4, 5));   // 15
        System.out.println(sum());                // 0
    }
}
```

---
*Core Java Mastery | Part 2: Methods & Arrays | Prepared for TCS NQT & Technical Interviews*
