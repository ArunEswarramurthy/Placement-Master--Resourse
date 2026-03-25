# 💸 08. Splitwise System (Expense Sharing)
### The Famous Owed/Owesk Balance Algorithm 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for an Expense Sharing application like Splitwise.
**Rules:**
1.  **Users:** A group of friends exist in the system.
2.  **Add Expense:** One person pays a bill for the whole group. The amount must be divided equally among all participants (including the payer).
3.  **Balance Sheet:** The system must track who owes whom.
    *(e.g., If A pays Rs. 300 for A, B, and C. B owes A Rs 100. C owes A Rs 100).*
4.  **Mutual Debt Simplification (Crucial Logic!):** 
    *   If A owes B: Rs 100
    *   And Later B owes A: Rs 50
    *   The system must automatically simplify this to: **A owes B Rs 50.**
5.  **Output:** Print exactly how much each person owes the others.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`User` Class**: Stores name and their personal `Map`.
    *   **The Magic Map:** `Map<Integer, Integer> owes`. This map tracks exactly how much this specific user owes other people. (Key = Friend's ID, Value = Amount Owed).
2.  **`SplitwiseManager` Class**: Handles the math division and updates every involved user's hashmap simultaneously.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO: USER (WITH OWES MAP)
// ==========================================
class User {
    int id;
    String name;
    
    // Key: Friend's User ID | Value: The amount THIS user owes to that friend
    Map<Integer, Double> balances; 

    public User(int id, String name) {
        this.id = id;
        this.name = name;
        this.balances = new HashMap<>();
    }
}

// ==========================================
// 2. THE CORE LOGIC ENGINE (SPLIT MATH)
// ==========================================
class SplitwiseManager {

    Map<Integer, User> userDB;

    public SplitwiseManager() {
        userDB = new HashMap<>();
        // Seed initial friends
        userDB.put(1, new User(1, "Alice"));
        userDB.put(2, new User(2, "Bob"));
        userDB.put(3, new User(3, "Charlie"));
    }

    // --- ADD EXPENSE LOGIC ---
    public void addExpenseEqaul(int payerId, double totalAmount, List<Integer> splitBetweenIds) {
        
        int totalPeople = splitBetweenIds.size();
        if (totalPeople == 0) return;

        double splitAmount = totalAmount / totalPeople;
        User payer = userDB.get(payerId);

        System.out.println("\n✅ EXPENSE ADDED! " + payer.name + " paid Rs. " + totalAmount);
        System.out.println("   (Each person's share: Rs. " + splitAmount + ")");

        for (int borrowerId : splitBetweenIds) {
            // A person does not owe themselves!
            if (borrowerId == payerId) continue; 

            User borrower = userDB.get(borrowerId);

            // ==========================================
            // DEBT SIMPLIFICATION ALGORITHM
            // ==========================================
            
            // Scenario: Does the Payer already owe the Borrower money from before?
            // (e.g., Alice paid 300 for Bob, but Alice already owes Bob 50 from yesterday)
            double payerOwesBorrower = payer.balances.getOrDefault(borrowerId, 0.0);

            if (payerOwesBorrower > 0) {
                // If Alice owes Bob 50, and Bob's new bill is 100...
                if (payerOwesBorrower >= splitAmount) {
                    // Alice's debt easily pays off Bob's new bill! Reduce Alice's debt.
                    payer.balances.put(borrowerId, payerOwesBorrower - splitAmount);
                } else {
                    // Alice's debt (50) pays off half of Bob's new bill (100). 
                    // Alice is cleared of debt, and now Bob owes Alice (50).
                    payer.balances.remove(borrowerId); 
                    double remainingNewDebtForBob = splitAmount - payerOwesBorrower;
                    borrower.balances.put(payerId, borrower.balances.getOrDefault(payerId, 0.0) + remainingNewDebtForBob);
                }
            } else {
                // Standard case: No prior reversed debt. Just add normally!
                // Bob's debt to Alice increases by the split amount
                borrower.balances.put(payerId, borrower.balances.getOrDefault(payerId, 0.0) + splitAmount);
            }
        }
    }

    // --- SHOW ALL BALANCES ---
    public void showBalances() {
        System.out.println("\n--- 💰 CURRENT BALANCES ---");
        boolean everythingSettled = true;

        for (User u : userDB.values()) {
            for (Map.Entry<Integer, Double> entry : u.balances.entrySet()) {
                if (entry.getValue() > 0) {
                    User friend = userDB.get(entry.getKey());
                    System.out.println(u.name + " owes " + friend.name + ": Rs." + entry.getValue());
                    everythingSettled = false;
                }
            }
        }

        if (everythingSettled) {
            System.out.println("Everyone is settled up!");
        }
        System.out.println("---------------------------");
    }
}

// ==========================================
// 3. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        SplitwiseManager app = new SplitwiseManager();

        while (true) {
            System.out.println("\n=== SPLITWISE ===");
            System.out.println("1. Add group expense (Alice, Bob, Charlie)");
            System.out.println("2. Show Balances");
            System.out.println("3. Exit");
            System.out.print("Enter choice: ");
            int option = sc.nextInt();

            if (option == 1) {
                System.out.print("Who paid? (1: Alice, 2: Bob, 3: Charlie): ");
                int payerId = sc.nextInt();
                System.out.print("Enter Total Bill Amount: ");
                double amount = sc.nextDouble();

                // For simplicity, we assume the split involves everyone
                List<Integer> allFriends = Arrays.asList(1, 2, 3);
                
                app.addExpenseEqaul(payerId, amount, allFriends);
            } 
            else if (option == 2) {
                app.showBalances();
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
The holy grail of Splitwise coding is the **Debt Simplification Loop**. 
If you just blindly log "Alice owes Bob 100" and "Bob owes Alice 50", you fail the interview. The graph must auto-resolve cycles. 

How our algorithm handles a complex transaction:
1. `payerOwesBorrower` checks if the physical flow of money is reversing an older record. 
2. If Alice owes Bob 50 currently, and Bob just ate 100 worth of Alice's food...
3. The IF block triggers! It completely wipes (`.remove()`) Alice's debt to Bob out of Alice's HashMap, subtracts 50 from Bob's bill, and registers the remaining 50 into Bob's HashMap as "Bob owes Alice 50".
4. Result: Instead of 2 separate confusing ledger entries, only 1 math-perfect ledger entry remains!
