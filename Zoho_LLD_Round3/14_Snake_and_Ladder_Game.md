# 🐍 14. Snake and Ladder Game Engine
### Board Grids, Portals, and Turn Simulation 🚀

---

## 📌 PROBLEM STATEMENT

Build a fully functioning text-based Snake and Ladder Game Simulator.
**Rules:**
1.  **Board Space:** The board runs from `1 to 100`.
2.  **Players:** Multiple players can play (N players). They all start strictly at position 0.
3.  **Portals (Snakes & Ladders):**
    *   *Ladder:* If you land exactly on `Start_Square`, you instantly jump to `End_Square` (where End > Start).
    *   *Snake:* If you land exactly on the Snake's head `Start_Square`, you instantly fall to the tail `End_Square` (where End < Start).
4.  **Win Condition:** The first player to reach EXACTLY square 100 wins!
5.  **Dice Roll Limit:** A standard dice rolls random numbers from 1 to 6. If the player is on square 98, and rolls a 4, they stay at 98 (they must roll exactly 2).

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Player` Class**: Holds `id`, `name`, and `currentPosition` (Starts at 0).
2.  **`Portal` Class**: (Represents both Snakes and Ladders). Holds `startPosition` and `endPosition`.
3.  **`Board` Class**: Holds a `HashMap<Integer, Portal>` mapping the specific trigger squares to their physical portals.
4.  **`GameEngine` Class**: Loops sequentially through an `ArrayDeque<Player>` forcing them to roll the dice one-by-one.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO: PLAYERS AND PORTALS
// ==========================================
class Player {
    String name;
    int currentPosition;

    public Player(String name) {
        this.name = name;
        this.currentPosition = 0; // Everyone starts off the board at 0
    }
}

class Portal {
    int start;
    int end;

    public Portal(int start, int end) {
        this.start = start;
        this.end = end;
    }
    
    // Distinguish type for the console printout
    public String getType() {
        return (end > start) ? "LADDER ⬆️" : "SNAKE ⬇️";
    }
}

// ==========================================
// 2. POJO: THE PHYSICAL BOARD (1-100)
// ==========================================
class Board {
    int size;
    // Maps the exact triggering square to the Portal object
    Map<Integer, Portal> portalsOnBoard; 

    public Board(int size) {
        this.size = size;
        this.portalsOnBoard = new HashMap<>();
    }

    public void addSnakeOrLadder(int start, int end) {
        // You cannot place a Snake head and a Ladder bottom on the exact same square!
        if (portalsOnBoard.containsKey(start)) {
            System.out.println("❌ Square " + start + " already has a portal!");
            return;
        }
        portalsOnBoard.put(start, new Portal(start, end));
    }
}

// ==========================================
// 3. THE CORE LOGIC ENGINE (GAME SIMULATOR)
// ==========================================
class GameEngine {

    Board board;
    Queue<Player> turnQueue; // Using a Queue naturally forces turn-by-turn logic!
    Random dice; // Used to simulate physical dice rolls

    public GameEngine(Board board) {
        this.board = board;
        this.turnQueue = new LinkedList<>();
        this.dice = new Random();
    }

    public void addPlayer(String name) {
        turnQueue.add(new Player(name));
    }

    // Mathematical Dice Roller
    private int rollDice() {
        return dice.nextInt(6) + 1; // Generates 1 to 6
    }

    public void startGameLoop() {
        System.out.println("🎮 Tossing the dice! Game is starting...\n");

        while (true) {
            // 1. Pop the player whose turn it is
            Player currentPlayer = turnQueue.poll();
            
            // 2. Roll Dice
            int diceValue = rollDice();
            int attemptedNextPosition = currentPlayer.currentPosition + diceValue;

            System.out.print("🎲 " + currentPlayer.name + " rolled a " + diceValue);
            
            // 3. Boundary Check (100)
            if (attemptedNextPosition > board.size) {
                 System.out.println(" -> But needs exactly " + (board.size - currentPlayer.currentPosition) + " to win! Stayed at " + currentPlayer.currentPosition);
                 turnQueue.add(currentPlayer); // Put back to end of queue
                 continue;
            }
            
            // 4. Move them physically
            currentPlayer.currentPosition = attemptedNextPosition;
            System.out.print(" -> Landed on " + currentPlayer.currentPosition);

            // 5. Portal Check (Did they land on a Snake or Ladder?)
            if (board.portalsOnBoard.containsKey(currentPlayer.currentPosition)) {
                Portal p = board.portalsOnBoard.get(currentPlayer.currentPosition);
                currentPlayer.currentPosition = p.end; // Teleport!
                System.out.print(" [" + p.getType() + " Triggered!] Teleported to " + currentPlayer.currentPosition);
            }
            System.out.println(); // Line break

            // 6. Win Condition!
            if (currentPlayer.currentPosition == board.size) {
                System.out.println("\n🎉🎉🎉 " + currentPlayer.name + " HAS WON THE GAME! 🎉🎉🎉");
                break; // Ends the infinite loop!
            }

            // 7. Push them back to the end of the line for the next round
            turnQueue.add(currentPlayer);
            
            // Artificial delay so the console prints readably 
            // (Remove this during real execution if running tests)
            try { Thread.sleep(500); } catch (Exception e) {} 
        }
    }
}

// ==========================================
// 4. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        // Setup Board Matrix (1 to 100)
        Board b = new Board(100);

        // Map the Ladders (Start < End)
        b.addSnakeOrLadder(2, 38);
        b.addSnakeOrLadder(9, 31);
        b.addSnakeOrLadder(21, 42);
        b.addSnakeOrLadder(28, 84);
        b.addSnakeOrLadder(51, 67);

        // Map the Snakes (Start > End)
        b.addSnakeOrLadder(17, 7);
        b.addSnakeOrLadder(54, 34);
        b.addSnakeOrLadder(62, 19);
        b.addSnakeOrLadder(87, 24);
        b.addSnakeOrLadder(98, 79);

        // Inject dependencies into the Game Engine
        GameEngine engine = new GameEngine(b);
        engine.addPlayer("Alice");
        engine.addPlayer("Bob");

        // Ignite!
        engine.startGameLoop();
    }
}
```

---
## 💡 HOW IT WORKS (Interview Explanation)
1. **The Game Loop Hack:** Writing `while(!gameOver)` logic for 4 players is exhausting using arrays and index tracking (`playerIndex++`). By throwing all players into a `Queue<Player>`, you literally `poll()` them, roll their dice, and if they don't win, `add()` them directly back to the rear of the Queue! Infinite, structurally perfect Turn Sequences completely for free!
2. **Abstracting the Portals:** Why make a `Snake` class and a `Ladder` class? Snakes and Ladders are the exact same physical mechanism (a teleporter). A `Portal` with a `start` and `end` handles both simultaneously, and the method `end > start` verifies which one it was purely for aesthetic printing. Object-Oriented polymorphism and inheritance aren't necessary if the mathematical root is identical.
3. **Trigger Lookups in O(1):** We mapped `Integer -> Portal`. When a player lands on `28`, instead of looping through all ladders on the board, `portalsOnBoard.containsKey(28)` executes instantly in O(1) hash math. It grabs the connected portal and overrides `currentPlayer.currentPosition`.
