# 🍫 13. Vending Machine Simulator
### The State Design Pattern & Coin Counters 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Vending Machine.
**Rules:**
1.  **Inventory:** The machine holds a Map of Items (`Item Code -> Price & Stock`).
2.  **State Machine:** A real vending machine operates strictly in stages:
    *   *IDLE State:* Waiting for a user to insert money.
    *   *MONEY_INSERTED State:* Holding the user's cash, waiting for them to punch an Item Code.
    *   *DISPENSING State:* Calculating change and physically dropping the item.
3.  **Coin/Note Acceptance:** The machine only accepts valid coins/notes (Rs. 10, 20, 50, 100).
4.  **Transaction Failure:** If the user presses "Cancel" or picks an item they cannot afford, refund ALL inserted physical cash.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Item` Class**: Product properties.
2.  **`VendingState` (Enum)**: `IDLE, CASH_INSERTED, DISPENSING`.
3.  **`VendingMachine` Class**: Holds `Map<String, Item> internalInventory`, the current `VendingState`, and a running counter of `insertedCash`.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO & ENUMS
// ==========================================
enum VendingState {
    IDLE,
    CASH_INSERTED,
    DISPENSING
}

class Item {
    String name;
    int price;
    int currentStock;

    public Item(String name, int price, int currentStock) {
        this.name = name;
        this.price = price;
        this.currentStock = currentStock;
    }
}

// ==========================================
// 2. THE CORE LOGIC ENGINE (THE MACHINE)
// ==========================================
class VendingMachine {
    Map<String, Item> inventory;
    VendingState currentState;
    int insertedCashBuffer;

    public VendingMachine() {
        inventory = new HashMap<>();
        currentState = VendingState.IDLE;
        insertedCashBuffer = 0;

        // Stocking the physical machine shelves
        inventory.put("A1", new Item("Lays Classic", 20, 5));
        inventory.put("A2", new Item("Kurkure", 10, 2));
        inventory.put("B1", new Item("Coke Can", 40, 3));
        inventory.put("B2", new Item("Dairy Milk", 50, 0)); // Out of stock target!
    }

    public void displayProducts() {
        System.out.println("\n--- 🍫 VENDING MACHINE ---");
        for (Map.Entry<String, Item> shelf : inventory.entrySet()) {
            Item i = shelf.getValue();
            System.out.println("[" + shelf.getKey() + "] " + i.name + " | Rs. " + i.price + " | Qty: " + i.currentStock);
        }
        System.out.println("--------------------------");
    }

    // --- STEP 1: INSERT CASH ---
    public void insertCash(int noteVal) {
        // Validation check for accepted currency types
        if (noteVal != 10 && noteVal != 20 && noteVal != 50 && noteVal != 100) {
             System.out.println("❌ Machine only accepts Rs 10, 20, 50, or 100 notes.");
             return;
        }

        insertedCashBuffer += noteVal;
        
        // State transition!
        if (currentState == VendingState.IDLE) {
            currentState = VendingState.CASH_INSERTED;
        }

        System.out.println("💳 Accepted Rs. " + noteVal + ". Total inserted: Rs. " + insertedCashBuffer);
    }

    // --- STEP 2: SELECT PRODUCT & DISPENSE ---
    public void selectProduct(String code) {
        if (currentState == VendingState.IDLE) {
            System.out.println("❌ Error: Insert cash first!");
            return;
        }

        if (!inventory.containsKey(code)) {
            System.out.println("❌ Invalid Code! Does not exist on keypad.");
            return;
        }

        Item selectedItem = inventory.get(code);

        // Validation Checks
        if (selectedItem.currentStock <= 0) {
            System.out.println("❌ OUT OF STOCK! Refunding your Rs. " + insertedCashBuffer);
            resetMachine();
            return;
        }

        if (insertedCashBuffer < selectedItem.price) {
            System.out.println("❌ INSUFFICIENT FUNDS. " + selectedItem.name + " costs Rs. " + selectedItem.price);
            System.out.println("   You only inserted Rs. " + insertedCashBuffer);
            return; // Wait for them to insert more cash or cancel!
        }

        // --- Execute Dispension ---
        currentState = VendingState.DISPENSING;

        int changeDue = insertedCashBuffer - selectedItem.price;
        selectedItem.currentStock--; // Permanently remove from machine shelf

        System.out.println("\n✅ DISPENSING... *CLUNK*");
        System.out.println("🍫 Please collect your '" + selectedItem.name + "' from the tray!");

        if (changeDue > 0) {
            System.out.println("💰 Returning change: Rs. " + changeDue);
        }

        // Transaction Complete. Wipe memory buffer!
        resetMachine();
    }

    // --- STEP 3: USER PRESSES CANCEL ---
    public void cancelTransaction() {
        if (currentState == VendingState.IDLE) {
             System.out.println("❌ Nothing to cancel.");
             return;
        }
        
        System.out.println("🛑 TRANSACTION CANCELLED. Refunding Rs. " + insertedCashBuffer);
        resetMachine();
    }

    // Utility: Return physical cash back to the user and lock machine
    private void resetMachine() {
        insertedCashBuffer = 0;
        currentState = VendingState.IDLE;
    }
}

// ==========================================
// 3. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        VendingMachine vm = new VendingMachine();

        while (true) {
            System.out.println("\n[Machine State: " + vm.currentState + " | Inserted: Rs. " + vm.insertedCashBuffer + "]");
            System.out.println("1. View Shelf");
            System.out.println("2. Insert Cash (Rs 10, 20, 50, 100)");
            System.out.println("3. Type Item Code (e.g., A1, B2)");
            System.out.println("4. Press 'Cancel' Button");
            System.out.println("5. Walk away (Exit Simulation)");
            System.out.print("Action: ");
            int option = sc.nextInt();
            sc.nextLine();

            if (option == 1) {
                vm.displayProducts();
            } 
            else if (option == 2) {
                System.out.print("Insert Note Value: "); int note = sc.nextInt();
                vm.insertCash(note);
            } 
            else if (option == 3) {
                 System.out.print("Keypad Input: ");
                 String code = sc.nextLine().toUpperCase();
                 vm.selectProduct(code);
            }
            else if (option == 4) {
                 vm.cancelTransaction();
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
1. **The State Design Pattern:** A normal IF-block logic engine falls apart quickly because you cannot predict if a user is going to type the product code first, or push coins in first. The `VendingState` enum completely prevents these crashes. If the user presses "A1", but `currentState == IDLE`, the system refuses to run the block! You MUST put coins in to flip the variable to `CASH_INSERTED`.
2. **Buffer Isolation:** At checkout on Amazon, your Credit Card gets charged only at the end. In an ATM or Vending Machine, physical cash goes in to a `buffer` mid-transaction. If a user inserts Rs 50, but selects an empty shelf, `resetMachine()` immediately wipes the `buffer` to 0 and spits the money back out to prevent them from spending that buffer on a second product!
