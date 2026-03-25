# 🎟️ 12. Movie Reservation System (BookMyShow)
### Seating Grids, Showtimes, and Concurrency Locks 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Movie Ticket Booking App like BookMyShow.
**Rules:**
1.  **Multiple Theaters:** The system has multiple Theaters.
2.  **Screens & Shows:** Each theater has multiple Screens. Each Screen plays different Shows at different timings.
3.  **Seating:** A Screen has a grid of seats (e.g., Row A-E, Cols 1-10). Some are Premium, some are Regular.
4.  **Booking Logic (The Challenge):** When a user requests to book `Row A, Seat 1`, the system must check if that *exact seat* is available for that *exact showtime*. If yes, lock it and generate a Ticket.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Seat` Class**: Represents a physical chair. Contains `row`, `col`, `isReserved`.
2.  **`Show` Class**: Represents a specific movie screening (e.g., "Batman at 6PM"). The Show MUST contain its own independent 2D Array / Grid of `Seat` objects!
3.  **`Theater` Class**: Houses a `List<Show>`.
4.  **`BookMyShowManager` Class**: The search and selection engine.

*(Note: We will simplify this to 1 Theater and 1 Show for interview brevity, focusing purely on the Seat Grid Locking mechanics).*

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO: SEAT & TICKET
// ==========================================
class Seat {
    String seatId; // e.g., "A1"
    int price;
    boolean isReserved;

    public Seat(String seatId, int price) {
        this.seatId = seatId;
        this.price = price;
        this.isReserved = false;
    }
}

class Ticket {
    static int idProvider = 8800;
    
    int ticketId;
    String movieName;
    String time;
    List<Seat> bookedSeats;
    int totalAmount;

    public Ticket(String movieName, String time, List<Seat> lockedSeats) {
        this.ticketId = idProvider++;
        this.movieName = movieName;
        this.time = time;
        this.bookedSeats = new ArrayList<>(lockedSeats);
        
        for (Seat s : lockedSeats) {
            this.totalAmount += s.price;
        }
    }
}

// ==========================================
// 2. POJO: SHOW (Contains the 2D Physics)
// ==========================================
class Show {
    String showId;
    String movieName;
    String timing;
    
    // Seat ID -> PHYSICAL SEAT OBJECT. 
    // This Map represents the Layout of the specific theater room!
    Map<String, Seat> seatLayout; 

    public Show(String showId, String movieName, String timing) {
        this.showId = showId;
        this.movieName = movieName;
        this.timing = timing;
        this.seatLayout = new LinkedHashMap<>();

        // Generate a Theater layout (Rows A, B, C | 5 seats per row)
        // Row A is Premium (Rs. 200), B & C are Regular (Rs. 100)
        char[] rows = {'A', 'B', 'C'};
        for (char row : rows) {
            for (int col = 1; col <= 5; col++) {
                String sId = "" + row + col;
                int price = (row == 'A') ? 200 : 100;
                seatLayout.put(sId, new Seat(sId, price));
            }
        }
    }

    public void displaySeatingArrangement() {
        System.out.println("\n--- SCREEN LAYOUT ---");
        int count = 0;
        for (Seat s : seatLayout.values()) {
            if (s.isReserved) {
                System.out.print("[ X ] "); // X means booked!
            } else {
                System.out.print("[" + s.seatId + "] ");
            }
            
            count++;
            if (count % 5 == 0) System.out.println(); // Line break after 5 cols
        }
        System.out.println("---------------------\n");
    }
}

// ==========================================
// 3. THE CORE LOGIC ENGINE (BOOK_MY_SHOW MANAGER)
// ==========================================
class BookMyShowManager {

    Map<String, Show> activeShows;

    public BookMyShowManager() {
        activeShows = new HashMap<>();
        // Set up the daily movie schedule
        activeShows.put("S1", new Show("S1", "Batman", "18:00"));
        activeShows.put("S2", new Show("S2", "Spiderman", "21:00"));
    }

    // --- BOOKING LOGIC ---
    public void bookSeats(String showId, List<String> requestedSeatIds) {
        if (!activeShows.containsKey(showId)) {
            System.out.println("❌ Invalid Show ID.");
            return;
        }

        Show show = activeShows.get(showId);

        // 1. Transaction Simulation Locks
        // We must check ALL seats first. If even 1 fails, we reject the whole transaction!
        List<Seat> verifiedSeatsToLock = new ArrayList<>();

        for (String requestedId : requestedSeatIds) {
            if (!show.seatLayout.containsKey(requestedId)) {
                System.out.println("❌ Error: Seat " + requestedId + " does not exist in this screen layout.");
                return;
            }

            Seat physicalSeat = show.seatLayout.get(requestedId);

            if (physicalSeat.isReserved) {
                System.out.println("❌ Error: Seat " + requestedId + " was already booked by someone else!");
                return; // Entire transaction gets cancelled
            }

            verifiedSeatsToLock.add(physicalSeat); // Validated! Add to holding array.
        }

        // 2. Commit the Transaction! Everything verified.
        for (Seat s : verifiedSeatsToLock) {
            s.isReserved = true; // Permanently lock
        }

        Ticket t = new Ticket(show.movieName, show.timing, verifiedSeatsToLock);

        System.out.println("✅ PAYMENT SUCCESSFUL! Transaction Complete.");
        System.out.println("🎟️ Ticket ID: #" + t.ticketId);
        System.out.println("   Movie: " + t.movieName + " at " + t.timing);
        System.out.print("   Seats: ");
        for (Seat s : t.bookedSeats) System.out.print(s.seatId + " ");
        System.out.println("\n   Total Bill: Rs. " + t.totalAmount);
    }

    public void displayMovies() {
        System.out.println("\n--- TODAY'S SHOWS ---");
        for (Show s : activeShows.values()) {
            System.out.println("ID: " + s.showId + " | Movie: " + s.movieName + " | Time: " + s.timing);
        }
    }
}

// ==========================================
// 4. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        BookMyShowManager bms = new BookMyShowManager();

        while (true) {
            System.out.println("\n=== BOOK-MY-SHOW ===");
            System.out.println("1. View Shows");
            System.out.println("2. View Seating Layout");
            System.out.println("3. Book Tickets");
            System.out.println("4. Exit");
            System.out.print("Enter choice: ");
            int option = sc.nextInt();
            sc.nextLine();

            if (option == 1) {
                bms.displayMovies();
            } 
            else if (option == 2) {
                System.out.print("Enter Show ID (e.g., S1): ");
                String sh = sc.nextLine();
                if (bms.activeShows.containsKey(sh)) {
                    bms.activeShows.get(sh).displaySeatingArrangement();
                } else {
                    System.out.println("Invalid ID.");
                }
            } 
            else if (option == 3) {
                 System.out.print("Enter Show ID: ");
                 String sh = sc.nextLine();
                 System.out.print("Enter Comma-Separated Seats (e.g., A1,A2,B5): ");
                 String seatStr = sc.nextLine();
                 
                 // Clean string and convert "A1,A2" -> ["A1", "A2"]
                 List<String> list = Arrays.asList(seatStr.split("\\s*,\\s*"));
                 bms.bookSeats(sh, list);
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
1. **Scope of the Map Phase:** The most common mistake candidates make is attaching the `List<Seat>` to the *Theater*. But what if the 6PM show is completely sold out, but the 9PM show is empty? The `SeatLayout Map` MUST belong to the `Show` object, NOT the building! Thus, every `Show` generates its own independent clean physics grid of chairs upon initialization.
2. **ACID Transaction Emulation:** When a user books "A1, A2, A3", we do **NOT** flip `isReserved = true` immediately inside the loop. If A1 and A2 are free, but A3 is taken, and we flipped A1 and A2 inside the loop prematurely... we just stole A1 and A2 and broke the application! We loop through everything first, add safe seats to a temporary `verifiedSeatsToLock` list, and only run the lock loop once we guarantee 100% of the required seats are free. This is exactly how SQL transaction isolation (`COMMIT` vs `ROLLBACK`) works under the hood.
