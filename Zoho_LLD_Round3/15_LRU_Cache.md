# 💾 15. LRU Cache Implementation
### Least Recently Used Data Eviction Algorithm 🚀

---

## 📌 PROBLEM STATEMENT

Build an LRU (Least Recently Used) Cache System from scratch.
**Rules:**
1.  **Capacity Constraint:** The cache operates with a strictly fixed max size (e.g., 3 items).
2.  **Get (Read):** If a user requests a Key, return its Value. Reading an item makes it the *Most Recently Used*.
3.  **Put (Write):** If a user inserts a Key-Value pair, add it to the cache. 
    *   If the Cache is FULL, you must **EVICT** the *Least Recently Used* item before inserting the new one.
4.  **$O(1)$ Time Requirement:** Both `Get()` and `Put()` operations must run in constant $O(1)$ time complexity without loops (The ultimate FAANG test!).

---

## 🏗️ SYSTEM DESIGN (The Architecture)

To achieve strict $O(1)$ math, you CANNOT loop through arrays or use `LinkedHashMap` (the interviewer will ban it). You must manually build a **Doubly Linked List + HashMap** combination!
1.  **`Node` Class**: A doubly-linked list node holding `key`, `value`, `prev`, and `next`.
2.  **`LRUCache` Class**: Holds a `HashMap<Integer, Node>` for instant $O(1)$ finding, and two dummy nodes (`head` and `tail`) to execute instant $O(1)$ shifting!

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO: DOUBLY LINKED LIST NODE
// ==========================================
class Node {
    int key;
    int value;
    Node prev;
    Node next;

    public Node(int key, int value) {
        this.key = key;
        this.value = value;
    }
}

// ==========================================
// 2. THE CORE LOGIC ENGINE (THE CACHE)
// ==========================================
class LRUCache {

    // Database
    int capacity;
    Map<Integer, Node> cacheMap;
    
    // Boundary Pointers
    Node head; // The Most Recently Used side
    Node tail; // The Least Recently Used side (Eviction zone)

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.cacheMap = new HashMap<>();

        // Create Dummy Head and Tail to prevent NullPointerException checks!
        this.head = new Node(-1, -1);
        this.tail = new Node(-1, -1);
        head.next = tail;
        tail.prev = head;
    }

    // --- DOUBLY STRINGS: ADD NODE TO FRONT (O(1)) ---
    private void insertRightBehindHead(Node node) {
        Node currentFirst = head.next;
        
        // Connect block to head
        head.next = node;
        node.prev = head;

        // Connect block to old first
        node.next = currentFirst;
        currentFirst.prev = node;
    }

    // --- DOUBLY STRINGS: DETACH A NODE (O(1)) ---
    private void removeNode(Node node) {
        Node leftNode = node.prev;
        Node rightNode = node.next;

        // Snip the node out of the middle by tying the left and right together
        leftNode.next = rightNode;
        rightNode.prev = leftNode;
    }

    // --- PUBLIC: GET (READ) ---
    public int get(int key) {
        if (!cacheMap.containsKey(key)) {
            System.out.println("❌ Get(" + key + "): CACHE MISS");
            return -1;
        }

        Node node = cacheMap.get(key);
        
        // Promote it to Most Recently Used!
        removeNode(node);
        insertRightBehindHead(node);

        System.out.println("✅ Get(" + key + ") success. Promoted to Head.");
        return node.value;
    }

    // --- PUBLIC: PUT (WRITE) ---
    public void put(int key, int value) {
        // If it already exists, update the value and promote it!
        if (cacheMap.containsKey(key)) {
            Node existingNode = cacheMap.get(key);
            existingNode.value = value;
            removeNode(existingNode);
            insertRightBehindHead(existingNode);
            System.out.println("✅ Put(" + key + "): Updated and Promoted.");
            return;
        }

        // If it's brand new, but we are FULL
        if (cacheMap.size() == capacity) {
            // Who is sitting right next to the tail? The LRU item!
            Node lruNode = tail.prev;
            
            removeNode(lruNode);          // Cut from Linked List
            cacheMap.remove(lruNode.key); // Delete from Hash Map
            System.out.println("⚠️ CACHE FULL! Evicted LRU Key: " + lruNode.key);
        }

        // It's safe to insert now
        Node newNode = new Node(key, value);
        insertRightBehindHead(newNode);
        cacheMap.put(key, newNode);
        System.out.println("✅ Put(" + key + "): Inserted new item.");
    }

    // --- DEBUGGING VIEW ---
    public void printCacheState() {
        System.out.print("CACHE LIST (Recent -> Old): HEAD ");
        Node temp = head.next;
        while (temp != tail) {
            System.out.print("<-> [" + temp.key + ":" + temp.value + "] ");
            temp = temp.next;
        }
        System.out.println("<-> TAIL\n");
    }
}

// ==========================================
// 3. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        // Build a cache that holds exactly 3 items
        LRUCache cache = new LRUCache(3);
        
        System.out.println("--- INITIALIZING LRU CACHE (MAX SIZE: 3) ---");
        
        cache.put(1, 100); 
        cache.printCacheState(); // [1]
        
        cache.put(2, 200); 
        cache.printCacheState(); // [2, 1]
        
        cache.put(3, 300); 
        cache.printCacheState(); // [3, 2, 1] (FULL!)

        // This will EVICT Key 1 because it is at the very tail!
        cache.put(4, 400); 
        cache.printCacheState(); // [4, 3, 2] (1 is gone)

        // Read Key 2. This promotes it from the bottom to the TOP of the chain!
        cache.get(2);
        cache.printCacheState(); // [2, 4, 3]

        // This will now EVICT Key 3, because Key 2 saved itself!
        cache.put(5, 500);
        cache.printCacheState(); // [5, 2, 4]
    }
}
```

---
## 💡 HOW IT WORKS (Interview Explanation)
This exact code structure is how production-grade Redis engines map memory under the hood! 
1. **O(1) Access:** `cacheMap.get(key)` allows the system to instantly find the memory block in RAM.
2. **O(1) Shifting:** Normally in an Array, if you want to push something to the front, you have to shift all other elements by one (an $O(N)$ penalty crash!). In our custom `Doubly Linked List`, we bypass arrays. We just sever the strings binding a node and superglue it directly to the Dummy Head. This physics-based string manipulation executes instantly and uniformly regardless of whether the cache has 3 items or 3 billion items!
