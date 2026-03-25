# 🚕 02. Taxi Booking System (Uber Logic)
### The Complete Zoho Round 3 Solution 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Taxi Booking Application (like Uber/Ola).
**Rules:**
1.  There are **4 Taxis** initially stationed at Point A.
2.  There are **6 Points (A, B, C, D, E, F)** in a straight line.
3.  The distance between each adjacent point is **15 KMs** (e.g., A to B is 15 KM, A to C is 30 KM).
4.  It takes **60 minutes** to travel between two adjacent points.
5.  **Pricing:** Rs. 100 for the first 5 KMs, and Rs. 10 for every subsequent 1 KM.
6.  **Allotment Logic (Crucial):** When a customer requests a taxi, find a free taxi at the pickup point. If no taxi is free at the pickup point, find a free taxi at the *nearest* point. If multiple taxis are free at the same distance, assign the one that has **earned the least amount of money** so far.

---

## 🏗️ SYSTEM DESIGN (The HashMaps & Classes)

We need three files/classes:
1.  **`Taxi` Class**: Stores taxi ID, current location, total earnings, free time, and an `ArrayList` of its completed trips (for printing details later).
2.  **`BookingManager` Class**: The core engine! Contains the logic to find the nearest taxi, calculate the fare, and allocate the trip.
3.  **`Main` Class**: The UI interface with a Scanner to accept Pickup and Drop points.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

You can run this entire code as one file (or break the classes into separate `.java` files).

```java
import java.util.*;

// ==========================================
// 1. POJO: TAXI DATA & TRIP HISTORY
// ==========================================
class Taxi {
    static int idProvider = 1;

    int id;
    char currentLocation;
    int totalEarnings;
    int freeTime; // The time (in hours) when the taxi becomes free again
    List<String> tripHistory; // To print the details later

    public Taxi() {
        this.id = idProvider++;
        this.currentLocation = 'A'; // All taxis start at point A
        this.totalEarnings = 0;
        this.freeTime = 6; // Let's assume the day starts at 6:00 AM
        this.tripHistory = new ArrayList<>();
    }

    public void addTripDetails(int customerId, char pickup, char drop, int pickupTime, int dropTime, int amount) {
        this.currentLocation = drop;
        this.freeTime = dropTime;
        this.totalEarnings += amount;
        
        String details = String.format("   %d            %d          %c           %c          %d            %d            %d", 
                                        this.id, customerId, pickup, drop, pickupTime, dropTime, amount);
        this.tripHistory.add(details);
    }
}

// ==========================================
// 2. THE CORE LOGIC ENGINE (UBER ALGORITHM)
// ==========================================
class BookingManager {

    // --- DATABASE ---
    List<Taxi> taxis;
    int customerIdProvider = 1;

    public BookingManager(int totalTaxis) {
        taxis = new ArrayList<>();
        for (int i = 0; i < totalTaxis; i++) {
            taxis.add(new Taxi());
        }
    }

    // --- CORE SELECTION LOGIC ---
    public void bookTaxi(char pickup, char drop, int pickupTime) {
        
        // 1. Filter Taxis that are FREE at the required pickup time
        List<Taxi> freeTaxis = new ArrayList<>();
        for (Taxi t : taxis) {
            if (t.freeTime <= pickupTime) {
                freeTaxis.add(t);
            }
        }

        if (freeTaxis.size() == 0) {
            System.out.println("❌ No Taxis are currently available at " + pickupTime + ":00 hrs. Please try again later.");
            return;
        }

        // 2. Find the NEAREST Taxi
        // We calculate distance using absolute ASCII difference (e.g., 'C' - 'A' = 2 blocks = 30 KM)
        Taxi bestTaxi = null;
        int minDistance = Integer.MAX_VALUE;

        for (Taxi t : freeTaxis) {
            int distanceToPickup = Math.abs(t.currentLocation - pickup);
            if (distanceToPickup < minDistance) {
                bestTaxi = t;
                minDistance = distanceToPickup;
            } 
            // 3. TIE-BREAKER: If distances are equal, pick the one with LEAST EARNINGS
            else if (distanceToPickup == minDistance) {
                if (bestTaxi == null || t.totalEarnings < bestTaxi.totalEarnings) {
                    bestTaxi = t;
                }
            }
        }

        if (bestTaxi != null) {
            // Calculate Travel Distance and Fare
            int distanceBetweenPickupAndDrop = Math.abs(drop - pickup) * 15; // 15 KM per point
            int fare = calculateFare(distanceBetweenPickupAndDrop);
            int dropTime = pickupTime + Math.abs(drop - pickup); // 1 hour per point

            // Allocate the trip
            bestTaxi.addTripDetails(customerIdProvider++, pickup, drop, pickupTime, dropTime, fare);
            
            System.out.println("✅ Taxi " + bestTaxi.id + " has been assigned successfully!");
            System.out.println("   Distance: " + distanceBetweenPickupAndDrop + " KM | Estimated Fare: Rs. " + fare);
        }
    }

    // --- FARE CALCULATION ---
    private int calculateFare(int totalKms) {
        if (totalKms <= 5) return 100; // First 5 kms is Rs. 100
        return 100 + ((totalKms - 5) * 10); // Rest is Rs. 10 per km
    }

    // --- PRINTING TAXI DETAILS ---
    public void printTaxiDetails() {
        for (Taxi t : taxis) {
            System.out.println("----------------------------------------------------------------------------------");
            System.out.println("Taxi ID: " + t.id + " | Total Earnings: Rs. " + t.totalEarnings + " | Current Location: " + t.currentLocation);
            System.out.println("TaxiID    CustomerID    PickupPoint    DropPoint    PickupTime    DropTime    Amount");
            for (String trip : t.tripHistory) {
                System.out.println(trip);
            }
            if(t.tripHistory.isEmpty()) {
                System.out.println("   (No trips assigned yet)");
            }
        }
        System.out.println("----------------------------------------------------------------------------------");
    }
}

// ==========================================
// 3. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Initialize the system with 4 Taxis
        BookingManager manager = new BookingManager(4);

        while (true) {
            System.out.println("\n=== OLA / UBER BACKEND SYSTEM ===");
            System.out.println("1. Book a Taxi");
            System.out.println("2. Print Taxi Details & History");
            System.out.println("3. Exit");
            System.out.print("Enter choice: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter Pickup Point (A-F): ");
                    char pickup = sc.next().toUpperCase().charAt(0);
                    System.out.print("Enter Drop Point (A-F): ");
                    char drop = sc.next().toUpperCase().charAt(0);
                    System.out.print("Enter Pickup Time (in 24hr format, e.g., 9): ");
                    int time = sc.nextInt();
                    
                    if(pickup < 'A' || pickup > 'F' || drop < 'A' || drop > 'F') {
                        System.out.println("❌ Invalid points! Please enter between A and F.");
                        break;
                    }
                    if(pickup == drop) {
                        System.out.println("❌ Pickup and Drop cannot be the same!");
                        break;
                    }

                    manager.bookTaxi(pickup, drop, time);
                    break;
                case 2:
                    manager.printTaxiDetails();
                    break;
                case 3:
                    System.out.println("Shutting Down...");
                    sc.close();
                    System.exit(0);
            }
        }
    }
}
```

---
## 💡 HOW IT WORKS (Interview Explanation)
If the interviewer asks you to explain the core algorithm:

1.  **Availability Check:** We immediately filter out taxis that are currently on a trip by checking `if (taxi.freeTime <= requestedPickupTime)`.
2.  **ASCII Distance Math:** The secret trick! Because points are sequentially named `A, B, C, D`, their ASCII values map mathematically. To find the distance between `A` and `C`: `abs('C' - 'A')` which is `67 - 65 = 2`. Multiply 2 by the static 15KM rate to get 30KM. No hardcoded arrays are needed!
3.  **The Tie-Breaker Filter:** We keep finding a lower `minDistance`. If the distance is equal, we instantly check `if (totalEarnings < bestTaxi.totalEarnings)` guaranteeing fair wage distribution amongst drivers.
