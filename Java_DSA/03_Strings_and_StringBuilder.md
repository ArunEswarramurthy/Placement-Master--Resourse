\# 🧵 JAVA STRINGS & STRINGBUILDER
### Conquering the String Pool, Immutability & RegEx 🚀

---

## 📌 TABLE OF CONTENTS

1. [The String Immutability Rule (Constant Pool)](#1-the-string-immutability-rule-constant-pool)
2. [String Initialization (`"xyz"` vs `new String()`)](#2-string-initialization-xyz-vs-new-string)
3. [Crucial Issue: `==` versus `.equals()`](#3-crucial-issue--versus-equals)
4. [Mastering String Methods (`length`, `charAt`, `substring`)](#4-mastering-string-methods-length-charat-substring)
5. `StringBuilder`: The Solution to Slow Strings](#5-stringbuilder-the-solution-to-slow-strings)
6. [Character Class Utilities (`Character.isDigit`)](#6-character-class-utilities-characterisdigit)
7. [Splitting Strings & Regular Expressions (`split`)](#7-splitting-strings--regular-expressions-split)

---

## 1. The String Immutability Rule (Constant Pool)

**CRITICAL CONCEPT:** In Java, Strings are **Immutable** (they cannot be changed once created).
When you change a String, Java actually creates a brand-new String in memory and points your variable to the new one! The old one sits in memory until Garbage Collected.

```java
String s = "Hello";
s.concat(" World");     // Modifies the newly created "Hello World" object, but 's' stays "Hello"!
s = s.concat(" World"); // Now 's' points to the new object!
```

To save memory, Java stores all literal Strings in a special memory area called the **String Constant Pool**. If two variables have the exact same literal, they point to the exact same RAM spot!

---

## 2. String Initialization (`"xyz"` vs `new String()`)

```java
// Method 1: Using Literal (Goes into String Pool - FAST & MEMORY EFFICIENT)
String s1 = "Hello";
String s2 = "Hello"; // s2 simply points to s1's location in the Pool!

// Method 2: Using 'new' Keyword (Creates a BRAND NEW object in Heap Memory!)
String s3 = new String("Hello");
String s4 = new String("Hello");
```

---

## 3. Crucial Issue: `==` versus `.equals()`

**Always use `.equals()` to compare Strings in Java!**
*   `==` checks if both variables point to the **exact same memory location (Address)**.
*   `.equals()` checks if the **text content** inside is exactly the same.

```java
public class StringComp {
    public static void main(String[] args) {
        String s1 = "Hello";
        String s2 = "Hello";
        String s3 = new String("Hello");

        // Literal vs Literal (Same memory in Pool)
        System.out.println(s1 == s2);      // true

        // Literal vs Object (Different memory addresses!)
        System.out.println(s1 == s3);      // false

        // Comparing actual text contents
        System.out.println(s1.equals(s3)); // true! (ALWAYS USE THIS)

        // Ignore Case Comparison
        System.out.println(s1.equalsIgnoreCase("hello")); // true
    }
}
```

---

## 4. Mastering String Methods (`length`, `charAt`, `substring`)

Unlike C++, String is a massive class in Java with dozens of built-in powerful methods.

### The Cheatsheet:
```java
String str = "Hello World";

// 1. Length (NOTE THE PARENTHESES! Array has none, String does!)
int len = str.length();       // 11

// 2. Char At Index (Replacing C++ str[i])
char ch = str.charAt(0);      // 'H'

// 3. Substring
// .substring(start_index(inclusive), end_index(exclusive))
String sub1 = str.substring(0, 5); // "Hello"
String sub2 = str.substring(6);    // "World" (From index 6 to end)

// 4. Searching for Index
int idx1 = str.indexOf("World");   // 6 (Starts at index 6)
int idx2 = str.indexOf('l');       // 2 (First 'l')
int idx3 = str.lastIndexOf('l');   // 9 (Last 'l' in "World")

// 5. Changing Case
String upper = str.toUpperCase();  // "HELLO WORLD"
String lower = str.toLowerCase();  // "hello world"

// 6. Replacing Chars / Substrings
String replaced = str.replace('o', 'a');       // "Hella Warld"
String repText = str.replaceAll("Hello", "Hi");// "Hi World"

// 7. Contains, StartsWith, EndsWith (Returns Boolean)
boolean hasWorld = str.contains("World"); // true
boolean startsH = str.startsWith("He");   // true
boolean endsD = str.endsWith("ld");       // true

// 8. Trim (Removes Leading & Trailing Spaces)
String blank = "   Java!   ";
System.out.println(blank.trim()); // "Java!"
```

---

## 5. `StringBuilder`: The Solution to Slow Strings

Because Strings are Immutable, doing this in a loop is incredibly slow (O(N²) time due to constant memory copying):
```java
String s = "";
for(int i=0; i<10000; i++) s += i; // AVOID DOING THIS! Very slow!
```

**The Solution:** Use `StringBuilder`! It acts as a mutable (changeable) string that modifies the actual character array internally.

```java
StringBuilder sb = new StringBuilder(); // Default capacity is 16

// 1. Append (Add to the end) O(1) time
sb.append("TCS");
sb.append(" NQT"); // "TCS NQT"

// 2. Insert (Add in the middle)
sb.insert(4, "Ninja "); // "TCS Ninja NQT"

// 3. Replace
sb.replace(4, 9, "Digital"); // "TCS Digital NQT"

// 4. Delete
sb.delete(4, 12); // "TCS NQT"

// 5. Reverse (Built-in!)
sb.reverse(); // "TQN SCT"
sb.reverse(); // Back to "TCS NQT"

// 6. Convert back to String
String finalResult = sb.toString();
```
> 💡 **Golden Rule:** If you manipulate text inside a loop, ALWAYS use `StringBuilder`.

---

## 6. Character Class Utilities (`Character.isDigit`)

When iterating over Strings character by character, the `Character` wrapper class gives you everything you need.

```java
String text = "aB3!";

for (int i = 0; i < text.length(); i++) {
    char c = text.charAt(i);

    Character.isLetter(c);      // true for 'a', 'B'
    Character.isDigit(c);       // true for '3'
    Character.isLetterOrDigit(c); // true for 'a', 'B', '3'

    Character.isLowerCase(c);   // true for 'a'
    Character.isUpperCase(c);   // true for 'B'

    Character.toLowerCase('A'); // Converts 'A' to 'a'
    Character.toUpperCase('b'); // Converts 'b' to 'B'
}
```

---

## 7. Splitting Strings & Regular Expressions (`split`)

The `.split(regex)` method breaks a string into a `String[]` array around matches of the regular expression.

```java
public class SplitExample {
    public static void main(String[] args) {
        String sentence = "Java is very cool";

        // Split by exactly one space
        String[] words = sentence.split(" ");
        // words = ["Java", "is", "very", "cool"]

        // Splitting a CSV row (Comma Separated)
        String csv = "Arjun,22,Engineer";
        String[] data = csv.split(",");
        // data = ["Arjun", "22", "Engineer"]

        // POWERFUL: Split by one OR MORE spaces (Regex "\\s+")
        String badSpaces = "Hello    World   Java";
        String[] cleanWords = badSpaces.split("\\s+");
        // cleanWords = ["Hello", "World", "Java"]
    }
}
```

---

## 🚨 Final Checklist For Java Strings!
1. Do **NOT** use `==` for String comparison. Use **`.equals()`**!
2. Call `.length()` with parentheses for Strings. Wait, Arrays use `.length` (No parentheses).
3. Do not loop string concatenation `s += "x"`. Loop **`sb.append("x")`** using `StringBuilder`.
4. Use `.substring(start, end)` to fetch parts of a String. `charAt(i)` for single characters.

---
*Core Java Mastery | Part 3: Strings & StringBuilder | Prepared for TCS NQT & Technical Interviews*
