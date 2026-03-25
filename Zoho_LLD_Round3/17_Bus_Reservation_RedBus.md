# 🚌 17. Bus Reservation System (RedBus)
### Route Generation, Intermediate Stops & Seat Locking 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a long-distance Bus Reservation App (e.g., RedBus / FlixBus).
**Rules:**
1.  **Routes & Stops:** A bus runs on a specific route with multiple sequential stops (e.g., Chennai -> Trichy -> Madurai).
2.  **Partial Route Booking (Crucial Challenge!):** 
    *   The bus has 10 seats.
    *   If User A books Seat 1 from Chennai to Trichy...
    *   ...User B should **STILL** be able to book Seat 1 later for the Trichy to Madurai segment!
3.  **Pricing:** Calculate the ticket price based on how many "stops" the passenger travels through.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

Solving the "Partial booking" puzzle destroys candidates who just map a simple `Boolean[] isOccupied` array for seats. If `isOccupied = true` from Chennai to Trichy, how does the system know it is magically free again at Madurai? 

**The Solution:** We must use a `Map<String, Boolean>` *INSIDE* every single seat!
1.  **`Seat` Class**: Holds an internal HashMap tracking `Segment -> IsBooked` (e.g., "Chen-Tri": true, "Tri-Mad": false).
2.  **`Bus` Class**: Holds a `List<Seat>` and ordered List of Stops.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO: SEAT WITH SEGMENT HASHMAP
// ==========================================
class Seat {
    int seatNumber;
    
    // Tracks the Exact Route Segments!
    // Key: "StopA-StopB" | Value: TRUE if booked, FALSE if free
    Map<String, Boolean> segmentBookings; 

    public Seat(int number, List<String> busStops) {
        this.seatNumber = number;
        this.segmentBookings = new HashMap<>();

        // Initialize all physical road segments to FALSE (Empty)
        // e.g., If stops are [Chennai, Trichy, Madurai]
        // Create -> "Chennai-Trichy": False | "Trichy-Madurai": False
        for (int i = 0; i < busStops.size() - 1; i++) {
            String segment = busStops.get(i) + "-" + busStops.get(i+1);
            segmentBookings.put(segment, false);
        }
    }
}

// ==========================================
// 2. THE CORE LOGIC ENGINE (BUS MANAGER)
// ==========================================
class Bus {
    int busId;
    List<String> routeStops; 
    List<Seat> seats;

    public Bus(int busId, List<String> stops, int totalSeats) {
        this.busId = busId;
        this.routeStops = stops;
        this.seats = new ArrayList<>();

        for (int i = 1; i <= totalSeats; i++) {
            this.seats.add(new Seat(i, stops));
        }
    }

    // --- SEARCH LOGIC ---
    public void displayAvailableSeats(String fromStop, String toStop) {
        int startIndex = routeStops.indexOf(fromStop);
        int endIndex = routeStops.indexOf(toStop);

        if (startIndex == -1 || endIndex == -1 || startIndex >= endIndex) {
            System.out.println("❌ Invalid Route Direction!");
            return;
        }

        // Generate the required list of segments
        // If user wants Chennai to Madurai, segments = ["Chennai-Trichy", "Trichy-Madurai"]
        List<String> requiredSegments = getSegments(startIndex, endIndex);

        System.out.println("\n🔍 Available Seats for " + fromStop + " -> " + toStop + ":");
        boolean anySeatFound = false;

        for (Seat seat : seats) {
            boolean isSeatCompletelyFree = true;

            // Check if THIS specific seat is globally free across ALL required segments
            for (String segment : requiredSegments) {
                if (seat.segmentBookings.get(segment) == true) { // Someone is already in it!
                    isSeatCompletelyFree = false;
                    break; 
                }
            }

            if (isSeatCompletelyFree) {
                System.out.print("[Seat " + seat.seatNumber + "]  ");
                anySeatFound = true;
            }
        }
        if (!anySeatFound) System.out.println("No seats available for this entire stretch. Bus is full!");
        System.out.println();
    }

    // --- BOOKING LOGIC ---
    public void bookSeat(int seatNo, String fromStop, String toStop) {
        int startIndex = routeStops.indexOf(fromStop);
        int endIndex = routeStops.indexOf(toStop);

        if (startIndex == -1 || endIndex == -1 || startIndex >= endIndex) {
            System.out.println("❌ Invalid Route Direction!");
            return;
        }

        List<String> requiredSegments = getSegments(startIndex, endIndex);
        
        // Arrays are 0-indexed, but Seats are 1-indexed (Seat 1 = Index 0)
        Seat targetSeat = seats.get(seatNo - 1);

        // Verification Check First! (ACID Isolation)
        for (String segment : requiredSegments) {
            if (targetSeat.segmentBookings.get(segment) == true) {
                System.out.println("❌ BOOKING FAILED! Seat " + seatNo + " is occupied halfway through that route.");
                return;
            }
        }

        // All segments perfectly free? LOCK THEM!
        for (String segment : requiredSegments) {
            targetSeat.segmentBookings.put(segment, true);
        }

        // Billing: Rs. 150 per intermediate segment
        int cost = requiredSegments.size() * 150;

        System.out.println("✅ TICKET CONFIRMED! Bus #" + busId);
        System.out.println("   Seat: " + seatNo + " | Route: " + fromStop + " -> " + toStop);
        System.out.println("   Final Fare: Rs. " + cost);
    }

    // Mathematical Helper to dynamically string together stops
    private List<String> getSegments(int start, int end) {
        List<String> segments = new ArrayList<>();
        for (int i = start; i < end; i++) {
            segments.add(routeStops.get(i) + "-" + routeStops.get(i+1));
        }
        return segments;
    }
}

// ==========================================
// 3. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Build the Route
        List<String> stops = Arrays.asList("Chennai", "Trichy", "Madurai", "Kanyakumari");
        
        // Deploy Bus with exactly 5 physical seats
        Bus bus = new Bus(99, stops, 5);

        while (true) {
            System.out.println("\n=== REDBUS SIMULATOR ===");
            System.out.println("Route: Chennai -> Trichy -> Madurai -> Kanyakumari");
            System.out.println("1. Find Available Seats");
            System.out.println("2. Book a Seat");
            System.out.println("3. Exit");
            System.out.print("Enter choice: ");
            int option = sc.nextInt();
            sc.nextLine();

            if (option == 1) {
                System.out.print("From City: "); String f = sc.next();
                System.out.print("To City: "); String t = sc.next();
                bus.displayAvailableSeats(f, t);
            } 
            else if (option == 2) {
                System.out.print("From City: "); String f = sc.next();
                System.out.print("To City: "); String t = sc.next();
                System.out.print("Desired Seat Number (1-5): "); int sNo = sc.nextInt();
                bus.bookSeat(sNo, f, t);
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
1. **The Sub-Segment Fracture Logic:** When initialized, the `Bus` automatically fractures the raw string array `[Chennai, Trichy, Madurai]` into specific linked HashMap node keys inside every physical chair: `{"Chennai-Trichy": False, "Trichy-Madurai": False}`. 
2. If User A wants "Chennai to Madurai", the `getSegments()` builder loops between the array indices and stitches both keys together dynamically! It then checks both segments inside that specific seat's HashMap.
3. This completely prevents edge-case corruptions where a long-haul user overwrites a short-haul user's seat midway down the highway!
