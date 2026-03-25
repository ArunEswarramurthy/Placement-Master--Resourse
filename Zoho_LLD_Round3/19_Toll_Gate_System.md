# 🎟️ 19. Toll Gate Simulation
### Vehicle Classes, VIP Passes, and Multi-Booth Processing 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Highway Toll Plaza.
**Rules:**
1.  **Vehicle Types:** VIP (Zero Fee), Bike (Rs. 20), Car (Rs. 50), Heavy (Rs. 100).
2.  **Multiple Toll Booths:** The Toll Plaza has multiple parallel booths (e.g., 3 Booths).
3.  **Booth Assignment (Load Balancing Algorithm):** 
    *   When a new vehicle arrives at the highway, DO NOT just assign them to Booth 1 randomly!
    *   Send the vehicle to the booth with the **shortest queue** to optimize traffic!
4.  **Transaction Processing:** Booth operators pull vehicles from their Queue one by one, collect cash, generate a receipt, and let them pass. Calculate total revenue for the day.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Vehicle` Class**: Abstract class storing `licensePlate` and logic to calculate its specific fee.
2.  **`TollBooth` Class**: Represents a physical booth. Has an internal **`Queue<Vehicle>`** of waiting cars, and a `totalCashCollected` tracker.
3.  **`TollManager` Class**: The global load-balancer that looks at all 3 Toll Booth Queues and routes incoming highway traffic optimally.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. ENUMS & VEHICLE ARCHITECTURE
// ==========================================
enum VehicleType { VIP, BIKE, CAR, HEAVY }

class Vehicle {
    String licensePlate;
    VehicleType type;

    public Vehicle(String licensePlate, VehicleType type) {
        this.licensePlate = licensePlate;
        this.type = type;
    }

    public int getTollFee() {
        switch (type) {
            case VIP: return 0;
            case BIKE: return 20;
            case CAR: return 50;
            case HEAVY: return 100;
            default: return 0;
        }
    }
}

// ==========================================
// 2. THE PHYSICAL TOLL BOOTH
// ==========================================
class TollBooth {
    int boothId;
    int totalCashCollected;
    int totalVehiclesPassed;
    
    // Traffic waiting directly behind exactly THIS booth
    Queue<Vehicle> waitingQueue; 

    public TollBooth(int boothId) {
        this.boothId = boothId;
        this.totalCashCollected = 0;
        this.totalVehiclesPassed = 0;
        this.waitingQueue = new LinkedList<>();
    }

    // Pulls the car at the front of the line!
    public void processNextVehicle() {
        if (waitingQueue.isEmpty()) {
            System.out.println("Booth " + boothId + ": 🟢 Queue is empty. Operator is resting.");
            return;
        }

        // Dequeue!
        Vehicle v = waitingQueue.poll();
        int fee = v.getTollFee();

        totalCashCollected += fee;
        totalVehiclesPassed++;

        System.out.println("✅ Receipt [Booth " + boothId + "]: " + v.licensePlate + " (" + v.type + ") paid Rs. " + fee + " -> Crossed successfully.");
    }
}

// ==========================================
// 3. THE GLOBAL ROUTING ENGINE (LOAD BALANCER)
// ==========================================
class TollManager {

    List<TollBooth> allBooths;

    public TollManager(int numBooths) {
        allBooths = new ArrayList<>();
        for (int i = 1; i <= numBooths; i++) {
            allBooths.add(new TollBooth(i));
        }
    }

    // ALGORITHM: Send incoming traffic to the shortest physical line!
    public void addVehicleToPlaza(Vehicle v) {
        TollBooth bestBooth = allBooths.get(0);
        int shortestLine = bestBooth.waitingQueue.size();

        // Loop available booths to find the most efficient line
        for (TollBooth booth : allBooths) {
            if (booth.waitingQueue.size() < shortestLine) {
                shortestLine = booth.waitingQueue.size();
                bestBooth = booth;
            }
        }

        // Add vehicle to the optimally found booth
        bestBooth.waitingQueue.add(v);
        System.out.println("🚗 Traffic Control: Routed " + v.licensePlate + " to Booth " + bestBooth.boothId + " (Line Size: " + (shortestLine + 1) + ")");
    }

    // Simulate real life: Fire processing for ALL booths sequentially to simulate parallel time
    public void processAllBooths() {
        System.out.println("\n--- 🚥 GATES OPENING ---");
        for (TollBooth booth : allBooths) {
            booth.processNextVehicle();
        }
        System.out.println("------------------------\n");
    }

    public void displayPlazaStats() {
        System.out.println("\n=== 🏦 HIGHWAY REVENUE REPORT ===");
        int totalRevenues = 0;
        int totalPassed = 0;
        
        for (TollBooth booth : allBooths) {
            System.out.println("Booth " + booth.boothId + " | Vehicles: " + booth.totalVehiclesPassed + " | Cash: Rs. " + booth.totalCashCollected + " | Queue Length: " + booth.waitingQueue.size());
            totalRevenues += booth.totalCashCollected;
            totalPassed += booth.totalVehiclesPassed;
        }
        System.out.println("---------------------------------");
        System.out.println("Total Plaza Traffic Servered: " + totalPassed);
        System.out.println("Total Plaza Revenue Today: Rs. " + totalRevenues);
        System.out.println("=================================\n");
    }
}

// ==========================================
// 4. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Open the Plaza with exactly 3 parallel Toll Lanes
        TollManager plaza = new TollManager(3);

        while (true) {
            System.out.println("\n=== TOLL GATE SYSTEM ===");
            System.out.println("1. Add Incoming Vehicle to shortest Line");
            System.out.println("2. Process 1 Vehicle at EVERY Booth (Simulate Time)");
            System.out.println("3. Print Financial Status");
            System.out.println("4. Exit");
            System.out.print("Action: ");
            int option = sc.nextInt();
            sc.nextLine();

            if (option == 1) {
                System.out.print("Enter License Plate: "); String lp = sc.nextLine();
                System.out.print("Vehicle Type (1: VIP, 2: BIKE, 3: CAR, 4: HEAVY): "); int typeOpt = sc.nextInt();
                
                VehicleType t = VehicleType.CAR;
                if(typeOpt == 1) t = VehicleType.VIP;
                if(typeOpt == 2) t = VehicleType.BIKE;
                if(typeOpt == 4) t = VehicleType.HEAVY;

                plaza.addVehicleToPlaza(new Vehicle(lp, t));
            } 
            else if (option == 2) {
                plaza.processAllBooths();
            }
            else if (option == 3) {
                plaza.displayPlazaStats();
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
1. **Load Balancing Paradigm:** How does NGINX route traffic to Web Servers? Identically to this! 
    The logic `if (booth.waitingQueue.size() < shortestLine)` is a classic "Least Connections Load Balancer". If Booth 1 has 5 cars, and Booth 2 has 2 cars, it redirects the incoming driver to Booth 2, mimicking perfect real-world highway physics!
2. **Queue (FIFO Data Structure):** A Toll Gate is the literal definition of the FIFO (First In, First Out) algorithm. By mapping `Queue<Vehicle> waitingQueue = new LinkedList<>()`, we leverage the `.poll()` function, ensuring the car that arrived first is computationally guaranteed to trigger its `getTollFee()` receipt before the car behind it!
