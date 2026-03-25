# 🏏 16. Cricket Scoreboard System
### Overs, Deliveries, Wickets & Strike Rotation 🚀

---

## 📌 PROBLEM STATEMENT

Build a backend logic for a Cricket Match Scoreboard tracker (like ESPNcricinfo).
**Rules:**
1.  **Players:** Maintain data for two Batsmen (Striker and Non-Striker) and a Bowler.
2.  **Deliveries (Balls):** The user inputs the result of a ball: `0, 1, 2, 3, 4, 6, W (Wicket), Wd (Wide), Nb (No Ball)`.
3.  **Strike Rotation (Crucial Logic):** 
    *   If a batsman scores 1 or 3 runs, the Striker and Non-Striker swap places instantly.
    *   If an Over finishes (6 valid balls), the Striker and Non-Striker swap places!
4.  **Extras:** Wides and No-Balls do NOT count towards the 6-ball Over limit, but they DO add exactly 1 free run to the Team's Total Score!
5.  **Output:** Live printing of the Score, Overs completed, and Individual Batsman stats.

---

## 🏗️ SYSTEM DESIGN (The Architecture)

1.  **`Player` Class**: Stores name, `runsScored`, `ballsFaced`, `fours`, `sixes`, and `isOut`.
2.  **`Team` Class**: Stores the List of Players, total score, total wickets, and total valid balls bowled.
3.  **`MatchManager` Class**: Handles the algorithmic Strike Rotation parsing and extra-ball counting.

---

## 💻 COMPLETE JAVA IMPLEMENTATION

```java
import java.util.*;

// ==========================================
// 1. POJO: CRICKET PLAYER
// ==========================================
class Player {
    String name;
    int runsScored;
    int ballsFaced;
    int fours;
    int sixes;
    boolean isOut;

    public Player(String name) {
        this.name = name;
        this.runsScored = 0;
        this.ballsFaced = 0;
        this.fours = 0;
        this.sixes = 0;
        this.isOut = false;
    }

    public void addRuns(int runs) {
        this.runsScored += runs;
        this.ballsFaced++;
        if (runs == 4) fours++;
        if (runs == 6) sixes++;
    }
}

// ==========================================
// 2. THE CORE LOGIC ENGINE (SCOREBOARD)
// ==========================================
class MatchManager {

    // Team Level Stats
    String teamName;
    int totalTeamRuns;
    int totalWickets;
    int totalValidBalls;
    
    // Active Pitch Positions
    Player striker;
    Player nonStriker;
    
    // Database
    List<Player> battingLineup;
    int nextBatsmanIndex; 

    public MatchManager() {
        teamName = "India";
        totalTeamRuns = 0;
        totalWickets = 0;
        totalValidBalls = 0;

        // Init 11 players
        battingLineup = new ArrayList<>();
        battingLineup.add(new Player("Rohit Sharma"));
        battingLineup.add(new Player("Virat Kohli"));
        battingLineup.add(new Player("MS Dhoni"));
        battingLineup.add(new Player("Suryakumar Yadav"));

        // Setup the physical pitch with Openers
        striker = battingLineup.get(0);
        nonStriker = battingLineup.get(1);
        nextBatsmanIndex = 2; // Next man in!
    }

    // --- PHYSICS: STRIKE ROTATION ---
    private void rotateStrike() {
        Player temp = striker;
        striker = nonStriker;
        nonStriker = temp;
    }

    // --- MAIN BALL PROCESSING LOGIC ---
    public void processDelivery(String input) {
        // Is it the end of the inning?
        if (totalWickets == 10) {
            System.out.println("❌ Innings Over! All out.");
            return;
        }

        // 1. Handle Extras (Nb or Wd)
        if (input.equalsIgnoreCase("Wd") || input.equalsIgnoreCase("Nb")) {
            totalTeamRuns += 1; // Free run for team!
            // Note: Does NOT increment `totalValidBalls`
            System.out.println("⚠️ EXTRA BALL! +1 Run to Team.");
            return;
        }

        // 2. Handle Wickets (W)
        if (input.equalsIgnoreCase("W")) {
            striker.isOut = true;
            striker.ballsFaced++; // It counts as a ball faced!
            totalWickets++;
            totalValidBalls++;
            
            System.out.println("💥 WICKET! " + striker.name + " is OUT!");

            // Send new batsman to crease
            if (nextBatsmanIndex < battingLineup.size()) {
                striker = battingLineup.get(nextBatsmanIndex);
                nextBatsmanIndex++;
            }
        } 
        
        // 3. Handle Normal Runs (0, 1, 2, 3, 4, 6)
        else {
            try {
                int runs = Integer.parseInt(input);
                totalTeamRuns += runs;
                totalValidBalls++;
                
                // Add to individual batsman stats
                striker.addRuns(runs);

                // Strike rotation immediately on odd runs
                if (runs == 1 || runs == 3) {
                    rotateStrike();
                }
            } catch (Exception e) {
                System.out.println("❌ Invalid Input!");
                return;
            }
        }

        // 4. Over Completion Check
        // If 6 completely valid balls have been bowled, the over is done.
        if (totalValidBalls > 0 && totalValidBalls % 6 == 0) {
            System.out.println("🔁 OVER COMPLETED!");
            rotateStrike(); // Swap sides of the pitch!
        }
    }

    // --- UI DISPLAY ---
    public void displayScore() {
        int overs = totalValidBalls / 6;
        int ballsInCurrentOver = totalValidBalls % 6;
        
        System.out.println("\n=================================");
        System.out.println("🏏 TEAM SCORE: " + teamName + " - " + totalTeamRuns + "/" + totalWickets);
        System.out.println("⏱️  OVERS: " + overs + "." + ballsInCurrentOver);
        System.out.println("---------------------------------");
        System.out.println("👉 STRIKER:    " + striker.name + "   " + striker.runsScored + " (" + striker.ballsFaced + ")  [4s:" + striker.fours + ", 6s:" + striker.sixes + "]");
        System.out.println("   NON-STRIKER: " + nonStriker.name + "   " + nonStriker.runsScored + " (" + nonStriker.ballsFaced + ")  [4s:" + nonStriker.fours + ", 6s:" + nonStriker.sixes + "]");
        System.out.println("=================================\n");
    }
}

// ==========================================
// 3. MAIN (CLI INTERFACE)
// ==========================================
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        MatchManager app = new MatchManager();

        System.out.println("=== LIVE CRICKET SCOREBOARD TERMINAL ===");
        System.out.println("Instructions: Type 0, 1, 2, 4, 6 for runs.");
        System.out.println("Type 'W' for Wicket, 'Wd' for Wide, 'Nb' for No-Ball.");
        
        app.displayScore();

        while (true) {
            System.out.print("Enter Ball Outcome (or 'exit'): ");
            String input = sc.next();
            
            if (input.equalsIgnoreCase("exit")) break;
            
            app.processDelivery(input);
            app.displayScore();
        }
    }
}
```

---
## 💡 HOW IT WORKS (Interview Explanation)
1. **The Abstracted Pointer Swap:** `rotateStrike()` is highly efficient. By storing `striker` and `nonStriker` as Object References, we don't have to rewrite indices or search the `List<Player>`. We just swap the JVM memory pointers, instantly allowing the 1's and 3's logic to change who receives the `striker.addRuns()` in the next loop!
2. **Modulo Math for Overs:** Instead of writing a complex 2D-array for Overs, we track absolute continuous time: `totalValidBalls`.
   *   Overs Completed = `totalValidBalls / 6` (Integer math truncates decimals!)
   *   Balls in current over = `totalValidBalls % 6` (Modulo returns exactly 1-5).
   *   This automatically detects when to fire the "Over Completed" strike swap!
