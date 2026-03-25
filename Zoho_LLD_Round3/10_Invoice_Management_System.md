# 🧾 10. Invoice Management System
### Customer Billing, Tax Calculation & Receipt Generation 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for an Invoice / Billing Management System.
**Rules:**
1.  **Customers:** Can be added to the system. Each customer has a unique ID and Name.
2.  **Products:** The store has a catalog of products (ID, Name, Price).
3.  **Invoices:** A manager can generate an invoice for a specific customer. 
    *   An invoice contains multiple Line Items (Product + Quantity).
    *   The system must calculate the **Subtotal**, apply a **Tax Rate (e.g., 18% GST)**, and calculate the **Grand Total**.
4.  **History:** Users can fetch all past invoices generated for a specific customer.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Product` Class**: Holds item details.
2.  **`InvoiceLineItem` Class**: Holds the Product, Quantity, and the calculated cost for that specific row.
3.  **`Invoice` Class**: The main receipt. Holds the Customer, an `ArrayList<InvoiceLineItem>`, generating the final mathematical totals.
4.  **`BillingManager` Class**: Controls the active creation and logging of all invoices.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO: PRODUCT & CUSTOMER
// ==========================================
class Product {
    int id;
    String name;
    double price;

    public Product(int id, String name, double price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }
}

class Customer {
    int id;
    String name;

    public Customer(int id, String name) {
        this.id = id;
        this.name = name;
    }
}

// ==========================================
// 2. POJO: INVOICE & LINE ITEMS
// ==========================================
class InvoiceLineItem {
    Product product;
    int quantity;
    double totalRowPrice;

    public InvoiceLineItem(Product p, int qty) {
        this.product = p;
        this.quantity = qty;
        this.totalRowPrice = p.price * qty;
    }
}

class Invoice {
    static int idProvider = 1000;

    int invoiceId;
    Customer customer;
    List<InvoiceLineItem> items;
    double subToal;
    double taxAmount;
    double grandTotal;
    
    // Constant Tax Rate
    static final double GST_RATE = 0.18; // 18%

    public Invoice(Customer customer) {
        this.invoiceId = idProvider++;
        this.customer = customer;
        this.items = new ArrayList<>();
        this.subToal = 0;
        this.taxAmount = 0;
        this.grandTotal = 0;
    }

    public void addItem(Product p, int qty) {
        InvoiceLineItem line = new InvoiceLineItem(p, qty);
        items.add(line);
        calculateTotals();
    }

    // Recalculates everything dynamically whenever a new item is added!
    private void calculateTotals() {
        subToal = 0;
        for (InvoiceLineItem item : items) {
            subToal += item.totalRowPrice;
        }
        taxAmount = subToal * GST_RATE;
        grandTotal = subToal + taxAmount;
    }

    public void printInvoice() {
        System.out.println("\n==================================");
        System.out.println("      INVOICE #" + invoiceId);
        System.out.println("      Customer: " + customer.name);
        System.out.println("----------------------------------");
        System.out.println("ITEM       QTY       PRICE");
        for (InvoiceLineItem item : items) {
            System.out.printf("%-10s %-9d Rs.%.2f\n", item.product.name, item.quantity, item.totalRowPrice);
        }
        System.out.println("----------------------------------");
        System.out.printf("Subtotal:            Rs.%.2f\n", subToal);
        System.out.printf("GST (18%%):           Rs.%.2f\n", taxAmount);
        System.out.println("----------------------------------");
        System.out.printf("GRAND TOTAL:         Rs.%.2f\n", grandTotal);
        System.out.println("==================================\n");
    }
}

// ==========================================
// 3. THE CORE LOGIC ENGINE (BILLING MANAGER)
// ==========================================
class BillingManager {

    Map<Integer, Product> productDB;
    Map<Integer, Customer> customerDB;
    
    // Customer ID -> List of their historical invoices
    Map<Integer, List<Invoice>> invoiceLedger; 

    public BillingManager() {
        productDB = new HashMap<>();
        customerDB = new HashMap<>();
        invoiceLedger = new HashMap<>();

        productDB.put(1, new Product(1, "Laptop", 50000));
        productDB.put(2, new Product(2, "Mouse", 800));
        productDB.put(3, new Product(3, "Keyboard", 1500));

        customerDB.put(101, new Customer(101, "Arun Ltd."));
    }

    public void createInvoice(int customerId, Map<Integer, Integer> cartItems) {
        if (!customerDB.containsKey(customerId)) {
            System.out.println("❌ Invalid Customer ID.");
            return;
        }

        Customer c = customerDB.get(customerId);
        Invoice newInvoice = new Invoice(c);

        for (Map.Entry<Integer, Integer> currItem : cartItems.entrySet()) {
            int prodId = currItem.getKey();
            int qty = currItem.getValue();

            if (productDB.containsKey(prodId)) {
                newInvoice.addItem(productDB.get(prodId), qty);
            } else {
                System.out.println("⚠️ Warning: Product ID " + prodId + " skipped (Does not exist).");
            }
        }

        if (newInvoice.items.isEmpty()) {
            System.out.println("❌ Invoice generation failed: No valid items provided.");
            return;
        }

        // Save to Ledger
        invoiceLedger.putIfAbsent(customerId, new ArrayList<>());
        invoiceLedger.get(customerId).add(newInvoice);

        System.out.println("✅ Invoice #" + newInvoice.invoiceId + " generated successfully!");
        newInvoice.printInvoice();
    }

    public void viewCustomerHistory(int customerId) {
        if (!invoiceLedger.containsKey(customerId)) {
            System.out.println("📭 No historical invoices found for Customer ID " + customerId);
            return;
        }

        System.out.println("\n--- HISTORY FOR CUSTOMER " + customerId + " ---");
        for (Invoice inv : invoiceLedger.get(customerId)) {
            System.out.println("Invoice #" + inv.invoiceId + " | Total: Rs." + inv.grandTotal);
        }
    }
}

// ==========================================
// 4. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        BillingManager app = new BillingManager();

        while (true) {
            System.out.println("\n=== ZOHO BILLING SYSTEM ===");
            System.out.println("1. Generate New Invoice");
            System.out.println("2. View Customer History");
            System.out.println("3. Exit");
            System.out.print("Enter choice: ");
            int option = sc.nextInt();

            if (option == 1) {
                System.out.println("We are creating an invoice for Customer 101 (Arun Ltd.)");
                Map<Integer, Integer> itemsToBill = new HashMap<>(); // ProdID -> Qty
                
                while(true) {
                    System.out.print("Enter Product ID (1: Laptop, 2: Mouse, 3: Keyboard) or 0 to Finish: ");
                    int pId = sc.nextInt();
                    if(pId == 0) break;
                    
                    System.out.print("Enter Quantity: ");
                    int qty = sc.nextInt();
                    itemsToBill.put(pId, itemsToBill.getOrDefault(pId, 0) + qty);
                }
                
                app.createInvoice(101, itemsToBill);
            } 
            else if (option == 2) {
                System.out.print("Enter Customer ID: ");
                int cId = sc.nextInt();
                app.viewCustomerHistory(cId);
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
1. **The Abstract Item Logic:** We never just store raw text lines in an invoice. Notice how `InvoiceLineItem` physically holds a reference to the `Product` Object. This allows the system to fetch the actual product name and dynamically update prices if needed!
2. **Auto-Computing Fields:** In `Invoice.java`, calling `calculateTotals()` after every `.addItem()` is a classic OOP pattern. It ensures the Math is encapsulated privately inside the object, rather than having the massive `Main` function do the math calculations.
3. **The 1-To-Many Ledger:** `Map<Integer, List<Invoice>> invoiceLedger` perfectly models a relational database's 1-to-many relationship (One Customer has Many Invoices).
