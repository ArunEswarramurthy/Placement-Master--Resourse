# 🌊 JAVA 8 FEATURES & STREAMS API
### Functional Programming, Lambdas, and `map/filter/reduce` 🚀

---

## 📌 TABLE OF CONTENTS

1. [Why Java 8 Changed Everything](#1-why-java-8-changed-everything)
2. [Functional Interfaces (`@FunctionalInterface`)](#2-functional-interfaces-functionalinterface)
3. [Lambda Expressions (`() -> {}`)](#3-lambda-expressions----)
4. [Method References (`::`)](#4-method-references-)
5. [The Streams API (The Heart of Java 8)](#5-the-streams-api-the-heart-of-java-8)
6. [Intermediate Operations (`filter`, `map`, `sorted`)](#6-intermediate-operations-filter-map-sorted)
7. [Terminal Operations (`collect`, `forEach`, `reduce`)](#7-terminal-operations-collect-foreach-reduce)
8. [The `Optional` Class (Killing NullPointerException)](#8-the-optional-class-killing-nullpointerexception)

---

## 1. Why Java 8 Changed Everything

Before Java 8 (2014), Java was strictly 100% Object-Oriented. If you wanted to run a tiny function, you HAD to create an entire class or a clunky "Anonymous Inner Class".

Java 8 introduced **Functional Programming** concepts. You can now pass *behavior* (methods/functions) as arguments to other methods, without needing to wrap them in objects!

---

## 2. Functional Interfaces (`@FunctionalInterface`)

A Functional Interface is an interface that contains **EXACTLY one abstract method.**
(It can have multiple `default` or `static` methods, but only ONE abstract method).

```java
// 1. Mark it so the compiler enforces the 1-method rule!
@FunctionalInterface 
interface MathOperation {
    int operate(int a, int b); // Only 1 abstract method allowed!
}

// Built-in Java 8 Functional Interfaces (In java.util.function):
// 1. Predicate<T> (Takes T, returns boolean)
// 2. Consumer<T>  (Takes T, returns nothing / void)
// 3. Supplier<T>  (Takes nothing, returns T)
// 4. Function<T,R>(Takes T, returns R)
```

---

## 3. Lambda Expressions (`() -> {}`)

Lambdas are short blocks of code which take in parameters and return a value.
They are used to INSTANTLY implement a Functional Interface.

```java
// OLD WAY (Java 7 - Anonymous Inner Class)
MathOperation additionObj = new MathOperation() {
    @Override
    public int operate(int a, int b) {
        return a + b;
    }
};

// NEW WAY (Java 8 Lambda Expression)
MathOperation additionLambda = (a, b) -> a + b; 
MathOperation multiplyLambda = (a, b) -> a * b;

public class Main {
    public static void main(String[] args) {
        // Look how clean this is!
        System.out.println(additionLambda.operate(5, 3)); // 8
        System.out.println(multiplyLambda.operate(5, 3)); // 15
    }
}
```

---

## 4. Method References (`::`)

Sometimes a Lambda just calls an existing method. You can shorten it further using `::`.

```java
List<String> names = Arrays.asList("Arjun", "Ram", "Sita");

// Lambda Way:
names.forEach(name -> System.out.println(name));

// Method Reference Way: (Class::methodName)
names.forEach(System.out::println); 
```

---

## 5. The Streams API (The Heart of Java 8)

A **Stream** is a sequence of elements from a data source (List, Set, Array) that supports aggregate operations.
**Rules of Streams:**
1.  **They do not change the original list!** They just process data and return a *new* list or value.
2.  They only run once! If you consume a stream, it is closed forever.

```java
List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 9);

// Create a stream to process the collection:
Stream<Integer> stream = numbers.stream();
```

---

## 6. Intermediate Operations (The Factory Line)

These operations process the stream and return **another Stream**, allowing you to chain them together.

1.  **`filter(Predicate)`:** Keeps only elements that return `true`.
2.  **`map(Function)`:** Transforms every element into something else.
3.  **`sorted()`:** Sorts the elements.
4.  **`distinct()`:** Removes duplicates.

*Example problem: Find all even numbers, multiply them by 10, and sort them.*

```java
List<Integer> numList = Arrays.asList(4, 1, 6, 2, 8, 4);

// This does nothing yet! (Intermediate operations are "Lazy")
Stream<Integer> pipeline = numList.stream()
    .filter(n -> n % 2 == 0) // Keeps: 4, 6, 2, 8, 4
    .map(n -> n * 10)        // Becomes: 40, 60, 20, 80, 40
    .distinct()              // Becomes: 40, 60, 20, 80
    .sorted();               // Becomes: 20, 40, 60, 80
```

---

## 7. Terminal Operations (The Output)

These operations finish the stream process and output a final result (a List, an integer, or just printing).
**Streams will not execute AT ALL until a Terminal Operation is called!**

1.  **`collect(Collectors.toList())`:** Packs the stream back into a physical List.
2.  **`forEach(Consumer)`:** Loops through and does something (like printing).
3.  **`reduce()`:** Shrinks the entire stream into a single value (like sum).
4.  **`count()`:** Returns the total number of elements passing the filters.

```java
import java.util.List;
import java.util.Arrays;
import java.util.stream.Collectors;

public class StreamMagic {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("apple", "bat", "cat", "dog", "elephant");

        // Goal: Get all words with > 3 letters, convert to UPPERCASE, save to new list!
        List<String> bigWords = words.stream()
            .filter(w -> w.length() > 3)
            .map(w -> w.toUpperCase())
            .collect(Collectors.toList()); // Terminal! Executes the whole chain.

        System.out.println(bigWords); // [APPLE, ELEPHANT]

        // Goal: Calculate sum of an Integer List
        List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);
        int sum = nums.stream()
            .reduce(0, (a, b) -> a + b); // Starts at 0, adds each 'b' to 'a'
            
        System.out.println("Total Sum: " + sum); // 15
    }
}
```

---

## 8. The `Optional` Class (Killing NullPointerException)

Before Java 8, if a method couldn't find a user in a database, it returned `null`. Calling `.getName()` on that null crashed the app with `NullPointerException`.
**`Optional<T>`** is a wrapper box that may or may not contain an object. It forces the programmer to handle the empty case safely.

```java
import java.util.Optional;

public class OptionalExample {
    
    // Returns a safe Box instead of returning String/null
    static Optional<String> searchDatabase(int id) {
        if (id == 1) return Optional.of("Arjun");
        else return Optional.empty(); // Safely empty!
    }

    public static void main(String[] args) {
        Optional<String> result = searchDatabase(5); // Not found!
        
        // 1. The Safe Check
        if (result.isPresent()) {
            System.out.println("Name: " + result.get());
        } else {
            System.out.println("User not found!");
        }

        // 2. The Java 8 Pro Way (One-liner alternative to IF/ELSE)
        String finalName = result.orElse("Guest User");
        System.out.println("Name: " + finalName); // Outputs: "Guest User"
    }
}
```

---
*Java Core Mastery | Java 8 Features & Streams | Prepared for TCS NQT & Technical Interviews*
