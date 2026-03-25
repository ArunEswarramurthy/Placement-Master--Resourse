# 📦 JAVA GENERICS & WRAPPERS
### Type Safety, Autoboxing, and `<T>` Explained! 🚀

---

## 📌 TABLE OF CONTENTS

1. [Wrapper Classes (Primitives vs Objects)](#1-wrapper-classes-primitives-vs-objects)
2. [Autoboxing & Unboxing (The Magic Conversion)](#2-autoboxing--unboxing-the-magic-conversion)
3. [Why Generics? (The Problem with `Object`)](#3-why-generics-the-problem-with-object)
4. [Creating Generic Classes (`class Box<T>`)](#4-creating-generic-classes-class-boxt)
5. [Generic Methods (`<T> void print(T item)`)](#5-generic-methods-t-void-printt-item)
6. [Bounded Generics (`<T extends Number>`)](#6-bounded-generics-t-extends-number)
7. [Wildcards (`?`, `? extends T`, `? super T`)](#7-wildcards---extends-t--super-t)

---

## 1. Wrapper Classes (Primitives vs Objects)

In Java, Collections like `ArrayList` and `HashMap` **cannot store primitive data types** (`int`, `double`, `char`). They can only store Objects.
To fix this, Java provides a **Wrapper Class** for every primitive data type to "wrap" the primitive into an Object.

| Primitive Type | Wrapper Class |
|---|---|
| `byte` | `Byte` |
| `short` | `Short` |
| `int` | **`Integer`** (Careful, not Int!) |
| `long` | `Long` |
| `float` | `Float` |
| `double` | `Double` |
| `char` | **`Character`** |
| `boolean` | `Boolean` |

---

## 2. Autoboxing & Unboxing (The Magic Conversion)

You don't have to manually write `new Integer(5)` anymore (in fact, it's deprecated!). The Java compiler converts them automatically.

*   **Autoboxing:** Converting a primitive into its Wrapper Object automatically.
*   **Unboxing:** Converting a Wrapper Object back into a primitive automatically.

```java
import java.util.ArrayList;

public class WrapperExample {
    public static void main(String[] args) {
        // Autoboxing: The int '5' is automatically converted to an Integer object!
        Integer myObj = 5; 

        // Unboxing: The Integer object is automatically converted back to an int!
        int primitive = myObj; 

        // Why we need them: ArrayLists!
        // ArrayList<int> list = new ArrayList<>(); // ERROR! Primitives not allowed.
        ArrayList<Integer> list = new ArrayList<>(); // SUCCESS!
        list.add(10); // Autoboxing happens here!
    }
}
```

---

## 3. Why Generics? (The Problem with `Object`)

Before Java 5, Collections stored EVERYTHING as an `Object`. This caused massive crashes if you accidentally put a String into a List of Integers! Generics fix this by enforcing **Type Safety** at compile time.

```java
// THE OLD WAY (Pre-Java 5) 🔴 DANGEROUS!
ArrayList oldList = new ArrayList();
oldList.add("Arjun");
oldList.add(10); // Allowed! But wait...

// Crash at runtime! We expected Strings, but got an integer!
String name = (String) oldList.get(1); // ClassCastException!

// THE NEW WAY (With Generics) 🟢 SAFE!
ArrayList<String> safeList = new ArrayList<>();
safeList.add("Arjun");
// safeList.add(10); // COMPILER ERROR! Cannot add int to List of Strings.
```

---

## 4. Creating Generic Classes (`class Box<T>`)

You can create your own classes that work with ANY variable type using `<T>` (where T stands for Type). Standard naming conventions:
*   `T` = Type
*   `E` = Element (used in Collections)
*   `K` = Key, `V` = Value (used in Maps)

```java
// 1. Define the Generic Class
class Box<T> {
    private T item; // T can be Integer, String, Employee... anything!

    public void setItem(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }
}

public class Main {
    public static void main(String[] args) {
        // 2. Instantiate with a Specific Type
        Box<String> stringBox = new Box<>(); // Only accepts Strings
        stringBox.setItem("Hello World");
        System.out.println(stringBox.getItem());

        Box<Integer> intBox = new Box<>(); // Only accepts Integers
        intBox.setItem(99);
        System.out.println(intBox.getItem());
    }
}
```

---

## 5. Generic Methods (`<T> void print(T item)`)

You can write a single method that accepts an array of ANY type and processes it!

```java
public class GenericMethodExample {
    
    // The `<T>` must go BEFORE the return type `void`!
    static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.print(element + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        // Must use Wrapper classes for arrays if using Generics!
        Integer[] intArray = {1, 2, 3, 4, 5};
        String[] strArray = {"Java", "Python", "C++"};

        // One method prints BOTH types!
        printArray(intArray);
        printArray(strArray);
    }
}
```

---

## 6. Bounded Generics (`<T extends Number>`)

What if you want a Generic Class that accepts ONLY numbers (Integer, Double, Float), but strictly rejects Strings? Use Bounded Generics!

```java
// T MUST be a subclass of Number (Integer, Double, etc.)
class MathBox<T extends Number> {
    T num;
    MathBox(T num) { this.num = num; }

    double getSquare() {
        // Because of "extends Number", we know T definitely has .doubleValue()
        return num.doubleValue() * num.doubleValue();
    }
}

public class Main {
    public static void main(String[] args) {
        MathBox<Integer> m1 = new MathBox<>(5);     // Works!
        MathBox<Double> m2 = new MathBox<>(5.5);    // Works!
        
        // MathBox<String> m3 = new MathBox<>("Hi"); // COMPILER ERROR! String is not a Number.
        System.out.println(m1.getSquare()); // 25.0
    }
}
```

---

## 7. Wildcards (`?`, `? extends T`, `? super T`)

Wildcards are used in method parameters when dealing with Collections of generic types.
**The Problem:** `List<Integer>` is NOT a subclass of `List<Number>`, even though `Integer` is a subclass of `Number`.

```java
import java.util.List;
import java.util.Arrays;

public class WildcardExample {

    // 1. Unbounded Wildcard `<?>`: Accepts List of literally ANYTHING.
    static void printAnyList(List<?> list) {
        for (Object obj : list) System.out.print(obj + " ");
    }

    // 2. Upper Bounded `<? extends Number>`: Accepts Number, Integer, Double...
    // Useful when you ONLY want to READ data.
    static double sumList(List<? extends Number> list) {
        double sum = 0;
        for (Number num : list) {
            sum += num.doubleValue();
        }
        return sum;
    }

    // 3. Lower Bounded `<? super Integer>`: Accepts Integer, Number, Object...
    // Useful when you want to ADD data to a list safely.
    static void addNumbers(List<? super Integer> list) {
        list.add(50);
        list.add(100);
    }

    public static void main(String[] args) {
        List<Integer> intList = Arrays.asList(1, 2, 3);
        List<Double> doubleList = Arrays.asList(1.1, 2.2);

        System.out.println(sumList(intList));    // Works!
        System.out.println(sumList(doubleList)); // Works!
    }
}
```

---

## 🚨 Generics Final Checklist!
1. **No Primitives!** `<int>` is forbidden. Use `<Integer>`.
2. **Type Erasure:** Generics are a compile-time feature. The JVM removes (`erases`) all `<T>` at runtime to ensure backwards compatibility. You cannot do `new T()`.
3. Auto-boxing happens automatically. Don't waste time typing `new Integer(5)`.

---
*Java Core Mastery | Generics & Wrappers | Prepared for TCS NQT & Technical Interviews*
