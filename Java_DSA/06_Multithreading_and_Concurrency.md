# 🧵 JAVA MULTITHREADING & CONCURRENCY
### Unleashing the Power of the JVM | Master Threads, Sync & Deadlocks 🚀

---

## 📌 TABLE OF CONTENTS

1. [What is Multithreading? (Process vs Thread)](#1-what-is-multithreading-process-vs-thread)
2. [Creating Threads (Thread Class vs Runnable Interface)](#2-creating-threads-thread-class-vs-runnable-interface)
3. [The Thread Lifecycle & Key Methods (`sleep`, `join`)](#3-the-thread-lifecycle--key-methods-sleep-join)
4. [The Sync Problem (Race Conditions)](#4-the-sync-problem-race-conditions)
5. [The Solution: `synchronized` Blocks & Methods](#5-the-solution-synchronized-blocks--methods)
6. [The `volatile` Keyword (Memory Visibility)](#6-the-volatile-keyword-memory-visibility)
7. [Deadlocks (The Nightmare Scenario)](#7-deadlocks-the-nightmare-scenario)
8. [Modern Concurrency: `ExecutorService` & Thread Pools](#8-modern-concurrency-executorservice--thread-pools)

---

## 1. What is Multithreading? (Process vs Thread)

Modern CPUs have multiple cores. Multithreading allows Java to do multiple things at the exact same time.

*   **Process:** A heavyweight program in execution (e.g., Google Chrome, MS Word). Processes DO NOT share memory.
*   **Thread:** A lightweight sub-task inside a process (e.g., One Chrome tab downloading a file, another tab playing music). **Threads share the same memory space!**

---

## 2. Creating Threads (Thread Class vs Runnable Interface)

There are exactly two ways to create a thread in Java.

### Method 1: Extending the `Thread` Class
```java
// 1. Inherit from Thread
class MyThread extends Thread {
    @Override
    public void run() { // 2. Put the job inside run()
        System.out.println("Thread is running!");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        // t1.run(); // WRONG! This runs on the main thread like a normal method.
        t1.start();  // CORRECT! This asks the JVM to branch off a NEW timeline.
    }
}
```

### Method 2: Implementing the `Runnable` Interface (THE BEST WAY!)
Because Java doesn't support multiple inheritance, if you extend `Thread`, you can't extend any other class! `Runnable` fixes this.

```java
// 1. Implement Runnable
class MyTask implements Runnable {
    @Override
    public void run() {
        System.out.println("Runnable task is running!");
    }
}

public class Main {
    public static void main(String[] args) {
        MyTask task = new MyTask();
        
        // 2. Wrap it inside a standard Thread object
        Thread t1 = new Thread(task); 
        t1.start(); // Branch off!
    }
}
```

---

## 3. The Thread Lifecycle & Key Methods (`sleep`, `join`)

A thread goes through states: **New → Runnable → Running → Blocked/Waiting → Terminated**.

### Key Thread Methods:
*   `Thread.sleep(ms)`: Pauses the current thread. Must try/catch `InterruptedException`.
*   `t1.join()`: Forces the *main* thread to WAIT until `t1` completely finishes before moving on.
*   `Thread.currentThread().getName()`: Gets the name of whoever is running the code right now.

```java
public class JoinExample {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> { // Using a Lambda for Runnable!
            for (int i = 1; i <= 3; i++) {
                System.out.println("T1 working...");
                try { Thread.sleep(1000); } catch (Exception e){}
            }
        });

        t1.start();
        
        System.out.println("Main thread is waiting for T1...");
        t1.join(); // Main thread FREEZES here until T1 dies.
        
        System.out.println("T1 finished. Main thread ending.");
    }
}
```

---

## 4. The Sync Problem (Race Conditions)

Threads **share memory**. If two threads try to modify the exact same variable at the exact same millisecond, data gets corrupted! This is a **Race Condition**.

```java
class Counter {
    int count = 0;
    
    // NOT THREAD SAFE! 
    // count++ is secretly 3 steps: 1. Read, 2. Add, 3. Write.
    // Threads will interrupt each other in the middle of these steps!
    public void increment() { 
        count++; 
    }
}

public class RaceCondition {
    public static void main(String[] args) throws Exception {
        Counter c = new Counter();

        Runnable task = () -> { for(int i=0; i<1000; i++) c.increment(); };

        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);

        t1.start(); t2.start();
        t1.join();  t2.join();

        // You expect 2000... But you will get a random number like 1423!
        System.out.println("Final Count: " + c.count); 
    }
}
```

---

## 5. The Solution: `synchronized` Blocks & Methods

To fix Race Conditions, we use **Monitor Locks**. Java allows you to put a lock on a method or a block of code so that **only ONE thread can enter it at a time**.

### Option A: Synchronized Method
```java
class Counter {
    int count = 0;
    
    // The "synchronized" keyword locks the WHOLE method.
    // If T1 goes in, T2 must wait at the door until T1 leaves!
    public synchronized void increment() { 
        count++; 
    }
}
```

### Option B: Synchronized Block (Better Performance)
```java
class Counter {
    int count = 0;
    Object lock = new Object(); // Custom Lock

    public void increment() {
        System.out.println("Any thread can print this.");
        
        // Only ONE thread can enter this locked zone!
        synchronized(lock) { 
            count++; 
        }
    }
}
```

---

## 6. The `volatile` Keyword (Memory Visibility)

Normally, threads optimize speed by keeping local copies of variables in the **CPU Cache** rather than constantly checking the Main RAM.
If T1 changes a variable, T2 might not immediately see the change if it's looking at its own cache!

**`volatile`** forces all threads to completely ignore the CPU cache and read/write the variable directly to **Main RAM** every single time.

```java
class FlagObj {
    // T1 changing this guarantees T2 will instantly see it.
    volatile boolean stopRequested = false; 
}
```
> ⚠️ **Note:** `volatile` ONLY guarantees visibility. It does **NOT** prevent Race Conditions! Use `synchronized` to prevent Race Conditions.

---

## 7. Deadlocks (The Nightmare Scenario)

A Deadlock happens when T1 has Lock A and is waiting for Lock B... while T2 has Lock B and is waiting for Lock A. Both freeze forever!

```java
Object lockA = new Object();
Object lockB = new Object();

Thread t1 = new Thread(() -> {
    synchronized(lockA) {
        System.out.println("T1 holds A... waiting for B");
        synchronized(lockB) { System.out.println("T1 got B"); }
    }
});

Thread t2 = new Thread(() -> {
    synchronized(lockB) {
        System.out.println("T2 holds B... waiting for A");
        synchronized(lockA) { System.out.println("T2 got A"); }
    }
});

// If T1 and T2 run at exactly the same time, the program freezes infinitely!
```
> **How to fix Deadlocks?** Always acquire locks in the exact same order! If T1 and T2 both ask for `lockA` first, the deadlock is impossible.

---

## 8. Modern Concurrency: `ExecutorService` & Thread Pools

Creating a brand new Thread for every tiny task uses massive amounts of OS memory.
The **Thread Pool Worker Pattern** creates a pool of reusable threads (e.g., 5 threads). When a task arrives, a worker grabs it. When finished, the worker returns to the pool for the next task!

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class WebRequest implements Runnable {
    String url;
    WebRequest(String url) { this.url = url; }
    
    public void run() {
        System.out.println(Thread.currentThread().getName() + " fetching " + url);
    }
}

public class ThreadPoolExample {
    public static void main(String[] args) {
        
        // 1. Create a Thread Pool with exactly 3 workers
        ExecutorService pool = Executors.newFixedThreadPool(3);

        // 2. Send 10 tasks. Only 3 tasks run at a time! The rest wait in queue.
        for (int i = 1; i <= 10; i++) {
            pool.execute(new WebRequest("Page " + i));
        }

        // 3. Initiate an orderly shutdown (Finishes queue, accepts no new tasks)
        pool.shutdown(); 
    }
}
```

---

## 🚨 Final Checklist For Java Concurrency!
1. Always map out your **Shared Resources** (variables/objects edited by multiple threads).
2. Never call `t1.run()`. Always call **`t1.start()`** to spawn the new timeline.
3. Use **`synchronized`** or `AtomicInteger` to fix Race Conditions (incorrect math).
4. Use **`volatile`** to fix Visibility Problems (variables not updating for other threads).
5. In enterprise code, NEVER manually `new Thread()`. Always use an **`ExecutorService` ThreadPool**.

---
*Java Core Mastery | Multithreading & Concurrency | Prepared for TCS NQT & Technical Interviews*
