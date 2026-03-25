# 🛒 09. Amazon E-Commerce System
### Inventory Lock Validation, Carts, and Admin Restocking 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for an E-Commerce platform like Amazon.
**Rules:**
1.  **Admin Role:** 
    *   Can add new Products (ID, Name, Price, Stock Quantity).
    *   Can update the stock of existing products.
2.  **User Role:**
    *   Can view all available products.
    *   Can add items to their `Cart`. 
    *   *Constraint:* You cannot add more quantity to the cart than is currently available in the Admin's stock!
3.  **Checkout Logic:** 
    *   When the user checks out, calculate the total bill.
    *   PERMANENTLY deduct the purchased quantites from the Global Admin Stock.
4.  **Order History:** Users can view their past orders.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Product` Class**: The POJO holding product details.
2.  **`User` Class**: Holds their Wallet Balance (optional checkout limit) and an instance of `Map<Integer, Integer> cart` (ProductID -> Quantity selected).
3.  **`Order` Class**: A historical record of exactly what was bought and when.
4.  **`AmazonManager` Class**: The global engine controlling `GlobalInventory` vs `LocalCarts`.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO: PRODUCT & ORDER HISTORY
// ==========================================
class Product {
    int productId;
    String name;
    double price;
    int stockAvailable;

    public Product(int productId, String name, double price, int stockAvailable) {
        this.productId = productId;
        this.name = name;
        this.price = price;
        this.stockAvailable = stockAvailable;
    }
}

class Order {
    static int orderIdProvider = 5000;
    
    int orderId;
    double totalAmountPaid;
    // Snapshot of what they bought (ProductID -> Quantity)
    Map<Integer, Integer> itemsBought; 

    public Order(double amountPaid, Map<Integer, Integer> cartSnapshot) {
        this.orderId = orderIdProvider++;
        this.totalAmountPaid = amountPaid;
        this.itemsBought = new HashMap<>(cartSnapshot); // Deep Copy!
    }
}

// ==========================================
// 2. POJO: USER (WITH CART)
// ==========================================
class User {
    int userId;
    String name;
    
    // ProductID -> Quantity
    Map<Integer, Integer> cart;
    List<Order> orderHistory;

    public User(int id, String name) {
        this.userId = id;
        this.name = name;
        this.cart = new HashMap<>();
        this.orderHistory = new ArrayList<>();
    }
}

// ==========================================
// 3. THE CORE LOGIC ENGINE (AMAZON MANAGER)
// ==========================================
class AmazonManager {

    Map<Integer, Product> globalInventory;
    Map<Integer, User> userDatabase;

    public AmazonManager() {
        globalInventory = new HashMap<>();
        userDatabase = new HashMap<>();

        // Pre-loaded Database
        userDatabase.put(1, new User(1, "Arun"));
        
        globalInventory.put(101, new Product(101, "Laptop", 50000, 5));
        globalInventory.put(102, new Product(102, "Mouse", 1000, 20));
        globalInventory.put(103, new Product(103, "Keyboard", 2000, 10));
    }

    // --- ADMIN CONTROLS ---
    public void addOrUpdateStock(int productId, String name, double price, int newStockToAdd) {
        if (globalInventory.containsKey(productId)) {
            Product p = globalInventory.get(productId);
            p.stockAvailable += newStockToAdd;
            System.out.println("✅ ADMIN: Restocked " + name + ". Total new stock: " + p.stockAvailable);
        } else {
            globalInventory.put(productId, new Product(productId, name, price, newStockToAdd));
            System.out.println("✅ ADMIN: New Product Added -> " + name);
        }
    }

    public void displayProducts() {
        System.out.println("\n--- 📦 AMAZON CATALOG ---");
        for (Product p : globalInventory.values()) {
            System.out.println(p.productId + " | " + p.name + " | Rs. " + p.price + " | Stock: " + p.stockAvailable);
        }
        System.out.println("-------------------------");
    }

    // --- USER CART LOGIC ---
    public void addToCart(int userId, int productId, int requestedQuantity) {
        User u = userDatabase.get(userId);
        Product p = globalInventory.get(productId);

        if (p == null) {
            System.out.println("❌ Invalid Product ID.");
            return;
        }

        // Validate Inventory
        int currentCartQty = u.cart.getOrDefault(productId, 0);
        int totalAttemptingToBuy = currentCartQty + requestedQuantity;

        if (totalAttemptingToBuy > p.stockAvailable) {
            System.out.println("❌ INVENTORY ERROR: We only have " + p.stockAvailable + " units in stock.");
            System.out.println("   You already have " + currentCartQty + " in your cart.");
            return;
        }

        // Add to map
        u.cart.put(productId, totalAttemptingToBuy);
        System.out.println("✅ Added " + requestedQuantity + "x '" + p.name + "' to cart.");
    }

    public void viewCart(int userId) {
        User u = userDatabase.get(userId);
        System.out.println("\n--- 🛒 YOUR CART ---");
        
        if(u.cart.isEmpty()) { System.out.println("  (Cart is Empty)"); return; }
        
        double subtotal = 0;
        for (Map.Entry<Integer, Integer> entry : u.cart.entrySet()) {
            Product p = globalInventory.get(entry.getKey());
            int qty = entry.getValue();
            double cost = p.price * qty;
            subtotal += cost;
            System.out.println(p.name + " (x" + qty + ") = Rs. " + cost);
        }
        System.out.println("Estimated Total: Rs. " + subtotal);
    }

    // --- CHECKOUT LOGIC ---
    public void checkout(int userId) {
        User u = userDatabase.get(userId);
        
        if (u.cart.isEmpty()) {
            System.out.println("❌ Cart is empty.");
            return;
        }

        // 1. Final Safety Check (Someone else might have bought the item while it sat in our cart!)
        double finalBill = 0;
        for (Map.Entry<Integer, Integer> entry : u.cart.entrySet()) {
            Product p = globalInventory.get(entry.getKey());
            int requestedQty = entry.getValue();

            if (requestedQty > p.stockAvailable) {
                System.out.println("❌ OUT OF STOCK ERROR: '" + p.name + "' sold out while in your cart!");
                return; // Brutal cancellation (Real life Amazon does this too!)
            }
            finalBill += (p.price * requestedQty);
        }

        // 2. Process Order
        System.out.println("\n✅ PAYMENT SUCCESSFUL: Rs. " + finalBill);

        // Deduct physical inventory
        for (Map.Entry<Integer, Integer> entry : u.cart.entrySet()) {
            Product p = globalInventory.get(entry.getKey());
            p.stockAvailable -= entry.getValue();
        }

        // 3. Save Order History & Wipe Cart
        Order newOrder = new Order(finalBill, u.cart);
        u.orderHistory.add(newOrder);
        u.cart.clear(); // Reset Cart

        System.out.println("📦 Order ID #" + newOrder.orderId + " is preparing for dispatch!");
    }
}

// ==========================================
// 4. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        AmazonManager app = new AmazonManager();

        while (true) {
            System.out.println("\n=== AMAZON INC. ===");
            System.out.println("1. View Store");
            System.out.println("2. Add to Cart");
            System.out.println("3. View Cart");
            System.out.println("4. Checkout");
            System.out.println("5. Admin: Restock Item");
            System.out.println("6. Exit");
            System.out.print("Enter choice: ");
            int option = sc.nextInt();

            if (option == 1) {
                app.displayProducts();
            } 
            else if (option == 2) {
                System.out.print("Enter Product ID: "); int pId = sc.nextInt();
                System.out.print("Enter Quantity: "); int qty = sc.nextInt();
                app.addToCart(1, pId, qty); // Default User 1
            } 
            else if (option == 3) {
                app.viewCart(1);
            } 
            else if (option == 4) {
                app.checkout(1);
            } 
            else if (option == 5) {
                System.out.print("Enter Product ID: "); int pId = sc.nextInt();
                System.out.print("Enter Restock Qty: "); int qty = sc.nextInt();
                System.out.print("Enter Generic Name: "); String nm = sc.next();
                app.addOrUpdateStock(pId, nm, 500.0, qty);
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
1. **The Double Validation Logic:** It's absolutely crucial for interviews to double-check inventory. The system checks `if (totalAttemptingToBuy > p.stockAvailable)` during "Add to Cart". **BUT**, it checks the stock *again* during Checkout! Why? Because in a high-concurrency system, two different users can add 5 laptops to their separate carts when only 6 exist globally. The first person to click Checkout gets them, and the second person must be thrown an error!
2. **Deep Copy of Order Maps:** `new HashMap<>(cartSnapshot)`. If you do `this.itemsBought = cartSnapshot;` inside the Order constructor, Java passes the HashMap *by reference*. When you `clear()` the cart one second later, the `OrderHistory` inside the object will instantly get wiped blank! Using `new HashMap<>()` physically clones the data safely into the receipt.
