# 🛗 18. Lift / Elevator Control System
### Directional Priority and Queue Optimization 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for an Elevator System.
**Rules:**
1.  **Multiple Lifts:** A building has multiple lifts (e.g., 2 Lifts).
2.  **State Management:** An elevator has three directions: `UP`, `DOWN`, and `IDLE`.
3.  **The Algorithm (The Core Challenge!):** 
    *   If a user on Floor 5 presses "UP", the system must find the *nearest* elevator that is either `IDLE` or already moving `UP` towards Floor 5.
    *   If a lift is on Floor 8 moving `UP`, it *cannot* service a request on Floor 5!
    *   If no lifts are available in the right direction, the request is added to a Pending Queue.
4.  **Movement:** Lifts process one floor at a time in a loop until their target queue is empty.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Direction` Enum**: `UP, DOWN, IDLE`.
2.  **`Request` Class**: A POJO storing the `sourceFloor` and `destinationFloor`.
3.  **`Elevator` Class**: Stores its `currentFloor`, `Direction`, and a `PriorityQueue` of floors it needs to stop at (sorted dynamically based on whether it is moving up or down).
4.  **`ElevatorController` Class**: The active dispatcher that receives a user's button press and decides *which* of the 2 Elevators is mathematically best suited to take the job.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO & ENUMS
// ==========================================
enum Direction { UP, DOWN, IDLE }

class Request {
    int source;
    int destination;
    Direction requestedDirection;

    public Request(int source, int dest) {
        this.source = source;
        this.destination = dest;
        this.requestedDirection = (dest > source) ? Direction.UP : Direction.DOWN;
    }
}

// ==========================================
// 2. THE ELEVATOR CAR
// ==========================================
class Elevator {
    int liftId;
    int currentFloor;
    Direction currentDirection;
    
    // Using a TreeSet to automatically sort requested floors in Min-Max order 
    TreeSet<Integer> upServiceStops;
    TreeSet<Integer> downServiceStops;

    public Elevator(int id) {
        this.liftId = id;
        this.currentFloor = 0; // Starts at Ground Floor
        this.currentDirection = Direction.IDLE;
        
        this.upServiceStops = new TreeSet<>(); // Automatically sorts 1, 3, 5
        this.downServiceStops = new TreeSet<>(Collections.reverseOrder()); // Sorts 5, 3, 1!
    }

    public void addFloorToSchedule(Request req) {
        // We must stop at BOTH the source (to pick them up) AND the destination (to drop them off)
        if (req.requestedDirection == Direction.UP) {
            upServiceStops.add(req.source);
            upServiceStops.add(req.destination);
        } else {
            downServiceStops.add(req.source);
            downServiceStops.add(req.destination);
        }

        // Wake up the lift if it was sleeping!
        if (currentDirection == Direction.IDLE) {
            currentDirection = req.requestedDirection;
        }
    }

    // Move the physical lift by 1 step every "tick"
    public void moveOneStep() {
        if (currentDirection == Direction.UP) {
            // Find the lowest number in the Up Queue
            if (!upServiceStops.isEmpty()) {
                int nextTarget = upServiceStops.first();
                if (currentFloor < nextTarget) {
                    currentFloor++; // Move up one physical floor
                    System.out.println("🛗 Lift " + liftId + " moving UP to floor " + currentFloor);
                }
                if (currentFloor == nextTarget) {
                    System.out.println("✅ Lift " + liftId + " STOPPED at floor " + currentFloor + " (Opening Doors...)");
                    upServiceStops.remove(nextTarget); // Clear stop
                } 
            } else {
                // Done going up. Change direction if Down jobs exist, else IDLE.
                currentDirection = downServiceStops.isEmpty() ? Direction.IDLE : Direction.DOWN;
            }
        } 
        else if (currentDirection == Direction.DOWN) {
            // Find the highest number in the Down Queue (using the reverse sorted TreeSet!)
            if (!downServiceStops.isEmpty()) {
                int nextTarget = downServiceStops.first();
                if (currentFloor > nextTarget) {
                    currentFloor--; // Move down one physical floor
                    System.out.println("🛗 Lift " + liftId + " moving DOWN to floor " + currentFloor);
                }
                if (currentFloor == nextTarget) {
                    System.out.println("✅ Lift " + liftId + " STOPPED at floor " + currentFloor + " (Opening Doors...)");
                    downServiceStops.remove(nextTarget); // Clear stop
                }
            } else {
                 currentDirection = upServiceStops.isEmpty() ? Direction.IDLE : Direction.UP;
            }
        }
    }
}

// ==========================================
// 3. THE DISPATCHER (CONTROLLER LOGIC)
// ==========================================
class ElevatorController {

    List<Elevator> lifts;

    public ElevatorController() {
        lifts = new ArrayList<>();
        lifts.add(new Elevator(1)); // Build Lift 1
        lifts.add(new Elevator(2)); // Build Lift 2
    }

    // ALGORITHM: Find the most efficient lift to dispatch!
    public void handleRequest(Request req) {
        Elevator bestLift = null;
        int minDistance = Integer.MAX_VALUE;

        for (Elevator lift : lifts) {
            if (lift.currentDirection == Direction.IDLE) {
                // Lift is completely free! See how far away it is.
                int distance = Math.abs(lift.currentFloor - req.source);
                if (distance < minDistance) {
                    minDistance = distance;
                    bestLift = lift;
                }
            } 
            else if (lift.currentDirection == req.requestedDirection) {
                // Lift is moving the exact same way the passenger wants to go!
                // But is it moving TOWARDS the passenger, or has it already passed them?
                if (req.requestedDirection == Direction.UP && req.source >= lift.currentFloor) {
                    int distance = req.source - lift.currentFloor;
                    if (distance < minDistance) {
                        minDistance = distance;
                        bestLift = lift;
                    }
                } 
                else if (req.requestedDirection == Direction.DOWN && req.source <= lift.currentFloor) {
                    int distance = lift.currentFloor - req.source;
                    if (distance < minDistance) {
                        minDistance = distance;
                        bestLift = lift;
                    }
                }
            }
        }

        if (bestLift != null) {
            System.out.println("📡 Dispatcher: Assigned Lift " + bestLift.liftId + " (Currently at Floor " + bestLift.currentFloor + ") to pick up passenger at Floor " + req.source);
            bestLift.addFloorToSchedule(req);
        } else {
            System.out.println("📡 Dispatcher: All lifts are busy moving in the opposite direction! Ignoring request for now (In a real app, send to a pending Loop Queue).");
        }
    }

    // Triggers all lifts to move by exactly 1 floor physically
    public void pushTimeForward() {
        System.out.println("\n--- ⏰ TIME TICK ---");
        boolean anyLiftMoved = false;
        for (Elevator lift : lifts) {
            if (lift.currentDirection != Direction.IDLE) {
                lift.moveOneStep();
                anyLiftMoved = true;
            }
        }
        if(!anyLiftMoved) System.out.println("zzz... Lifts are currently IDLE.");
    }
}

// ==========================================
// 4. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ElevatorController app = new ElevatorController();

        System.out.println("=== ZOHO TOWER SIMULATOR ===");
        System.out.println("2 Lifts actively waiting at Ground Floor (0).");

        while (true) {
            System.out.println("\n1. Press Call Button (e.g., Ground to Floor 5)");
            System.out.println("2. Push Time Forward (Watch Lifts Move!)");
            System.out.println("3. Exit");
            System.out.print("Action: ");
            int option = sc.nextInt();

            if (option == 1) {
                System.out.print("Enter your current Floor: "); int source = sc.nextInt();
                System.out.print("Enter Destination Floor: "); int dest = sc.nextInt();
                app.handleRequest(new Request(source, dest));
            } 
            else if (option == 2) {
                app.pushTimeForward();
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
1. **The Look-Algorithm (Disk Scheduling Simulation):** Lifts don't process jobs chronologically (`First Come First Serve`). If First = Floor 10, Second = Floor 2, Third = Floor 8... the lift would wildly bounce up and down! Lifts actually use the "Elevator/Look Algorithm". 
    *   By adding all requested stops into a `TreeSet<Integer>`, Java automatically mathematically sorts them in ascending order (`1, 2, 5, 8`). The lift hits them in perfect sequence!
2. **Reverse Ordered Trees:** When going `DOWN`, you need the lift to hit `8, 5, 2, 1`. Notice how I initialized `downServiceStops = new TreeSet<>(Collections.reverseOrder())`. This forces the Tree to sort highest-to-lowest, requiring ZERO sorting math loops at runtime!
3. **Dispatcher Distance Math:** The dispatcher calculates `Math.abs(liftFloor - reqSource)`. It strictly filters out lifts that have physically *passed* the passenger's floor (`req.source >= lift.currentFloor`), ensuring the passenger isn't left stranted.
