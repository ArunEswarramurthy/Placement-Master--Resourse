# 📚 06. Library Management System
### Rack Allocation, Due Dates & Fine Calculation 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Library Management System.
**Rules:**
1.  **Books & Copies:** A book (e.g., "Harry Potter") can have multiple physical copies. Each copy is assigned a unique tracking ID.
2.  **Racks:** The library has multiple Racks (e.g., 5 racks). Each rack holds a specific set of books.
3.  **Borrowing Rules:** 
    *   A user can borrow a max of **3 books** at a time.
    *   The standard borrow period is **7 days**.
4.  **Returning & Fines:** 
    *   If a book is returned late, calculate a fine of **Rs. 10 per day**.
5.  **Search:** Users can search for books by Title or Author to find exactly which Rack the book is physically sitting on.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Book` Class**: Stores details of the book (Title, Author) and its physical copies (`List<String> copyIds`).
2.  **`User` Class**: Stores the user's details, books borrowed, and total accumulated fines.
3.  **`LibraryManager` Class**: The active engine processing borrowing, returning, searching, and Date calculations.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO: BOOK & COPY
// ==========================================
class Book {
    String bookId; // Generic ID for the Book Title
    String title;
    String author;
    int totalPhysicalCopies;
    int availableCopies;
    String rackLocation; 

    // Holds specific physical tracking barcodes (e.g., "HP-01", "HP-02")
    List<String> physicalCopyIds; 

    public Book(String id, String title, String author, int totalCopies, String rack) {
        this.bookId = id;
        this.title = title;
        this.author = author;
        this.totalPhysicalCopies = totalCopies;
        this.availableCopies = totalCopies;
        this.rackLocation = rack;
        
        // Generate physical barcodes
        physicalCopyIds = new ArrayList<>();
        for (int i = 1; i <= totalCopies; i++) {
            physicalCopyIds.add(id + "-" + i);
        }
    }
}

// ==========================================
// 2. POJO: USER (BORROWER)
// ==========================================
class User {
    int userId;
    String name;
    
    // Tracks the exact physical barcode borrowed and the Day it was borrowed
    // Map<PhysicalCopyId, BorrowDay>
    Map<String, Integer> borrowedBooks; 
    int totalFines;

    public User(int id, String name) {
        this.userId = id;
        this.name = name;
        this.borrowedBooks = new HashMap<>();
        this.totalFines = 0;
    }
}

// ==========================================
// 3. THE CORE LOGIC ENGINE (LIBRARY MANAGER)
// ==========================================
class LibraryManager {

    Map<String, Book> bookCatalog; // BookID -> Book
    Map<Integer, User> userDatabase; // UserID -> User

    public LibraryManager() {
        bookCatalog = new HashMap<>();
        userDatabase = new HashMap<>();

        // Admin Pre-loading Data
        bookCatalog.put("B1", new Book("B1", "Harry Potter", "J.K. Rowling", 5, "Rack-A"));
        bookCatalog.put("B2", new Book("B2", "Lord of the Rings", "Tolkien", 2, "Rack-B"));
        bookCatalog.put("B3", new Book("B3", "Java Basics", "Oracle", 1, "Rack-C"));

        userDatabase.put(101, new User(101, "Arun"));
        userDatabase.put(102, new User(102, "Sita"));
    }

    // --- SEARCH LOGIC ---
    public void searchBook(String query) {
        System.out.println("🔍 Search Results for '" + query + "':");
        boolean found = false;
        for (Book b : bookCatalog.values()) {
            if (b.title.toLowerCase().contains(query.toLowerCase()) || 
                b.author.toLowerCase().contains(query.toLowerCase())) {
                System.out.println("   -> Title: " + b.title + " | Author: " + b.author);
                System.out.println("      Location: " + b.rackLocation + " | Available Copies: " + b.availableCopies);
                found = true;
            }
        }
        if (!found) System.out.println("   (No books found)");
    }

    // --- BORROW LOGIC ---
    public void borrowBook(int userId, String bookId, int currentDay) {
        if (!userDatabase.containsKey(userId)) { System.out.println("❌ Invalid User."); return; }
        if (!bookCatalog.containsKey(bookId)) { System.out.println("❌ Invalid Book ID."); return; }

        User u = userDatabase.get(userId);
        Book b = bookCatalog.get(bookId);

        // Security Checks
        if (u.borrowedBooks.size() >= 3) {
            System.out.println("❌ " + u.name + " has already borrowed 3 books. Return one first!");
            return;
        }
        if (b.availableCopies <= 0) {
            System.out.println("❌ '" + b.title + "' is currently Out of Stock.");
            return;
        }
        if (u.totalFines > 0) {
            System.out.println("❌ Unpaid fines of Rs. " + u.totalFines + ". Please pay before borrowing.");
            return;
        }

        // Get the specific physical copy to give the user
        String specificCopyId = b.physicalCopyIds.remove(0); 
        b.availableCopies--;

        // Issue it to user
        u.borrowedBooks.put(specificCopyId, currentDay);
        
        System.out.println("✅ TICKET ISSUED. " + u.name + " borrowed '" + b.title + "' (Copy: " + specificCopyId + ")");
        System.out.println("   Must be returned by Day " + (currentDay + 7));
    }

    // --- RETURN LOGIC ---
    public void returnBook(int userId, String specificCopyId, int returnDay) {
         if (!userDatabase.containsKey(userId)) { System.out.println("❌ Invalid User."); return; }
         User u = userDatabase.get(userId);

         if (!u.borrowedBooks.containsKey(specificCopyId)) {
             System.out.println("❌ This user did not borrow Copy ID: " + specificCopyId);
             return;
         }

         // Calculate Fines
         int borrowDay = u.borrowedBooks.get(specificCopyId);
         int daysKept = returnDay - borrowDay;
         
         if (daysKept > 7) {
             int lateDays = daysKept - 7;
             int fine = lateDays * 10;
             u.totalFines += fine;
             System.out.println("⚠️ LATE RETURN: " + lateDays + " days late. Fine added: Rs. " + fine);
         }

         // Remove from user
         u.borrowedBooks.remove(specificCopyId);

         // Restore to Library Catalog
         // "B1-02" -> split by "-" -> "B1" is the BookID
         String parentBookId = specificCopyId.split("-")[0];
         Book b = bookCatalog.get(parentBookId);
         
         b.physicalCopyIds.add(specificCopyId);
         b.availableCopies++;

         System.out.println("✅ Book Returned Successfully.");
         if (u.totalFines > 0) System.out.println("   Please pay pending fines of Rs. " + u.totalFines);
    }
    
    // --- PAY FINE ---
    public void payFine(int userId, int amount) {
        User u = userDatabase.get(userId);
        if(u == null) return;
        
        if (amount >= u.totalFines) {
            int change = amount - u.totalFines;
            u.totalFines = 0;
            System.out.println("✅ Fine Paid! Return Change: Rs. " + change);
        } else {
            u.totalFines -= amount;
            System.out.println("✅ Partial Payment. Pending Fines: Rs. " + u.totalFines);
        }
    }
}

// ==========================================
// 4. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        LibraryManager lib = new LibraryManager();

        while (true) {
            System.out.println("\n=== CITY LIBRARY MANAGER ===");
            System.out.println("1. Search Book");
            System.out.println("2. Borrow Book");
            System.out.println("3. Return Book");
            System.out.println("4. Pay Fine");
            System.out.println("5. Exit");
            System.out.print("Enter choice: ");
            int option = sc.nextInt();
            sc.nextLine(); // Clear scanner buffer

            if (option == 1) {
                System.out.print("Enter Book Title/Author: ");
                String query = sc.nextLine();
                lib.searchBook(query);
            } 
            else if (option == 2) {
                System.out.print("Enter User ID: "); int uId = sc.nextInt();
                System.out.print("Enter Book ID (e.g., B1): "); String bId = sc.next();
                System.out.print("Enter Current Day (Int): "); int day = sc.nextInt();
                lib.borrowBook(uId, bId, day);
            } 
            else if (option == 3) {
                System.out.print("Enter User ID: "); int uId = sc.nextInt();
                System.out.print("Enter Physical Copy ID (e.g., B1-1): "); String cId = sc.next();
                System.out.print("Enter Return Day (Int): "); int day = sc.nextInt();
                lib.returnBook(uId, cId, day);
            } 
            else if(option == 4) {
                 System.out.print("Enter User ID: "); int uId = sc.nextInt();
                 System.out.print("Enter Payment Amount: "); int amt = sc.nextInt();
                 lib.payFine(uId, amt);
            }
            else {
                System.exit(0);
            }
        }
    }
}
```

---
## 💡 HOW IT WORKS (Interview Explanation)
1. **Physical Copy Tracking:** A major mistake candidates make is just keeping an integer `count = 5` for books. In real life, books get damaged or lost. By using a `List<String> physicalCopyIds` (e.g., generating B1-1 to B1-5), the library specifically knows *exactly* which physical barcode is missing when user 101 borrows it. Notice how we use `.remove(0)` to take a copy off the shelf, and `.add()` to put it back!
2. **String Splitting for Relationships:** When a user returns `"B1-02"`, how do we know which master Book Object to update? We use `specificCopyId.split("-")[0]`. It extracts `"B1"`, allowing an instant $O(1)$ HashMap search inside `bookCatalog`!
