# ✈️ 05. Flight Booking System
### Dynamic Pricing & Ticket Cancellation Logic 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Flight Ticket Booking application.
**Rules:**
1.  **Multiple Flights:** The system manages 2 flights (Flight 101 and Flight 102).
2.  **Seat Capacity:** Each flight has exactly 50 seats available initially.
3.  **Dynamic Pricing Strategy (Crucial):**
    *   The starting price for a ticket on any flight is **Rs. 5000**.
    *   Every time a ticket is booked on a flight, the price for the **next** ticket on that specific flight jumps by **Rs. 200**.
    *   *(e.g., Passenger A buys for 5000. Passenger B buys for 5200. Passenger C buys for 5400).*
4.  **Cancellation Logic:** When a passenger cancels their ticket, the flight refunds them the exact amount they paid, makes the seat available again, and **drops the current flight price by Rs. 200**.
5.  **Multi-Passenger Booking:** A user can book multiple seats in one single transaction (e.g., 3 seats at once).
    *   Wait... if they book 3 seats, seat 1 costs 5000, seat 2 costs 5200, and seat 3 costs 5400! Total bill = 15600.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

We need three primary files/classes:
1.  **`Passenger` Class**: Stores the passenger ID, the specific flight booked, the number of seats they purchased, and the exact total amount they paid (for accurate refunds later).
2.  **`Flight` Class**: Stores its Flight ID, available seats, current dynamic price ticket, and a `List<Passenger>` of everyone on the flight.
3.  **`BookingManager` Class**: The global interface to search flights, calculate dynamic math, and process transactions.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

You can run this entire code as one file.

```java
import java.util.*;

// ==========================================
// 1. POJO: PASSENGER & TICKET DETAILS
// ==========================================
class Passenger {
    static int idProvider = 1;

    int passengerId;
    int flightId;
    int noOfSeatsBooked;
    int totalPaidAmount; // Vital for accurate refunds!

    public Passenger(int flightId, int noOfSeatsBooked, int totalPaidAmount) {
        this.passengerId = idProvider++;
        this.flightId = flightId;
        this.noOfSeatsBooked = noOfSeatsBooked;
        this.totalPaidAmount = totalPaidAmount;
    }
}

// ==========================================
// 2. POJO: SPECIFIC FLIGHT LOGIC
// ==========================================
class Flight {
    int flightId;
    int availableSeats;
    int currentTicketPrice;
    
    // Database of passengers specifically on THIS flight
    List<Passenger> passengerList; 

    public Flight(int flightId) {
        this.flightId = flightId;
        this.availableSeats = 50;
        this.currentTicketPrice = 5000;
        this.passengerList = new ArrayList<>();
    }

    // Math function to calculate total if user books multiple seats at once
    public int calculateCostForMultipleSeats(int numberOfSeats) {
        int cost = 0;
        int tempPrice = currentTicketPrice;
        for (int i = 0; i < numberOfSeats; i++) {
            cost += tempPrice;
            tempPrice += 200; // Simulating the price jump for the next loop run
        }
        return cost;
    }

    public void bookSeats(Passenger p) {
        // Add passenger to the flight manifest
        passengerList.add(p);
        
        // Update flight status
        availableSeats -= p.noOfSeatsBooked;
        currentTicketPrice += (p.noOfSeatsBooked * 200); // Scale the price up permanently
        
        System.out.println("✅ BOOKING SUCCESSFUL! Passenger ID: " + p.passengerId);
        System.out.println("   Seats Booked: " + p.noOfSeatsBooked + " |  Total Paid: Rs. " + p.totalPaidAmount);
        System.out.println("   (Next ticket on this flight will now cost Rs. " + currentTicketPrice + ")");
    }

    public void cancelTicket(int passengerId) {
        Passenger passengerToCancel = null;
        
        // Find the passenger inside this flight's list
        for (Passenger p : passengerList) {
            if (p.passengerId == passengerId) {
                passengerToCancel = p;
                break;
            }
        }

        if (passengerToCancel == null) {
            System.out.println("❌ Error: Passenger ID not found on Flight " + flightId);
            return;
        }

        // Refund and restore state
        passengerList.remove(passengerToCancel);
        availableSeats += passengerToCancel.noOfSeatsBooked;
        
        // Drop the price back down!
        currentTicketPrice -= (passengerToCancel.noOfSeatsBooked * 200);

        System.out.println("✅ TICKET CANCELLED! Refund Initiated: Rs. " + passengerToCancel.totalPaidAmount);
        System.out.println("   (Flight price drops back down to Rs. " + currentTicketPrice + ")");
    }

    public void printFlightSummary() {
        System.out.println("\n--- FLIGHT " + flightId + " SUMMARY ---");
        System.out.println("Available Seats: " + availableSeats);
        System.out.println("Current Single Ticket Price: Rs. " + currentTicketPrice);
        System.out.println("Passenger Manifest:");
        if (passengerList.isEmpty()) {
             System.out.println("  (Empty)");
        }
        for (Passenger p : passengerList) {
            System.out.println("   -> ID: " + p.passengerId + " | Seats: " + p.noOfSeatsBooked + " | Paid: Rs. " + p.totalPaidAmount);
        }
    }
}

// ==========================================
// 3. THE CORE LOGIC ENGINE (BOOKING MANAGER)
// ==========================================
class BookingManager {

    // Database of all Flights
    Map<Integer, Flight> allFlights;

    public BookingManager() {
        allFlights = new HashMap<>();
        // Initialize the two requested flights
        allFlights.put(101, new Flight(101));
        allFlights.put(102, new Flight(102));
    }

    public void bookProcess(int flightId, int seatsRequired) {
        if (!allFlights.containsKey(flightId)) {
            System.out.println("❌ Invalid Flight ID!");
            return;
        }

        Flight f = allFlights.get(flightId);

        if (f.availableSeats < seatsRequired) {
            System.out.println("❌ Booking Failed: Only " + f.availableSeats + " seats available.");
            return;
        }

        // Calculate exact cost with dynamic pricing inflation
        int totalCost = f.calculateCostForMultipleSeats(seatsRequired);

        // Generate Ticket & Passenger Object
        Passenger p = new Passenger(flightId, seatsRequired, totalCost);

        // Tell the flight to execute the booking
        f.bookSeats(p);
    }

    public void cancelProcess(int flightId, int passengerId) {
         if (!allFlights.containsKey(flightId)) {
            System.out.println("❌ Invalid Flight ID!");
            return;
        }
        Flight f = allFlights.get(flightId);
        f.cancelTicket(passengerId);
    }

    public void printAllFlights() {
        for (Flight f : allFlights.values()) {
            f.printFlightSummary();
        }
    }
}

// ==========================================
// 4. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        BookingManager manager = new BookingManager();

        while (true) {
            System.out.println("\n=== MAKE-MY-TRIP FLIGHT ENGINE ===");
            System.out.println("1. Book Ticket");
            System.out.println("2. Cancel Ticket");
            System.out.println("3. Flight Summaries");
            System.out.println("4. Exit");
            System.out.print("Enter choice: ");
            int option = sc.nextInt();

            if (option == 1) {
                System.out.print("Enter Flight ID (101 or 102): "); int fId = sc.nextInt();
                System.out.print("Enter Number of Seats required: "); int seats = sc.nextInt();
                manager.bookProcess(fId, seats);
            } 
            else if (option == 2) {
                System.out.print("Enter Flight ID: "); int fId = sc.nextInt();
                System.out.print("Enter Passenger ID: "); int pId = sc.nextInt();
                manager.cancelProcess(fId, pId);
            } 
            else if (option == 3) {
                manager.printAllFlights();
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
1.  **Decentralized Logic (OOP Paradigm):** Notice how `BookingManager` does NOT do the heavy math calculation! It grabs the specific `Flight` object and asks the flight to calculate the cost via `f.calculateCostForMultipleSeats()`. This proves to the interviewer that you understand true Object-Oriented isolation and responsibilities.
2.  **Dynamic Loop Calculus:** If a user demands 3 seats immediately, we cannot just multiply `5000 * 3`. The `calculateCostForMultipleSeats` method uses a temporary price (`tempPrice`) that acts like a while-loop counter, increasing by 200 for every seat the user demands in the bulk order, ensuring perfectly accurate billing!
3.  **Self-healing State:** If someone cancels their ticket, the `cancelTicket` function extracts how many seats they held and reverses the math (`currentTicketPrice -= (seats * 200)`), instantly healing the system to correct defaults for the next buyer.
