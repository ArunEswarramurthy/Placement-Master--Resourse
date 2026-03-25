# 🏨 11. Hotel Booking System
### Room Categories, Check-in/Check-out & Date Overlaps 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Hotel Reservation System (Like OYO/Agoda).
**Rules:**
1.  **Rooms:** A hotel has two categories of rooms: `STANDARD` (Rs. 2000/day) and `DELUXE` (Rs. 4000/day).
2.  **Booking Logic:** A user can request to book a specific room type for a contiguous date range (e.g., Dates 10 to 15).
3.  **Overlap Prevention (Crucial!):** The system must search the rooms and ensure the requested dates do NOT clash with any existing bookings for that specific physical room.
4.  **Check-out:** Automatically calculate the total bill based on the actual number of days stayed.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Booking` Class**: Represents a locked time block (Start Date, End Date).
2.  **`Room` Class**: Represents a physical room number (e.g., 101). Contains a `List<Booking>` containing all its future reserved date blocks.
3.  **`HotelManager` Class**: Contains the logic to loop through rooms, check for date clashes, and generate the final bill.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. ENUMS & POJO: BOOKING TIME BLOCK
// ==========================================
enum RoomType { STANDARD, DELUXE }

class Booking {
    static int idProvider = 5000;
    
    int bookingId;
    String guestName;
    int startDate; // Using integers 1-365 for simplicity instead of Java Dates
    int endDate;
    Room assignedRoom;

    public Booking(String guestName, int start, int end, Room room) {
        this.bookingId = idProvider++;
        this.guestName = guestName;
        this.startDate = start;
        this.endDate = end;
        this.assignedRoom = room;
    }
}

// ==========================================
// 2. POJO: SPECIFIC HOTEL ROOM
// ==========================================
class Room {
    int roomNumber;
    RoomType type;
    int pricePerNight;
    
    // Tracks ALL future bookings for this exact physical room
    List<Booking> schedule; 

    public Room(int roomNumber, RoomType type, int price) {
        this.roomNumber = roomNumber;
        this.type = type;
        this.pricePerNight = price;
        this.schedule = new ArrayList<>();
    }

    // THE MAGIC OVERLAP DETECTOR
    public boolean isAvailable(int requestedStart, int requestedEnd) {
        for (Booking existingBooking : schedule) {
            // Overlap logic: If (New_Start < Old_End AND New_End > Old_Start) -> IT CLASHES!
            if (requestedStart < existingBooking.endDate && requestedEnd > existingBooking.startDate) {
                return false; // Clashes with an existing booking!
            }
        }
        return true; // No clashes found, room is safe to book!
    }
}

// ==========================================
// 3. THE CORE LOGIC ENGINE (HOTEL MANAGER)
// ==========================================
class HotelManager {

    List<Room> allRooms;
    Map<Integer, Booking> activeBookingsDB;

    public HotelManager() {
        allRooms = new ArrayList<>();
        activeBookingsDB = new HashMap<>();

        // Initialize Hotel: 3 Standard, 2 Deluxe
        allRooms.add(new Room(101, RoomType.STANDARD, 2000));
        allRooms.add(new Room(102, RoomType.STANDARD, 2000));
        allRooms.add(new Room(103, RoomType.STANDARD, 2000));
        allRooms.add(new Room(201, RoomType.DELUXE, 4000));
        allRooms.add(new Room(202, RoomType.DELUXE, 4000));
    }

    // --- BOOKING LOGIC ---
    public void searchAndBookRoom(String guestName, RoomType requestedType, int reqStart, int reqEnd) {
        if (reqStart >= reqEnd) {
            System.out.println("❌ Invalid Dates! End date must be after Start date.");
            return;
        }

        Room bestRoom = null;

        // 1. Loop through all rooms looking for the correct Type AND Availability
        for (Room room : allRooms) {
            if (room.type == requestedType) {
                if (room.isAvailable(reqStart, reqEnd)) {
                    bestRoom = room; // Found an empty room!
                    break; 
                }
            }
        }

        if (bestRoom == null) {
            System.out.println("❌ SOLD OUT! No " + requestedType + " rooms available for Dates " + reqStart + " to " + reqEnd);
            return;
        }

        // 2. Lock the room!
        Booking newBooking = new Booking(guestName, reqStart, reqEnd, bestRoom);
        bestRoom.schedule.add(newBooking); // Add to room's physical calendar
        activeBookingsDB.put(newBooking.bookingId, newBooking); // Add to System DB

        int totalDays = reqEnd - reqStart;
        double estimatedPrice = totalDays * bestRoom.pricePerNight;

        System.out.println("✅ BOOKING CONFIRMED!");
        System.out.println("   Guest: " + guestName + " | Booking ID: #" + newBooking.bookingId);
        System.out.println("   Assigned Room: " + bestRoom.roomNumber + " (" + bestRoom.type + ")");
        System.out.println("   Est. Bill for " + totalDays + " nights: Rs. " + estimatedPrice);
    }

    // --- CHECKOUT LOGIC ---
    public void checkout(int bookingId) {
        if (!activeBookingsDB.containsKey(bookingId)) {
            System.out.println("❌ Invalid Booking ID!");
            return;
        }

        Booking b = activeBookingsDB.get(bookingId);
        Room r = b.assignedRoom;

        int totalDays = b.endDate - b.startDate;
        double finalBill = totalDays * r.pricePerNight;

        // Free up the room's calendar historical block (optional, but good for keeping lists small)
        r.schedule.remove(b);
        activeBookingsDB.remove(bookingId);

        System.out.println("✅ CHECKOUT SUCCESSFUL! Room " + r.roomNumber + " is now clean and available.");
        System.out.println("💳 Please collect payment of Rs. " + finalBill + " from " + b.guestName);
    }
    
    public void viewHotelStatus() {
        System.out.println("\n--- HOTEL ROOM STATUS ---");
        for(Room r : allRooms) {
             System.out.print("Room " + r.roomNumber + " (" + r.type + ") -> Reserved Dates: ");
             if(r.schedule.isEmpty()) System.out.print("Completely Free");
             for(Booking b : r.schedule) {
                 System.out.print("[" + b.startDate + " to " + b.endDate + "] ");
             }
             System.out.println();
        }
    }
}

// ==========================================
// 4. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        HotelManager app = new HotelManager();

        while (true) {
            System.out.println("\n=== OYO HOTEL MANAGER ===");
            System.out.println("1. Book a Room");
            System.out.println("2. Checkout (Generate Bill)");
            System.out.println("3. View Hotel Calendar Status");
            System.out.println("4. Exit");
            System.out.print("Enter choice: ");
            int option = sc.nextInt();

            if (option == 1) {
                System.out.print("Enter Guest Name: "); String name = sc.next();
                System.out.print("Room Type (1 for Standard, 2 for Deluxe): "); int t = sc.nextInt();
                System.out.print("Enter Start Date (1-365): "); int start = sc.nextInt();
                System.out.print("Enter End Date (1-365): "); int end = sc.nextInt();
                
                RoomType type = (t == 1) ? RoomType.STANDARD : RoomType.DELUXE;
                app.searchAndBookRoom(name, type, start, end);
            } 
            else if (option == 2) {
                System.out.print("Enter Booking ID: ");
                int bId = sc.nextInt();
                app.checkout(bId);
            } 
            else if (option == 3) {
                 app.viewHotelStatus();
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
1. **The Overlap Algorithm:** The most famous logic puzzle in Hotel Systems is date clashing. If someone booked days `10 to 15`. Can someone book `14 to 20`? 
    *   The formula `(New_Start < Old_End AND New_End > Old_Start)` detects this! 
    *   Is `14 < 15`? Yes! AND is `20 > 10`? Yes! It instantly trips the alarm and blocks the booking!
2. **Infinite Future Scaling:** Because we mapped an `ArrayList<Booking>` inside *every specific room*, Room 101 can safely track 50 completely different future bookings scattered throughout the year without complex multi-dimensional boolean arrays!
