# 🍔 07. Food Delivery System (Zomato / Swiggy)
### Restaurant Menus, Cart Logic, and Delivery Assignment 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Food Delivery System.
**Rules:**
1.  **Restaurants:** The system has multiple restaurants. Each restaurant has a unique Menu (Item Name -> Price).
2.  **Users:** A user can add items from a single restaurant to their `Cart`. If they try to add an item from a different restaurant, clear the cart.
3.  **Ordering:** When the user checks out, calculate the total bill + a 5% tax + a fixed Delivery Fee of Rs. 40.
4.  **Delivery Excecutives:** There are multiple Delivery Agents. When an order is placed, assign it to a delivery agent who is currently `isAvailable == true`. The agent now becomes unavailable until they complete the order.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Restaurant` Class**: Holds the Restaurant Name and a predefined `Map<String, Integer> menu` (Dish->Price).
2.  **`DeliveryAgent` Class**: Represents the driver. Tracks if they are currently carrying an order.
3.  **`Cart` Class**: Attached to each user. Tracks the `restaurantId` and a `Map<String, Integer>` representing (Dish->Quantity).
4.  **`FoodManager` Class**: The active engine routing the orders and assigning drivers dynamically.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO: RESTAURANT & DRIVER
// ==========================================
class Restaurant {
    int id;
    String name;
    Map<String, Integer> menu; // Dish Name -> Price

    public Restaurant(int id, String name) {
        this.id = id;
        this.name = name;
        this.menu = new HashMap<>();
    }
}

class DeliveryAgent {
    int agentId;
    String name;
    boolean isAvailable;

    public DeliveryAgent(int id, String name) {
        this.agentId = id;
        this.name = name;
        this.isAvailable = true;
    }
}

// ==========================================
// 2. POJO: USER & CART
// ==========================================
class Cart {
    int expectedRestaurantId; // To prevent mixing food from multiple places
    Map<String, Integer> items; // Dish Name -> Quantity

    public Cart() {
        expectedRestaurantId = -1;
        items = new HashMap<>();
    }

    public void clearCart() {
        expectedRestaurantId = -1;
        items.clear();
    }
}

class User {
    int userId;
    String name;
    Cart cart;

    public User(int id, String name) {
        this.userId = id;
        this.name = name;
        this.cart = new Cart();
    }
}

// ==========================================
// 3. THE CORE LOGIC ENGINE (FOOD MANAGER)
// ==========================================
class FoodManager {

    Map<Integer, Restaurant> restaurants;
    Map<Integer, User> users;
    List<DeliveryAgent> agents;

    public FoodManager() {
        restaurants = new HashMap<>();
        users = new HashMap<>();
        agents = new ArrayList<>();

        // Pre-fill Dummy Data
        Restaurant dominos = new Restaurant(1, "Dominos Pizza");
        dominos.menu.put("Margherita", 200);
        dominos.menu.put("Pepperoni", 350);
        
        Restaurant kfc = new Restaurant(2, "KFC");
        kfc.menu.put("Zinger Burger", 180);
        kfc.menu.put("Chicken Wings", 220);

        restaurants.put(1, dominos);
        restaurants.put(2, kfc);

        users.put(101, new User(101, "Arun"));
        
        agents.add(new DeliveryAgent(501, "Ramesh"));
        agents.add(new DeliveryAgent(502, "Suresh"));
    }

    public void displayMenu() {
        System.out.println("--- RESTAURANTS ---");
        for (Restaurant r : restaurants.values()) {
            System.out.println(r.id + ". " + r.name);
            for (Map.Entry<String, Integer> dish : r.menu.entrySet()) {
                System.out.println("   - " + dish.getKey() + " : Rs. " + dish.getValue());
            }
        }
    }

    // --- ADD TO CART LOGIC ---
    public void addToCart(int userId, int restId, String dishName, int quantity) {
        User u = users.get(userId);
        Restaurant r = restaurants.get(restId);

        if (r == null || !r.menu.containsKey(dishName)) {
            System.out.println("❌ Invalid Restaurant or Dish!");
            return;
        }

        Cart c = u.cart;

        // Conflict check: Don't mix restaurants!
        if (c.expectedRestaurantId != -1 && c.expectedRestaurantId != restId) {
            System.out.println("⚠️ Warning: Cart contains items from another restaurant. Cart reset!");
            c.clearCart();
        }

        c.expectedRestaurantId = restId;
        // Add to map, increase quantity if already exists
        c.items.put(dishName, c.items.getOrDefault(dishName, 0) + quantity);

        System.out.println("✅ Added " + quantity + "x " + dishName + " to Cart.");
    }

    // --- CHECKOUT & DRIVER ASSIGNMENT ---
    public void checkout(int userId) {
        User u = users.get(userId);
        Cart c = u.cart;

        if (c.items.isEmpty()) {
            System.out.println("❌ Cart is empty.");
            return;
        }

        // 1. Calculate Food Total
        Restaurant r = restaurants.get(c.expectedRestaurantId);
        int foodTotal = 0;

        System.out.println("\n--- 🧾 INVOICE ---");
        System.out.println("Ordering from: " + r.name);
        for (Map.Entry<String, Integer> entry : c.items.entrySet()) {
            int dishPrice = r.menu.get(entry.getKey());
            int lineTotal = dishPrice * entry.getValue();
            foodTotal += lineTotal;
            System.out.println(entry.getValue() + "x " + entry.getKey() + " = Rs. " + lineTotal);
        }

        // 2. Add Taxes and Fees
        double tax = foodTotal * 0.05; // 5% GST
        int deliveryFee = 40;
        double finalBill = foodTotal + tax + deliveryFee;

        System.out.println("Food Subtotal: Rs. " + foodTotal);
        System.out.println("GST (5%): Rs. " + tax);
        System.out.println("Delivery Fee: Rs. " + deliveryFee);
        System.out.println("💵 FINAL TOTAL: Rs. " + finalBill);

        // 3. Assign Driver (The Uber-lite algorithm)
        DeliveryAgent assignedAgent = null;
        for (DeliveryAgent agent : agents) {
            if (agent.isAvailable) {
                assignedAgent = agent;
                break;
            }
        }

        if (assignedAgent == null) {
            System.out.println("❌ Sorry, all delivery executives are busy. Order failed. Try again.");
            return; // Order fails, cart is preserved for later
        }

        // Lock the driver!
        assignedAgent.isAvailable = false;
        c.clearCart(); // Order successful, empty cart!
        
        System.out.println("🚀 ORDER PLACED! Driver " + assignedAgent.name + " is picking it up.");
    }

    // --- DRIVER COMPLETES ORDER ---
    public void completeDelivery(int agentId) {
        for (DeliveryAgent agent : agents) {
            if (agent.agentId == agentId) {
                agent.isAvailable = true; // Driver is free again!
                System.out.println("✅ Driver " + agent.name + " completed the delivery and is now free!");
                return;
            }
        }
    }
}

// ==========================================
// 4. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        FoodManager app = new FoodManager();

        while (true) {
            System.out.println("\n=== ZOMATO BACKEND ===");
            System.out.println("1. View Restaurants & Menu");
            System.out.println("2. Add to Cart");
            System.out.println("3. Checkout & Order");
            System.out.println("4. Admin: Mark Delivery Complete");
            System.out.println("5. Exit");
            System.out.print("Enter choice: ");
            int option = sc.nextInt();
            sc.nextLine(); // Clear buffer

            if (option == 1) {
                app.displayMenu();
            } 
            else if (option == 2) {
                System.out.print("Enter Restaurant ID: "); int rId = sc.nextInt(); sc.nextLine();
                System.out.print("Enter Exact Dish Name: "); String dish = sc.nextLine();
                System.out.print("Enter Quantity: "); int qty = sc.nextInt();
                app.addToCart(101, rId, dish, qty); // Defaulting to User 101 for demo
            } 
            else if (option == 3) {
                app.checkout(101);
            } 
            else if (option == 4) {
                 System.out.print("Enter Delivery Agent ID (e.g. 501, 502): "); 
                 int aId = sc.nextInt();
                 app.completeDelivery(aId);
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
1. **The Cart State Machine:** The `expectedRestaurantId` acts as a crucial safety lock inside the user's Cart. If a user adds a KFC burger to their cart, `expectedRestaurantId` permanently locks to `2`. If they try to add a Dominos pizza `1`, the IF statement trips, physically wiping the cart HashMap (`items.clear()`) and setting the new lock!
2. **Driver Concurrency Simulation:** An essential part of LLD is locking resources. By checking `agent.isAvailable`, we fetch the first available driver and immediately execute `agent.isAvailable = false;`. If 100 orders come in and we only have 2 drivers, the 3rd order will correctly trigger the "Sorry, all executives are busy" logic!
