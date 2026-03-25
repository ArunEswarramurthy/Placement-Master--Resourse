# 🚆 01. Railway Reservation System (IRCTC)
### The Absolute Most Asked Zoho Round 3 Question 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Railway Ticket Booking System.
**Rules:**
1.  There are a total of **63 confirmed seats** (21 Lower, 21 Middle, 21 Upper).
2.  There are **18 RAC (Reservation Against Cancellation)** seats.
3.  There are **10 Waiting List (WL)** tickets.
4.  If Confirmed is full -> Issue RAC.
5.  If RAC is full -> Issue Waiting List.
6.  If WL is full -> Print "No Tickets Available".
7.  **Cancellation Logic:** If a confirmed ticket is cancelled, an RAC passenger moves to Confirmed. A Waiting List passenger moves to RAC.

---

## 🏗️ SYSTEM DESIGN (The HashMaps & Classes)

We need three primary files/classes:
1.  **`Passenger` Class**: Stores name, age, berth preference, and allocated seat.
2.  **`TicketBooker` Class**: The core engine! Contains the logic for booking, cancelling, and shifting passengers from RAC -> Confirmed.
3.  **`Main` Class**: The UI interface with a Scanner and Switch case.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

You can run this entire code as one file (or break the classes into separate `.java` files).

```java
import java.util.*;

// ==========================================
// 1. POJO: PASSENGER DATA
// ==========================================
class Passenger {
    static int idProvider = 1; // Auto-increments for every new passenger
    
    int passengerId;
    String name;
    int age;
    char berthPreference; // 'L', 'M', 'U'
    String allocatedBerth; // e.g., "1L", "5M", "RAC"
    int seatNumber;

    public Passenger(String name, int age, char berthPreference) {
        this.passengerId = idProvider++;
        this.name = name;
        this.age = age;
        this.berthPreference = berthPreference;
    }
}

// ==========================================
// 2. THE CORE LOGIC ENGINE
// ==========================================
class TicketBooker {
    
    // --- SYSTEM CONSTRAINTS ---
    static int availableLowerBerths = 21; // Changing to 1 or 2 for testing is highly recommended!
    static int availableMiddleBerths = 21;
    static int availableUpperBerths = 21;
    static int availableRacTickets = 18;
    static int availableWaitingList = 10;

    // --- SEAT TRACKERS (Lists of Available Seat Numbers 1 to 21) ---
    static List<Integer> lowerBerthsPositions = new ArrayList<>(Arrays.asList(1,2,3...21)); // Using pseudo-code here, use loop to fill 1 to 21
    static List<Integer> middleBerthsPositions = new ArrayList<>(Arrays.asList(1...21));
    static List<Integer> upperBerthsPositions = new ArrayList<>(Arrays.asList(1...21));
    static List<Integer> racPositions = new ArrayList<>(Arrays.asList(1...18));
    static List<Integer> waitingListPositions = new ArrayList<>(Arrays.asList(1...10));

    // --- DATABASE (NO MYSQL ALLOWED!) ---
    // Storing Passenger Info (ID -> Passenger)
    static Map<Integer, Passenger> passengersDatabase = new HashMap<>();
    
    // Ordered queues to easily pop the next person in line during cancellation
    static Queue<Integer> racList = new LinkedList<>(); 
    static Queue<Integer> waitingList = new LinkedList<>();

    // --- CONSTRUCTOR INITIALIZER (Fill the standard arrays 1 to N) ---
    public TicketBooker() {
        for(int i=1; i<=21; i++) { lowerBerthsPositions.add(i); middleBerthsPositions.add(i); upperBerthsPositions.add(i); }
        for(int i=1; i<=18; i++) racPositions.add(i);
        for(int i=1; i<=10; i++) waitingListPositions.add(i);
    }

    // --- BOOKING LOGIC ---
    public void bookTicket(Passenger p, int berthInfo, String allotedBerth) {
        // Assign the seat number and type
        p.seatNumber = berthInfo;
        p.allocatedBerth = allotedBerth;
        
        // Save to Database
        passengersDatabase.put(p.passengerId, p);

        // Deduct from available counters and remove the exact seat number from the list
        if(allotedBerth.equals("L")) { availableLowerBerths--; lowerBerthsPositions.remove(Integer.valueOf(berthInfo)); }
        else if(allotedBerth.equals("M")) { availableMiddleBerths--; middleBerthsPositions.remove(Integer.valueOf(berthInfo)); }
        else if(allotedBerth.equals("U")) { availableUpperBerths--; upperBerthsPositions.remove(Integer.valueOf(berthInfo)); }
        else if(allotedBerth.equals("RAC")) { availableRacTickets--; racPositions.remove(Integer.valueOf(berthInfo)); racList.add(p.passengerId); }
        else if(allotedBerth.equals("WL")) { availableWaitingList--; waitingListPositions.remove(Integer.valueOf(berthInfo)); waitingList.add(p.passengerId); }

        System.out.println("✅ TICKET BOOKED SUCCESSFULLY! (Passenger ID: " + p.passengerId + ", Seat: " + berthInfo + allotedBerth + ")");
    }

    // --- CANCELLATION & SHIFTING LOGIC ---
    public void cancelTicket(int passengerId) {
        if (!passengersDatabase.containsKey(passengerId)) {
            System.out.println("❌ Invalid Passenger ID!");
            return;
        }

        Passenger p = passengersDatabase.get(passengerId);
        passengersDatabase.remove(passengerId); // Delete from DB

        // Step 1: Free up the seat the passenger was using
        int freedSeat = p.seatNumber;
        System.out.println("Passenger " + p.name + " cancelled their ticket.");

        if(p.allocatedBerth.equals("L")) { availableLowerBerths++; lowerBerthsPositions.add(freedSeat); }
        else if(p.allocatedBerth.equals("M")) { availableMiddleBerths++; middleBerthsPositions.add(freedSeat); }
        else if(p.allocatedBerth.equals("U")) { availableUpperBerths++; upperBerthsPositions.add(freedSeat); }

        // Step 2: Auto-upgrade RAC to Confirmed!
        if(racList.size() > 0) {
            Passenger passengerFromRAC = passengersDatabase.get(racList.poll()); // Remove from RAC queue
            int racPositionFreed = passengerFromRAC.seatNumber; // Keep track of their RAC seat!
            
            racPositions.add(racPositionFreed);
            availableRacTickets++;

            // Recursively book them into the newly freed Confirmed seat!
            // (Assuming we give them the same berth type that was just cancelled)
            bookTicket(passengerFromRAC, freedSeat, p.allocatedBerth);
            System.out.println("🔼 RAC Passenger " + passengerFromRAC.name + " upgraded to Confirmed!");

            // Step 3: Auto-upgrade WL to the newly freed RAC seat!
            if(waitingList.size() > 0) {
                Passenger passengerFromWL = passengersDatabase.get(waitingList.poll());
                int wlPositionFreed = passengerFromWL.seatNumber;

                waitingListPositions.add(wlPositionFreed);
                availableWaitingList++;

                // Book them into the newly freed RAC seat
                bookTicket(passengerFromWL, racPositionFreed, "RAC");
                System.out.println("🔼 WL Passenger " + passengerFromWL.name + " upgraded to RAC!");
            }
        }
    }

    public void printAvailableSeats() {
        System.out.println("--- AVAILABLE TICKETS ---");
        System.out.println("Lower Berths: " + availableLowerBerths);
        System.out.println("Middle Berths: " + availableMiddleBerths);
        System.out.println("Upper Berths: " + availableUpperBerths);
        System.out.println("RAC Tickets: " + availableRacTickets);
        System.out.println("Waiting List: " + availableWaitingList);
        System.out.println("-------------------------");
    }
}

// ==========================================
// 3. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        TicketBooker booker = new TicketBooker();

        while (true) {
            System.out.println("\n=== IRCTC ZOHO SYSTEM ===");
            System.out.println("1. Book Ticket");
            System.out.println("2. Cancel Ticket");
            System.out.println("3. Print Available Tickets");
            System.out.println("4. Exit");
            System.out.print("Enter choice: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter Name: "); String name = sc.next();
                    System.out.print("Enter Age: "); int age = sc.nextInt();
                    System.out.print("Enter Prefered Berth (L/M/U): "); char berth = sc.next().charAt(0);

                    Passenger p = new Passenger(name, age, berth);

                    // LOGIC: Check availability based on preference OR fallback to anything available
                    if (berth == 'L' && TicketBooker.availableLowerBerths > 0) {
                        booker.bookTicket(p, TicketBooker.lowerBerthsPositions.get(0), "L");
                    } else if (berth == 'M' && TicketBooker.availableMiddleBerths > 0) {
                        booker.bookTicket(p, TicketBooker.middleBerthsPositions.get(0), "M");
                    } else if (berth == 'U' && TicketBooker.availableUpperBerths > 0) {
                        booker.bookTicket(p, TicketBooker.upperBerthsPositions.get(0), "U");
                    } else if (TicketBooker.availableLowerBerths > 0) { // Fallback to L
                        booker.bookTicket(p, TicketBooker.lowerBerthsPositions.get(0), "L");
                    } else if (TicketBooker.availableMiddleBerths > 0) { // Fallback to M
                         booker.bookTicket(p, TicketBooker.middleBerthsPositions.get(0), "M");
                    } else if (TicketBooker.availableUpperBerths > 0) { // Fallback to U
                         booker.bookTicket(p, TicketBooker.upperBerthsPositions.get(0), "U");
                    } else if (TicketBooker.availableRacTickets > 0) { // Fallback to RAC
                        booker.bookTicket(p, TicketBooker.racPositions.get(0), "RAC");
                    } else if (TicketBooker.availableWaitingList > 0) { // Fallback to WL
                        booker.bookTicket(p, TicketBooker.waitingListPositions.get(0), "WL");
                    } else {
                        System.out.println("❌ NO TICKETS AVAILABLE!");
                    }
                    break;
                case 2:
                    System.out.print("Enter Passenger ID to cancel: ");
                    int id = sc.nextInt();
                    booker.cancelTicket(id);
                    break;
                case 3:
                    booker.printAvailableSeats();
                    break;
                case 4:
                    System.out.println("Shutting Down...");
                    System.exit(0);
            }
        }
    }
}
```

---
## 💡 HOW IT WORKS (Interview Explanation)
If the interviewer asks you to explain the cancellation logic:
1.  **Delete the target Passenger** from the `passengersDatabase` Map (O(1) time).
2.  **Add the Seat Number back** into the `lowerBerthsPositions` (or M/U) List so the next guy can take seat #4 instead of leaving it empty.
3.  **Check the RAC Queue:** Using a `Queue` is critical here! `racList.poll()` pulls the person who has been waiting in RAC the longest and deletes them from the physical RAC queue.
4.  **Check the WL Queue:** We do the same `Queue.poll()` logic to promote the longest-waiting person into the newly freed RAC ticket!

*This is the epitome of pure Object-Oriented Logic without relying on MySQL!*
