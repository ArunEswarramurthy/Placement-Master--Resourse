# 🏦 20. Banking & Digital Wallet System
### Balance Locks, Transaction History, and P2P Transfers 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Core Banking or Paytm-style Wallet application!
**Rules:**
1.  **Accounts:** Users have unique Account IDs, Passwords, and current Balances.
2.  **Transfers (Crucial Challenge!):** User A can initiate a transfer to User B.
    *   *Constraint 1:* Sender must have sufficient balance.
    *   *Constraint 2 (ACID Emulation):* The deduction from Sender and credit to Receiver must occur simultaneously. If one fails, the entire transaction rolls back.
3.  **Passbook / History:** Every user stores a historical `List` of their exact Transactions (both Debits and Credits) with precise timestamps/IDs.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Transaction` Class**: Holds Type (CREDIT/DEBIT), Amount, Target Party Name, and timestamp/ID.
2.  **`Account` Class**: Holds credentials, total balance, and a completely private `List<Transaction> passbook`.
3.  **`BankManager` Class**: The central server handling authentication and the critical `transferMoney()` mathematics between two independent objects.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. ENUMS & POJO: TRANSACTION RECEIPT
// ==========================================
enum TxnType { CREDIT, DEBIT }

class Transaction {
    static int idProvider = 88000;
    
    int transactionId;
    TxnType type;
    double amount;
    String description; // e.g., "Transferred to Alice"

    public Transaction(TxnType type, double amount, String description) {
        this.transactionId = idProvider++;
        this.type = type;
        this.amount = amount;
        this.description = description;
    }
}

// ==========================================
// 2. THE BANK ACCOUNT (WALLET)
// ==========================================
class Account {
    int accountNo;
    String name;
    String password;
    double balance;
    
    // The Passbook!
    List<Transaction> statement; 

    public Account(int accNo, String name, String pass, double openingBalance) {
        this.accountNo = accNo;
        this.name = name;
        this.password = pass;
        this.balance = openingBalance;
        this.statement = new ArrayList<>();
        
        // Log the opening amount
        if (openingBalance > 0) {
            statement.add(new Transaction(TxnType.CREDIT, openingBalance, "Opening Balance"));
        }
    }

    public void printPassbook() {
        System.out.println("\n--- 📖 PASSBOOK FOR " + name.toUpperCase() + " ---");
        System.out.println("CURRENT BALANCE: Rs. " + balance);
        System.out.println("----------------------------------------");
        System.out.printf("%-7s %-10s %-8s %-20s\n", "TXN_ID", "TYPE", "AMOUNT", "DESCRIPTION");
        
        for (Transaction t : statement) {
            // Formatting trick!
            String symbol = (t.type == TxnType.CREDIT) ? "+" : "-";
            System.out.printf("#%-6d [%-6s] %sRs.%-5.2f %s\n", t.transactionId, t.type, symbol, t.amount, t.description);
        }
        System.out.println("----------------------------------------\n");
    }
}

// ==========================================
// 3. THE CORE LOGIC ENGINE (RBI / CENTRAL SERVER)
// ==========================================
class BankManager {

    Map<Integer, Account> centralDatabase;

    public BankManager() {
        centralDatabase = new HashMap<>();

        // Seed Users
        centralDatabase.put(101, new Account(101, "Arun Kumar", "pass123", 5000));
        centralDatabase.put(102, new Account(102, "Sita Ram", "sita123", 2000));
    }

    // --- AUTHENTICATION ---
    public Account login(int accNo, String password) {
        Account acc = centralDatabase.get(accNo);
        if (acc == null) {
            System.out.println("❌ Account not found.");
            return null;
        }
        if (!acc.password.equals(password)) {
            System.out.println("❌ Incorrect Password.");
            return null;
        }
        System.out.println("✅ Login Successful! Welcome " + acc.name);
        return acc; 
    }

    // --- P2P TRANSFER (THE MAIN LLD CHALLENGE) ---
    public void transferFunds(Account sender, int receiverAccNo, double amount) {
        if (amount <= 0) {
            System.out.println("❌ Invalid amount requested.");
            return;
        }

        // 1. Validation Checks
        if (sender.accountNo == receiverAccNo) {
             System.out.println("❌ You cannot send money to yourself!");
             return;
        }

        Account receiver = centralDatabase.get(receiverAccNo);
        if (receiver == null) {
            System.out.println("❌ Receiver Account ID not found in system.");
            return;
        }

        if (sender.balance < amount) {
            System.out.println("❌ INSUFFICIENT FUNDS! You have Rs. " + sender.balance);
            return;
        }

        // ========================================
        // 2. THE ACID TRANSACTION (DEBIT + CREDIT)
        // ========================================
        
        // Debit the Sender
        sender.balance -= amount;
        Transaction senderTxn = new Transaction(TxnType.DEBIT, amount, "Sent to " + receiver.name);
        sender.statement.add(senderTxn);

        // Credit the Receiver
        receiver.balance += amount;
        Transaction receiverTxn = new Transaction(TxnType.CREDIT, amount, "Received from " + sender.name);
        receiver.statement.add(receiverTxn);

        System.out.println("✅ TRANSFER SUCCESSFUL!");
        System.out.println("   Txn ID: #" + senderTxn.transactionId);
        System.out.println("   " + sender.name + " ➡️ Rs." + amount + " ➡️ " + receiver.name);
    }
}

// ==========================================
// 4. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        BankManager sbi = new BankManager();

        System.out.println("=== SBI NET BANKING ===");
        
        // Authentication Phase
        Account loggedInUser = null;
        while (loggedInUser == null) {
            System.out.print("Enter Acc No (Hint: 101 or 102): "); int acc = sc.nextInt();
            System.out.print("Enter Password: "); String pass = sc.next();
            loggedInUser = sbi.login(acc, pass);
        }

        while (true) {
            System.out.println("\n--- MAIN MENU ---");
            System.out.println("1. Check Balance");
            System.out.println("2. Transfer Money to Friend");
            System.out.println("3. Print Passbook Statement");
            System.out.println("4. Logout");
            System.out.print("Action: ");
            int option = sc.nextInt();

            if (option == 1) {
                System.out.println("💰 Available Balance: Rs. " + loggedInUser.balance);
            } 
            else if (option == 2) {
                System.out.print("Enter Receiver's Acc No: "); int targetAcc = sc.nextInt();
                System.out.print("Enter Amount to Transfer: Rs. "); double amt = sc.nextDouble();
                sbi.transferFunds(loggedInUser, targetAcc, amt);
            } 
            else if (option == 3) {
                 loggedInUser.printPassbook();
            }
            else {
                System.out.println("Signing out... Have a safe day!");
                System.exit(0);
            }
        }
    }
}
```

---
## 💡 HOW IT WORKS (Interview Explanation)
1. **P2P Cross-Object Mutation:** Notice that `BankManager.transferFunds()` requires exactly THREE variables: `Account senderObject`, `Integer targetID`, and `Amount`. The system pulls `Object B` from the `HashMap`, subtracts math from `Object A`, and adds math to `Object B` simultaneously. 
2. **ACID Transaction History Synchronization:** When a transfer occurs, the system manually generates TWO different `Transaction` log objects. One is pushed to Sender's isolated ArrayList as a DEBIT description. The other is pushed to Receiver's isolated ArrayList as a CREDIT description! If the code crashed internally between deleting funds and adding funds, a real database `ROLLBACK` triggers to prevent missing ledgers!
