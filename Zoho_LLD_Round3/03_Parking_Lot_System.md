# 🏙️ 03. Parking Lot System
### Multi-Level Vehicle Parking Architecture 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Multi-Level Parking Lot System.
**Rules:**
1.  The parking lot has **multiple floors** (e.g., 2 floors).
2.  Each floor has **multiple slots** (e.g., 10 slots per floor).
3.  There are **3 types of vehicles:**
    *   `BIKE` (Needs 1 slot of type BIKE/COMPACT)
    *   `CAR` (Needs 1 slot of type COMPACT/LARGE)
    *   `TRUCK` (Needs 1 slot of type LARGE)
4.  When a vehicle enters, the system must **find the nearest available space** (First Floor 1, then Floor 2) and issue a Parking Ticket.
5.  When a vehicle exits, the system calculates the **fee based on hours parked** and frees up the slot.
    *   Bike: Rs. 20/hr | Car: Rs. 50/hr | Truck: Rs. 100/hr

---

## 🏗️ SYSTEM DESIGN (The Architecture)

We need four interconnected classes:
1.  **`Vehicle` (Enum & Class)**: Defines the vehicle type (`BIKE, CAR, TRUCK`) and its license plate.
2.  **`Slot` Class**: Represents a physical parking space on a specific floor, tracking its size/capacity and whether it is currently occupied.
3.  **`Ticket` Class**: Stores the Vehicle, entry time, and the exact Slot it was assigned.
4.  **`ParkingLotManager` Class**: The core engine! Contains the `List<Slot>` and functions to dynamically search for empty spaces, park vehicles, and unpark them.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

You can run this entire code as one file (or separate them for your Zoho interview).

```java
import java.util.*;

// ==========================================
// 1. ENUMS FOR TYPES
// ==========================================
enum VehicleType { BIKE, CAR, TRUCK }

// ==========================================
// 2. POJO: VEHICLE & TICKET
// ==========================================
class Vehicle {
    String licensePlate;
    VehicleType type;

    public Vehicle(String licensePlate, VehicleType type) {
        this.licensePlate = licensePlate;
        this.type = type;
    }
}

class Ticket {
    static int idProvider = 1000; // Ticket Numbers start at 1000
    
    int ticketId;
    Vehicle vehicle;
    Slot assignedSlot;
    int entryTime; // Stored as military hour (e.g., 9 for 9:00 AM)

    public Ticket(Vehicle vehicle, Slot assignedSlot, int entryTime) {
        this.ticketId = idProvider++;
        this.vehicle = vehicle;
        this.assignedSlot = assignedSlot;
        this.entryTime = entryTime;
    }
}

// ==========================================
// 3. POJO: PHYSICAL SLOT IN PARKING LOT
// ==========================================
class Slot {
    int floorNumber;
    int slotNumber;
    VehicleType allowedType; // Which vehicle can park here?
    boolean isOccupied;

    public Slot(int floor, int slot, VehicleType type) {
        this.floorNumber = floor;
        this.slotNumber = slot;
        this.allowedType = type;
        this.isOccupied = false;
    }
}

// ==========================================
// 4. THE CORE LOGIC ENGINE (PARKING MANAGER)
// ==========================================
class ParkingLotManager {

    // --- DATABASE (NO MYSQL ALLOWED!) ---
    List<Slot> allSlots; // Physical map of the building
    Map<Integer, Ticket> activeTickets; // Fast lookup for Unparking

    public ParkingLotManager(int floors, int slotsPerFloor) {
        allSlots = new ArrayList<>();
        activeTickets = new HashMap<>();

        // Initialize the building!
        // Floor 1: Slots 1-3 (Truck), 4-7 (Car), 8-10 (Bike)
        // Floor 2: Slots 1-3 (Truck), 4-7 (Car), 8-10 (Bike)
        for (int f = 1; f <= floors; f++) {
            for (int s = 1; s <= slotsPerFloor; s++) {
                if (s <= 3) allSlots.add(new Slot(f, s, VehicleType.TRUCK));
                else if (s <= 7) allSlots.add(new Slot(f, s, VehicleType.CAR));
                else allSlots.add(new Slot(f, s, VehicleType.BIKE));
            }
        }
    }

    // --- PARKING LOGIC ---
    public void parkVehicle(Vehicle vehicle, int time) {
        Slot availableSlot = findAvailableSlot(vehicle.type);

        if (availableSlot == null) {
            System.out.println("❌ PARKING FULL: No empty slots for " + vehicle.type);
            return;
        }

        // Occupy the slot and generate a ticket
        availableSlot.isOccupied = true;
        Ticket ticket = new Ticket(vehicle, availableSlot, time);
        
        // Save to Database
        activeTickets.put(ticket.ticketId, ticket);

        System.out.println("✅ PARKED SUCCESSFULLY!");
        System.out.println("   Ticket ID: " + ticket.ticketId);
        System.out.println("   Location: Floor " + availableSlot.floorNumber + ", Slot " + availableSlot.slotNumber);
    }

    // Helper: Find the nearest slot dynamically
    private Slot findAvailableSlot(VehicleType type) {
        for (Slot slot : allSlots) {
            if (!slot.isOccupied && slot.allowedType == type) {
                return slot; // Returns the very first empty slot it finds!
            }
        }
        return null;
    }

    // --- UNPARKING LOGIC ---
    public void unparkVehicle(int ticketId, int exitTime) {
        if (!activeTickets.containsKey(ticketId)) {
            System.out.println("❌ Invalid Ticket ID!");
            return;
        }

        Ticket ticket = activeTickets.get(ticketId);
        Slot slot = ticket.assignedSlot;

        // Free up the physical slot
        slot.isOccupied = false;
        
        // Remove from Active DB
        activeTickets.remove(ticketId);

        // Calculate Fee
        int hoursParked = exitTime - ticket.entryTime;
        if (hoursParked <= 0) hoursParked = 1; // Minimum 1 hour charge
        int totalFee = calculateFee(ticket.vehicle.type, hoursParked);

        System.out.println("✅ VEHICLE UNPARKED!");
        System.out.println("   License Plate: " + ticket.vehicle.licensePlate);
        System.out.println("   Hours Parked: " + hoursParked + " hrs");
        System.out.println("   Total Fee: Rs. " + totalFee);
    }

    // Helper: Dynamic Pricing
    private int calculateFee(VehicleType type, int hours) {
        switch (type) {
            case BIKE: return hours * 20;
            case CAR: return hours * 50;
            case TRUCK: return hours * 100;
            default: return 0;
        }
    }

    // --- UTILITY ---
    public void displayAvailability() {
        int bike = 0, car = 0, truck = 0;
        for (Slot s : allSlots) {
            if (!s.isOccupied) {
                if (s.allowedType == VehicleType.BIKE) bike++;
                else if (s.allowedType == VehicleType.CAR) car++;
                else if (s.allowedType == VehicleType.TRUCK) truck++;
            }
        }
        System.out.println("--- AVAILABLE SLOTS ---");
        System.out.println("TRUCKS : " + truck);
        System.out.println("CARS   : " + car);
        System.out.println("BIKES  : " + bike);
    }
}

// ==========================================
// 5. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Initialize building with 2 Floors, 10 Slots per floor
        ParkingLotManager manager = new ParkingLotManager(2, 10);

        while (true) {
            System.out.println("\n=== SMART PARKING LOT ===");
            System.out.println("1. Park a Vehicle");
            System.out.println("2. Unpark a Vehicle");
            System.out.println("3. Display Available Slots");
            System.out.println("4. Exit");
            System.out.print("Enter choice: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter License Plate: ");
                    String lp = sc.next();
                    System.out.print("Enter Type (1 for BIKE, 2 for CAR, 3 for TRUCK): ");
                    int typeChoice = sc.nextInt();
                    System.out.print("Enter Entry Hour (1-24): ");
                    int time = sc.nextInt();

                    VehicleType type = VehicleType.BIKE;
                    if(typeChoice == 2) type = VehicleType.CAR;
                    if(typeChoice == 3) type = VehicleType.TRUCK;

                    manager.parkVehicle(new Vehicle(lp, type), time);
                    break;
                case 2:
                    System.out.print("Enter Ticket ID: ");
                    int ticketId = sc.nextInt();
                    System.out.print("Enter Exit Hour (1-24): ");
                    int exitTime = sc.nextInt();
                    
                    manager.unparkVehicle(ticketId, exitTime);
                    break;
                case 3:
                    manager.displayAvailability();
                    break;
                case 4:
                    System.out.println("Shutting Down System...");
                    System.exit(0);
            }
        }
    }
}
```

---
## 💡 HOW IT WORKS (Interview Explanation)
If the interviewer asks you to explain the data modeling:
1.  **The Slot Initialization:** Every physical space in the entire building is virtually represented by adding `Slot` objects to the `List<Slot> allSlots`. This handles multi-level complexity automatically! Floor 1, Slot 1 and Floor 2, Slot 1 are completely distinct objects in the List.
2.  **Greedy Search Algorithm:** `findAvailableSlot()` loops through `allSlots` from the beginning (Floor 1). The exact moment it hits an `.isOccupied == false` slot that matches the vehicle type, it returns it! This guarantees vehicles park on lower floors first.
3.  **Active Ticket Lookup:** We use `Map<Integer, Ticket> activeTickets`. When a user types their `Ticket ID` at the exit machine, `activeTickets.get(id)` allows us to find their vehicle, entry time, and exact parking spot in **O(1) continuous time** without searching the building!
