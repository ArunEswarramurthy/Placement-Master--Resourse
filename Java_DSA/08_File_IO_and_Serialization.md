# 📁 JAVA FILE I/O & SERIALIZATION
### Read/Write Files, Byte Streams vs Character Streams & Saving Objects to Disk 🚀

---

## 📌 TABLE OF CONTENTS

1. [Stream Basics (Bytes vs Characters)](#1-stream-basics-bytes-vs-characters)
2. [The `File` Class (Checking if a file exists)](#2-the-file-class-checking-if-a-file-exists)
3. [Writing to a File (`FileWriter`, `BufferedWriter`)](#3-writing-to-a-file-filewriter-bufferedwriter)
4. [Reading from a File (`Scanner`, `BufferedReader`)](#4-reading-from-a-file-scanner-bufferedreader)
5. [The Try-With-Resources Block (No more `.close()`)](#5-the-try-with-resources-block-no-more-close)
6. [Serialization (Saving Objects to Hard Drive)](#6-serialization-saving-objects-to-hard-drive)
7. [Deserialization (Loading Objects from Hard Drive)](#7-deserialization-loading-objects-from-hard-drive)

---

## 1. Stream Basics (Bytes vs Characters)

In Java, an I/O Stream represents an input source or an output destination.

1.  **Byte Streams (8-bit):** Used for reading/writing binary data (Images, Audio, PDF files).
    *   Classes: `FileInputStream`, `FileOutputStream`
2.  **Character Streams (16-bit):** Used for reading/writing plain text (`.txt` files). They automatically handle converting Java's 16-bit Unicode characters to the local character set.
    *   Classes: `FileReader`, `FileWriter`

---

## 2. The `File` Class (Checking if a file exists)

The `java.io.File` class does NOT read or write data. It only shows you metadata about the file (Size, Path, Does it exist?).

```java
import java.io.File;
import java.io.IOException;

public class FileExample {
    public static void main(String[] args) {
        File myFile = new File("test.txt");

        try {
            if (myFile.createNewFile()) { // Creates file if it doesn't exist!
                System.out.println("File created: " + myFile.getName());
            } else {
                System.out.println("File already exists.");
            }
            
            System.out.println("Absolute path: " + myFile.getAbsolutePath());
            System.out.println("File size: " + myFile.length() + " bytes");
            
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
    }
}
```

---

## 3. Writing to a File (`FileWriter`, `BufferedWriter`)

### The Simple Way (`FileWriter`)
Writes character by character to the disk. (Can be slow for massive files).

```java
import java.io.FileWriter;
import java.io.IOException;

public class WriteFile {
    public static void main(String[] args) {
        try {
            // "true" means APPEND MODE. If missing, it OVERWRITES the file completely.
            FileWriter writer = new FileWriter("test.txt", true);
            writer.write("Java is awesome!\n");
            writer.write("Let's master File I/O.\n");
            
            writer.close(); // REQUIRED! Or the text might not actually save.
            System.out.println("Successfully wrote to the file.");
            
        } catch (IOException e) {
            System.out.println("An error occurred.");
        }
    }
}
```

### The Fast Way (`BufferedWriter`)
Writes huge chunks of text to memory (buffer) first, then dumps it to the disk all at once. Much faster!
```java
BufferedWriter bw = new BufferedWriter(new FileWriter("test.txt"));
bw.write("Fast bulk writing!");
bw.close();
```

---

## 4. Reading from a File (`Scanner`, `BufferedReader`)

### Method 1: Using `Scanner` (Easiest)
Best for parsing specific data types (ints, doubles) from a file.
```java
import java.io.File;
import java.util.Scanner;

public class ReadScanner {
    public static void main(String[] args) {
        try {
            File file = new File("test.txt");
            Scanner reader = new Scanner(file);
            
            while (reader.hasNextLine()) { // Loop until end of file
                String line = reader.nextLine();
                System.out.println(line);
            }
            reader.close();
            
        } catch (Exception e) {
            System.out.println("File not found.");
        }
    }
}
```

### Method 2: Using `BufferedReader` (Fastest for Huge Files)
Best for reading millions of lines of pure text.
```java
import java.io.BufferedReader;
import java.io.FileReader;

public class ReadBuffer {
    public static void main(String[] args) {
        try {
            BufferedReader br = new BufferedReader(new FileReader("test.txt"));
            String line;
            
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
            br.close();
            
        } catch (Exception e) {
            System.out.println("Error reading file.");
        }
    }
}
```

---

## 5. The Try-With-Resources Block (No more `.close()`)

**CRITICAL JAVA 7+ FEATURE!**
Normally, if your program crashes while writing a file, `.close()` never runs, and the file gets corrupted or locked.
You used to put `.close()` in a `finally` block. Now, we use **Try-With-Resources**.
It **automatically closes the file** the exact moment the block finishes!

```java
import java.io.FileWriter;
// Put the FileWriter INSIDE the try() parentheses!
public class TryWithResources {
    public static void main(String[] args) {
        
        try (FileWriter writer = new FileWriter("test.txt")) {
            writer.write("This file automatically closes itself!");
            // No need to write writer.close()!
        } catch (Exception e) {
            System.out.println("Error");
        }
    }
}
```

---

## 6. Serialization (Saving Objects to Hard Drive)

**Concept:** What if you want to save a `Player` object (health, level, name) exactly as it is, without splitting it into pieces of text?
**Serialization** converts a Java Object into a raw Byte Stream so it can be saved to an `.ser` or `.dat` file, or sent over a network.

### Step 1: Implement `Serializable`
```java
import java.io.Serializable;

// 1. MUST implement Serializable (It's a "Marker Interface" with 0 methods!)
class Player implements Serializable {
    String name;
    int level;
    
    // "transient" means DO NOT SAVE THIS VALUE! (Used for passwords or temporary data)
    transient String temporaryBuff; 

    public Player(String name, int level) {
        this.name = name;
        this.level = level;
        this.temporaryBuff = "Speed Boost";
    }
}
```

### Step 2: Write Object to File (`ObjectOutputStream`)
```java
import java.io.*;

public class Serializer {
    public static void main(String[] args) {
        Player p1 = new Player("Arjun", 50);

        try (FileOutputStream fileOut = new FileOutputStream("player.ser");
             ObjectOutputStream out = new ObjectOutputStream(fileOut)) {
            
            out.writeObject(p1); // MAGIC! The entire object is saved to disk!
            System.out.println("Player saved successfully.");
            
        } catch (IOException i) {
            i.printStackTrace();
        }
    }
}
```

---

## 7. Deserialization (Loading Objects from Hard Drive)

Now we load the exact `Player` object back into our program from the byte file!

```java
import java.io.*;

public class Deserializer {
    public static void main(String[] args) {
        Player p = null;

        try (FileInputStream fileIn = new FileInputStream("player.ser");
             ObjectInputStream in = new ObjectInputStream(fileIn)) {
            
            p = (Player) in.readObject(); // CAST back to Player!
            
            System.out.println("Loaded Player: " + p.name + " (Level " + p.level + ")");
            // Output for transient variable will be "null" because it wasn't saved!
            System.out.println("Buff: " + p.temporaryBuff); 
            
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 🚨 Final Checklist!
1. Always use **Try-With-Resources** `try(FileWriter f = ...)` to prevent memory leaks!
2. `Scanner` is good for parsing chunks. `BufferedReader` is king for speed with massive files.
3. Classes MUST implement **`Serializable`** to be written to a file as an Object.
4. The **`transient`** keyword prevents highly sensitive data (like passwords) from being saved to the hard drive during serialization.

---
*Java Core Mastery | File I/O & Serialization | Prepared for TCS NQT & Technical Interviews*
