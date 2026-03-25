# 🏧 04. ATM Machine Simulator
### Note Denomination Tracking & Transaction Logic 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for an ATM Machine.
**Rules:**
1.  **ATM Storage:** The ATM stores cash in specific denominations: Rs. 2000, 500, 200, and 100.
2.  **Customer DB:** Customers have an exact account balance and a 4-digit PIN.
3.  **Deposit Logic:** When a customer deposits money, they must specify *exactly how many notes* of each denomination they are inserting (e.g., Two 500s and One 100). The ATM adds this to its internal vault and updates the customer's balance.
4.  **Withdrawal Logic (The Tricky Part):** When a customer withdraws, the ATM must deduct the amount using the **highest possible denominations first** (Greedy Algorithm). 
    *   *If the ATM does not have the exact change, it must decline the transaction!*
5.  **Security:** Limit wrong PIN attempts to 3 times before locking the card.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

We need three primary files/classes:
1.  **`Customer` Class**: Stores the Bank Account details, PIN, and balance.
2.  **`ATM` Class**: The physical machine! It holds a huge `Map<Integer, Integer>` to track exactly how many Rs. 100, Rs. 500 bills it has left in its physical vault.
3.  **`Main` Class**: The UI interface with a Scanner.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

You can run this entire code as one file.

```java
import java.util.*;

// ==========================================
// 1. POJO: CUSTOMER DETAILS
// ==========================================
class Customer {
    int accountNo;
    String accountName;
    int pin;
    int balance;
    int failedAttempts;
    boolean isLocked;

    public Customer(int accountNo, String accountName, int pin, int balance) {
        this.accountNo = accountNo;
        this.accountName = accountName;
        this.pin = pin;
        this.balance = balance;
        this.failedAttempts = 0;
        this.isLocked = false;
    }
}

// ==========================================
// 2. THE CORE LOGIC ENGINE (THE ATM MACHINE)
// ==========================================
class ATM {

    // --- DATABASE ---
    // Customer DB
    Map<Integer, Customer> bankDatabase;
    
    // ATM Vault DB (Denomination -> Count of Notes)
    Map<Integer, Integer> atmVault;
    int totalAtmCash;

    public ATM() {
        bankDatabase = new HashMap<>();
        atmVault = new LinkedHashMap<>(); // To keep insertion order!
        totalAtmCash = 0;

        // Initialize ATM Vault with 0 notes initially
        // We use LinkedHashMap so it loops in descending order automatically later!
        atmVault.put(2000, 0);
        atmVault.put(500, 0);
        atmVault.put(200, 0);
        atmVault.put(100, 0);

        // Pre-fill some Dummy Customers
        bankDatabase.put(101, new Customer(101, "Arun", 2343, 25000));
        bankDatabase.put(102, new Customer(102, "Sita", 5432, 10000));
        bankDatabase.put(103, new Customer(103, "Ravi", 1234, 50000));
    }

    // --- ADMIN LOGIC: LOAD MONEY INTO ATM ---
    public void loadCash(int n2000, int n500, int n200, int n100) {
        atmVault.put(2000, atmVault.get(2000) + n2000);
        atmVault.put(500, atmVault.get(500) + n500);
        atmVault.put(200, atmVault.get(200) + n200);
        atmVault.put(100, atmVault.get(100) + n100);

        refreshTotalCash();
        System.out.println("✅ ATM Vault loaded successfully! Total Cash: Rs. " + totalAtmCash);
    }

    private void refreshTotalCash() {
        totalAtmCash = 0;
        for (Map.Entry<Integer, Integer> entry : atmVault.entrySet()) {
            totalAtmCash += (entry.getKey() * entry.getValue());
        }
    }

    // --- AUTHENTICATION LOGIC ---
    public Customer authenticate(int accNo, int pin) {
        if (!bankDatabase.containsKey(accNo)) {
            System.out.println("❌ Invalid Account Number!");
            return null;
        }

        Customer c = bankDatabase.get(accNo);
        if (c.isLocked) {
            System.out.println("❌ ACCOUNT LOCKED! Please contact the bank.");
            return null;
        }

        if (c.pin != pin) {
            c.failedAttempts++;
            System.out.println("❌ Wrong PIN! Attempt " + c.failedAttempts + " of 3.");
            if (c.failedAttempts >= 3) {
                c.isLocked = true;
                System.out.println("❌ ACCOUNT NOW LOCKED due to too many failed attempts.");
            }
            return null;
        }

        c.failedAttempts = 0; // Reset on success
        System.out.println("✅ Welcome, " + c.accountName + "!");
        return c;
    }

    // --- DEPOSIT LOGIC ---
    public void deposit(Customer c, int n2000, int n500, int n200, int n100) {
        int depositAmount = (n2000 * 2000) + (n500 * 500) + (n200 * 200) + (n100 * 100);
        
        if(depositAmount == 0) return;

        // 1. Update Customer Balance
        c.balance += depositAmount;

        // 2. Add physical notes to the ATM Vault
        atmVault.put(2000, atmVault.get(2000) + n2000);
        atmVault.put(500, atmVault.get(500) + n500);
        atmVault.put(200, atmVault.get(200) + n200);
        atmVault.put(100, atmVault.get(100) + n100);

        refreshTotalCash();

        System.out.println("✅ Deposit Successful! Rs. " + depositAmount + " credited.");
        System.out.println("   New Balance: Rs. " + c.balance);
    }

    // --- WITHDRAWAL LOGIC (THE TRICKY PART) ---
    public void withdraw(Customer c, int amount) {
        if (amount > c.balance) {
            System.out.println("❌ Insufficient Account Balance!");
            return;
        }
        if (amount > totalAtmCash) {
            System.out.println("❌ ATM Out of Cash! Max available: Rs. " + totalAtmCash);
            return;
        }
        if (amount % 100 != 0) {
            System.out.println("❌ Please enter a multiple of 100.");
            return;
        }

        // GREEDY ALGORITHM: Try to build the amount using highest notes first
        Map<Integer, Integer> withdrawnNotes = new LinkedHashMap<>();
        int remainingAmount = amount;

        for (Map.Entry<Integer, Integer> entry : atmVault.entrySet()) {
            int denom = entry.getKey();
            int atmHasCount = entry.getValue();

            if (remainingAmount >= denom && atmHasCount > 0) {
                // How many notes of this denomination do we need?
                int notesNeeded = remainingAmount / denom;
                
                // We can only take what the ATM actually has!
                int notesToTake = Math.min(notesNeeded, atmHasCount);

                withdrawnNotes.put(denom, notesToTake);
                remainingAmount -= (notesToTake * denom);
            }
            if (remainingAmount == 0) break; // We successfully found the exact change!
        }

        // Check if we successfully formed the amount
        if (remainingAmount > 0) {
            System.out.println("❌ ATM does not have exact change combinations for this amount.");
            return;
        }

        // SUCCESS! Execute the transaction.
        // 1. Deduct from Customer
        c.balance -= amount;

        // 2. Remove physical notes from ATM Vault
        for (Map.Entry<Integer, Integer> entry : withdrawnNotes.entrySet()) {
            int denom = entry.getKey();
            int notesTaken = entry.getValue();
            atmVault.put(denom, atmVault.get(denom) - notesTaken);
        }

        refreshTotalCash();

        System.out.println("✅ Please collect your cash: Rs. " + amount);
        System.out.println("   Dispended: ");
        for (Map.Entry<Integer, Integer> entry : withdrawnNotes.entrySet()) {
             System.out.println("     " + entry.getValue() + " notes of Rs. " + entry.getKey());
        }
        System.out.println("   New Balance: Rs. " + c.balance);
    }

    public void displayVault() {
        System.out.println("--- INTERNAL ATM VAULT ---");
        System.out.println("2000s: " + atmVault.get(2000));
        System.out.println(" 500s: " + atmVault.get(500));
        System.out.println(" 200s: " + atmVault.get(200));
        System.out.println(" 100s: " + atmVault.get(100));
        System.out.println("TOTAL: Rs. " + totalAtmCash);
        System.out.println("--------------------------");
    }
}

// ==========================================
// 3. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ATM atm = new ATM();

        // Admin pre-loads the ATM with some cash to start the day
        atm.loadCash(10, 20, 50, 100); // (20000 + 10000 + 10000 + 10000 = 50,000)

        while (true) {
            System.out.println("\n=== HDFC ATM TERMINAL ===");
            System.out.println("1. Customer Login");
            System.out.println("2. Admin: View Vault");
            System.out.println("3. Exit");
            System.out.print("Enter choice: ");
            int option = sc.nextInt();

            if (option == 1) {
                System.out.print("Enter Acc No: "); int acc = sc.nextInt();
                System.out.print("Enter PIN: "); int pin = sc.nextInt();

                Customer c = atm.authenticate(acc, pin);
                if (c != null) {
                    while (true) {
                        System.out.println("\n--- MAIN MENU ---");
                        System.out.println("1. Check Balance  |  2. Withdraw  |  3. Deposit  |  4. Logout");
                        System.out.print("Option: ");
                        int choice = sc.nextInt();

                        if (choice == 1) {
                            System.out.println("💰 Balance: Rs. " + c.balance);
                        } 
                        else if (choice == 2) {
                            System.out.print("Enter amount to withdraw: ");
                            int amount = sc.nextInt();
                            atm.withdraw(c, amount);
                        } 
                        else if (choice == 3) {
                            System.out.println("Enter number of notes you are inserting:");
                            System.out.print("2000s: "); int n2k = sc.nextInt();
                            System.out.print(" 500s: "); int n500 = sc.nextInt();
                            System.out.print(" 200s: "); int n200 = sc.nextInt();
                            System.out.print(" 100s: "); int n100 = sc.nextInt();
                            atm.deposit(c, n2k, n500, n200, n100);
                        } 
                        else if (choice == 4) {
                            System.out.println("Logging out... Thank you!");
                            break;
                        }
                    }
                }
            } else if (option == 2) {
                atm.displayVault();
            } else {
                System.exit(0);
            }
        }
    }
}
```

---
## 💡 HOW IT WORKS (Interview Explanation)
1.  **LinkedHashMap Magic:** For the `atmVault`, we used a `LinkedHashMap` instead of a standard `HashMap`. Standard HashMaps do NOT guarantee insertion order! By using a LinkedHashMap, when we loop through the vault during withdrawal, it automatically checks the `2000` notes first, then `500`, executing a perfect **Greedy Algorithm** without needing a sorting function!
2.  **The Failsafe Withdrawal:** Notice that in the `withdraw` math block, we do NOT deduct anything from the vault or the user's balance yet. We use a temporary `withdrawnNotes` map to mathematically "test" if we have exact change. Only after `remainingAmount == 0` do we permanently execute the deduction. This prevents the ATM from accidentally stealing a user's balance if it runs out of 100-rupee notes midway through dispensing cash!
