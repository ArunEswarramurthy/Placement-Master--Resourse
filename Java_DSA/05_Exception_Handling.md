# ⚠️ JAVA EXCEPTION HANDLING
### The Complete Guide to `try`, `catch`, `throw`, `throws` & Custom Errors 🚀

---

## 📌 TABLE OF CONTENTS

1. [What is an Exception? (Errors vs Exceptions)](#1-what-is-an-exception-errors-vs-exceptions)
2. [Checked vs Unchecked Exceptions (The Interview Trap!)](#2-checked-vs-unchecked-exceptions-the-interview-trap)
3. [The `try`, `catch`, and `finally` Blocks](#3-the-try-catch-and-finally-blocks)
4. [Multiple Catch Blocks (Order Matters!)](#4-multiple-catch-blocks-order-matters)
5. [The `throw` Keyword (Manually Causing Errors)](#5-the-throw-keyword-manually-causing-errors)
6. [The `throws` Keyword (Passing the Buck)](#6-the-throws-keyword-passing-the-buck)
7. [Creating Custom Exceptions](#7-creating-custom-exceptions)

---

## 1. What is an Exception? (Errors vs Exceptions)

An exception is an unwanted or unexpected event occurring during the execution of a program (at runtime) that disrupts the normal flow of instructions.

**Hierarchy of `Throwable`:**
*   **`java.lang.Error`:** Fatal issues you **cannot** recover from (e.g., `OutOfMemoryError`, `StackOverflowError`). Never try to catch these!
*   **`java.lang.Exception`:** Issues your code **can and should** handle (e.g., `NullPointerException`, `IOException`).

---

## 2. Checked vs Unchecked Exceptions (The Interview Trap!)

You WILL be asked the difference between these two.

| Feature | Checked Exceptions | Unchecked Exceptions (Runtime) |
|---|---|---|
| Checked at Compile Time? | ✅ Yes | ❌ No |
| What must you do? | The compiler forces you to handle them using `try/catch` or `throws`. | The compiler ignores them. It's up to you to write good logic. |
| Examples | `IOException`, `SQLException`, `FileNotFoundException` | `ArithmeticException` (10/0), `NullPointerException`, `ArrayIndexOutOfBoundsException` |
| Parent Class | `Exception` | `RuntimeException` (which inherits from Exception) |

---

## 3. The `try`, `catch`, and `finally` Blocks

*   **`try`**: Defines a block of code to test for errors.
*   **`catch`**: Defines a block of code to execute if an error occurs.
*   **`finally`**: Defines a block of code that **ALWAYS** executes, whether an error occurred or not! Perfect for closing Scanners, Files, or DB connections.

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = 10, b = 0;

        try {
            System.out.println("Trying division...");
            int result = a / b; // Throws ArithmeticException!
            
            // This line NEVER runs because of the exception above.
            System.out.println("Result is: " + result); 
        } 
        catch (ArithmeticException e) {
            System.out.println("ERROR: Cannot divide by zero!");
            // e.printStackTrace(); // Prints exact error & line numbers
        } 
        finally {
            System.out.println("Closing the Scanner (Always runs!).");
            sc.close(); 
        }
    }
}
```

---

## 4. Multiple Catch Blocks (Order Matters!)

You can have multiple `catch` blocks to handle different exceptions gracefully.
**🚨 CRITICAL RULE:** Catch blocks must be ordered from most specific subclass to the most general superclass (`Exception`). 

```java
public class MultiCatch {
    public static void main(String[] args) {
        int[] arr = new int[3];

        try {
            arr[4] = 10 / 0; // Throws ArithmeticException first
        } 
        catch (ArithmeticException e) {
            System.out.println("Math Error: Division by Zero!");
        } 
        catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array Error: Index does not exist!");
        } 
        catch (Exception e) { // The "Catch-All" Parent Exception MUST be last!
            System.out.println("Generic Error: Something else went wrong.");
        }
    }
}
```

---

## 5. The `throw` Keyword (Manually Causing Errors)

Sometimes you want to intentionally crash your program or force an error based on your own business logic.

*   `throw` is used to **explicitly throw a single exception** from within a method.

```java
public class ThrowExample {
    
    static void checkAge(int age) {
        if (age < 18) {
            // We manually stop the program by throwing a new exception
            throw new IllegalArgumentException("Access Denied - You must be at least 18.");
        } 
        else {
            System.out.println("Access Granted!");
        }
    }

    public static void main(String[] args) {
        checkAge(15); // This crashes the program with our custom message!
    }
}
```

---

## 6. The `throws` Keyword (Passing the Buck)

If a method contains a **Checked Exception** (e.g., `Thread.sleep()` which throws `InterruptedException`), you can either `try/catch` it immediately... OR you can "pass the buck" up to whoever called your method.

*   `throws` is written in the **method signature**.
*   It tells the JVM: "This method might throw an error. Whoever calls this method has to deal with it."

```java
import java.io.File;
import java.io.IOException;

public class ThrowsExample {

    // "throws IOException" forces the caller (main) to handle the error
    static void openFile() throws IOException {
        File file = new File("not_found.txt");
        file.createNewFile(); // Checked logic that throws IOException
    }

    public static void main(String[] args) {
        // Since main() called openFile(), main() MUST try/catch it!
        try {
            openFile(); 
        } 
        catch (IOException e) {
            System.out.println("File could not be opened!");
            e.printStackTrace();
        }
    }
}
```
> **Cheat Code:** `throw` is used inside the body to literally *do the throwing*. `throws` is used in the signature to *warn* others.

---

## 7. Creating Custom Exceptions

Built-in exceptions don't cover everything. What if a user's bank balance is too low? We can create an `InsufficientFundsException`!

To do this, create a class that inherits from `Exception` (for Checked) or `RuntimeException` (for Unchecked), and call the parent constructor using `super()`.

```java
// 1. Define the Custom Exception
class InsufficientFundsException extends Exception { // Checked Exception!
    public InsufficientFundsException(String message) {
        super(message); // Pass the message to the parent Exception class
    }
}

public class Bank {
    // 2. Warn users this method throws our custom error
    static void withdraw(double balance, double amount) throws InsufficientFundsException {
        if (amount > balance) {
            // 3. Throw the custom error!
            throw new InsufficientFundsException("Error: balance is only $" + balance);
        } else {
            System.out.println("Withdrawal successful! Remaining: $" + (balance - amount));
        }
    }

    public static void main(String[] args) {
        // 4. Handle the custom error!
        try {
            withdraw(100.0, 500.0);
        } catch (InsufficientFundsException e) {
            System.out.println(e.getMessage()); // Prints our custom message
        }
    }
}
```

---

## 🚨 Final Checklist For Java Exceptions!
1. Never put the parent `catch (Exception e)` ABOVE specific exceptions in a multi-catch block.
2. The `finally` block runs NO MATTER WHAT (except `System.exit(0)`).
3. **`throw`** manually executes an error. **`throws`** warns the method caller they must handle a checked error.
4. **Checked** = Compile-time forced handling. **Unchecked** = Runtime errors (Bugs in your code like division by 0).

---
*Java Core Mastery | Exception Handling | Prepared for TCS NQT & Technical Interviews*
