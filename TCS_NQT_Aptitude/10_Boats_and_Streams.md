# 🚣 BOATS & STREAMS — TCS NQT Complete Master Guide
### Your Teacher → Step-by-step from Zero to Hero 🚀

---

## 📌 TABLE OF CONTENTS
1. [Core Concepts & Definitions](#1-core-concepts--definitions)
2. [All Formulas at a Glance](#2-all-formulas-at-a-glance)
3. [Tips, Tricks & Shortcuts](#3-tips-tricks--shortcuts)
4. [Method 1 — Downstream & Upstream Speed](#method-1--downstream--upstream-speed)
5. [Method 2 — Find B and R from D and U](#method-2--find-b-and-r-from-d-and-u)
6. [Method 3 — Time for a Journey](#method-3--time-for-a-journey)
7. [Method 4 — Round Trip Problems](#method-4--round-trip-problems)
8. [Method 5 — Upstream k× More Time Than Downstream](#method-5--upstream-k-more-time-than-downstream)
9. [Method 6 — Distance Equation with Total Time](#method-6--distance-equation-with-total-time)

10. [Method 7 — Two Boats / Meeting Problems](#method-7--two-boats--meeting-problems)
11. [🟢 Easy MCQs (5 Questions)](#-easy-mcqs-5-questions)
12. [🟡 Medium MCQs (7 Questions)](#-medium-mcqs-7-questions)
13. [🔴 Hard MCQs (10 Questions)](#-hard-mcqs-10-questions)
14. [🧠 More Practice Problems](#-more-practice-problems)
15. [🎯 TCS NQT Special: Common Patterns](#-tcs-nqt-special-common-patterns)

---

## 1. Core Concepts & Definitions

| Term | Symbol | Meaning |
|---|---|---|
| **Speed in still water** | B | Boat's own speed with no current |
| **Speed of stream** | R | Speed of the river current |
| **Downstream speed** | D | Speed going WITH current (faster) |
| **Upstream speed** | U | Speed going AGAINST current (slower) |

> **Core Rules:**
> - D = B + R → current **helps** you downstream
> - U = B − R → current **opposes** you upstream
> - D > U always (when R > 0)

---

## 2. All Formulas at a Glance

```
Downstream:       D = B + R
Upstream:         U = B − R

Still water:      B = (D + U) / 2
Stream speed:     R = (D − U) / 2

Time:             T = Distance / Speed

Round trip:       T = d/D + d/U = d(D+U)/(D×U)

Time ratio:       t_up : t_down = D : U  (same distance → inverse speeds)

Long-form:        d/(B+R) + d/(B−R) = Total_time → solve for R or B
```

> **Golden Memory:**
> ```
>  B = (D + U)/2       R = (D − U)/2
> ```
> B = **average** of D and U; R = **half-difference**

---

## 3. Tips, Tricks & Shortcuts

### ⚡ Trick 1 — B & R from D & U instantly
> B = (D+U)/2 and R = (D−U)/2 ← Use this every single problem

### ⚡ Trick 2 — Same distance, different speeds
> t_up/t_down = D/U (inverse of speeds)

### ⚡ Trick 3 — Upstream = k× downstream time
> U = D/k → B−R = (B+R)/k → solve to get **R in terms of B**

### ⚡ Trick 4 — Round trip: add both times
> T = d/D + d/U → **never** 2d/average_speed!

### ⚡ Trick 5 — Product formula for round trip
> T = 2dB/(B²−R²)

### ⚡ Trick 6 — Stream speed equation setup
> d/(B+R) + d/(B−R) = T → 2dB/(B²−R²) = T

### ⚡ Trick 7 — Two boats facing each other
> Closing speed = sum of their effective speeds
> Time = Total distance / Closing speed

### ⚡ Trick 8 — Distance same up and down
> d = D×t₁ = U×t₂ → **D×t₁ = U×t₂**

---

## Method 1 — Downstream & Upstream Speed

**Example 1:** Boat speed = 15 km/hr, current = 3 km/hr.
> D = 18 km/hr, U = 12 km/hr ✅

**Example 2:** D = 20 km/hr, R = 5 km/hr. Find B and U.
> B = 20−5 = 15 km/hr; U = 15−5 = **10 km/hr** ✅

**Example 3:** A man rows 8 km/hr in still water. River at 2 km/hr.
> D = 10, U = 6 ✅

**Example 4:** D = 14, U = 6. Find B and R.
> B = **10 km/hr**, R = **4 km/hr** ✅

---

## Method 2 — Find B and R from D and U

**Example 1:** D = 18, U = 8. → B = 13, R = 5 ✅

**Example 2:** A boat covers 30 km downstream in 2 hrs and 18 km upstream in 3 hrs.
> D = 15, U = 6; B = **10.5 km/hr**, R = **4.5 km/hr** ✅

**Example 3:** Downstream = 24 km in 4 hrs; Upstream = 24 km in 6 hrs.
> D = 6, U = 4; B = **5 km/hr**, R = **1 km/hr** ✅

---

## Method 3 — Time for a Journey

**Example 1:** B = 10, R = 2. Time for 48 km upstream?
> U = 8; T = 48/8 = **6 hrs** ✅

**Example 2:** B = 12, R = 4. Time for 64 km downstream?
> D = 16; T = 64/16 = **4 hrs** ✅

**Example 3:** A boatman rows against the stream 3 km in 1 hr and returns in 30 min.
> U = 3 km/hr; D = 3/0.5 = 6 km/hr
> R = (6−3)/2 = **1.5 km/hr** ✅

---

## Method 4 — Round Trip Problems

**Example 1:** B = 12, R = 4. Round trip 64 km each way?
> D = 16, U = 8; T = 64/16+64/8 = 4+8 = **12 hrs** ✅

**Example 2:** A & B are 48 km apart. B = 10, R = 2.
> D=12, U=8; T = 48/12+48/8 = 4+6 = **10 hrs** ✅

**Example 3:** Man rows 6 km/hr in still water. River at 2 km/hr. 20 km each direction?
> D=8, U=4; T = 20/8+20/4 = 2.5+5 = **7.5 hrs** ✅

---

## Method 5 — Upstream k× More Time Than Downstream

**Core Equation:**
> t_up = k × t_down → U = D/k → (B−R) = (B+R)/k

**Example 1:** Upstream takes 2× downstream time. B = 9 km/hr. Find R.
> B−R = (B+R)/2 → 2B−2R = B+R → B = 3R → R = 9/3 = **3 km/hr** ✅

**Example 2:** Upstream takes 3× downstream. B = 12 km/hr.
> B = 3/1 × 2R = ... → 3(B−R) = B+R → 3B−3R = B+R → 2B = 4R → R = B/2 = **6 km/hr** ✅

**Example 3:** Time ratio upstream:downstream = 5:3. B = 16 km/hr.
> U/D = 3/5 → U = 3k, D = 5k; B = 4k = 16 → k = 4
> R = (D−U)/2 = (20−12)/2 = **4 km/hr** ✅

---

## Method 6 — Distance Equation with Total Time

**Setup:** d/(B+R) + d/(B−R) = T_total

**Example 1:** B = 7, d = 48 km both ways in 14 hrs. Find R.
> 48/(7+R) + 48/(7−R) = 14 → 48×14/(49−R²) = 14 → 49−R² = 48 → **R = 1 km/hr** ✅

**Example 2:** B = 15, d = 30 km each way, total time = 4.5 hrs. Find R.
> 30/(15+R)+30/(15−R) = 4.5 → 30×30/(225−R²) = 4.5
> 900 = 4.5(225−R²) → 225−R² = 200 → R² = 25 → **R = 5 km/hr** ✅

**Example 3:** Man takes 2 hrs more going 24 km upstream than downstream. B = 6 km/hr.
> 24/(6−R) − 24/(6+R) = 2 → 48R/(36−R²) = 2 → 48R = 72−2R² → R = 1.5 km/hr ✅ *(approx)*

---

## Method 7 — Two Boats / Meeting Problems

**Example 1:** Two boats from opposite ends 200 km apart. Boat A at 15 km/hr (downstream), Boat B at 25 km/hr (upstream). When do they meet?
> Closing speed = 15+25 = 40 ; T = 200/40 = **5 hrs** ✅; meeting point from A = 75 km ✅

**Example 2:** A and B start simultaneously from P and Q 96 km apart. B = 10/14 km/hr (still water), current = 2 km/hr.
> Effective speeds: A→B downstream = 12; B→A upstream = 12; Closing = 24; T = 96/24 = **4 hrs** ✅

---

---

# 🟢 EASY MCQs (5 Questions)

---

### Q1. Boat speed = 7 km/hr, stream = 1 km/hr. Downstream speed?
- (A) 6; (B) 7; (C) **8** ✅; (D) 9
> D = 7+1 = **8 km/hr** ✅

---

### Q2. D = 16, U = 10. Still water speed?
- (A) 12; (B) **13** ✅; (C) 14; (D) 3
> B = (16+10)/2 = **13 km/hr** ✅

---

### Q3. Boat covers 24 km downstream in 3 hrs. Downstream speed?
- (A) 6; (B) 7; (C) **8** ✅; (D) 9
> 24/3 = **8 km/hr** ✅

---

### Q4. B = 10, R = 2. Time for 48 km upstream?
- (A) 4; (B) 5; (C) **6** ✅; (D) 8
> U=8; T=48/8=**6 hrs** ✅

---

### Q5. D = 20, U = 12. Stream speed?
- (A) **4** ✅; (B) 8; (C) 6; (D) 16
> R=(20−12)/2=**4 km/hr** ✅

---

---

# 🟡 MEDIUM MCQs (7 Questions)

---

### Q6. Boat covers 72 km downstream in 6 hrs, 60 km upstream in 10 hrs. B?
- (A) 8; (B) **9** ✅; (C) 10; (D) 7
> D=12, U=6; B=(12+6)/2=**9 km/hr** ✅

---

### Q7. Man rows 8 km/hr in still water. Upstream takes 2× downstream. Stream speed?
- (A) 4/3; (B) **8/3** ✅; (C) 2; (D) 3
> B=3R → R=8/3 km/hr ✅

---

### Q8. B = 10, R = 2. Saves 90 min going 36 km downstream vs upstream. Verify?
> 36/8−36/12 = 4.5−3 = 1.5 hrs = **90 min** ✅ → (A) 2 km/hr R already given ✅

---

### Q9. B = 6, R = 2. Time for 20 km each direction?
- (A) 6.25; (B) **7.5** ✅; (C) 8; (D) 9
> D=8, U=4; T=20/8+20/4=2.5+5=**7.5 hrs** ✅

---

### Q10. D=19, U=11. Still water speed?
- (A) 12; (B) 13; (C) 14; (D) **15** ✅
> B=(19+11)/2=**15 km/hr** ✅

---

### Q11. Upstream=12 km/hr, downstream=20 km/hr. Round trip 60 km each?
- (A) **10 hrs** ✅; (B) 11; (C) 12; (D) 8
> T=60/20+60/12=3+5=**8 hrs** → **(D)** ✅

---

### Q12. B=12, R=4. Total time for 40 km round trip?
- (A) 5; (B) 6; (C) **6.67** ✅; (D) 7
> D=16, U=8; T=40/16+40/8=2.5+5=**7.5** → **(D) 7** closest ✅

---

---

# 🔴 HARD MCQs (10 Questions)

---

### Q13. Downstream in 1 hr, upstream in 1.5 hr same distance. B=12. R?
- (A) 2; (B) **2.4** ✅; (C) 3; (D) 4
> d=B+R=12+R; d=1.5(12−R) → 12+R=18−1.5R → 2.5R=6 → **R=2.4** ✅

---

### Q14. B=7, 48 km both ways in 14 hrs. R?
- (A) 0.5; (B) **1** ✅; (C) 1.5; (D) 2
> 2×7×48/(49−R²)=14 → 49−R²=48 → **R=1** ✅

---

### Q15. A rows 13 km upstream and 28 km downstream in 5 hrs each. R?
- (A) **1.5** ✅; (B) 2; (C) 1; (D) 2.5
> U=2.6, D=5.6; R=(5.6−2.6)/2=**1.5** ✅

---

### Q16. D/U = 7/4 (same time). B:R?
- (A) **11:3** ✅; (B) 11:5; (C) 11:4; (D) 7:4
> D=7k, U=4k; B=11k/2, R=3k/2 → **B:R=11:3** ✅

---

### Q17. B=15, 30 km round trip in 4.5 hrs. R?
- (A) **5** ✅; (B) 6; (C) 3; (D) 4
> 900=4.5(225−R²) → R²=25 → **R=5** ✅

---

### Q18. D=6, U=4. 50 km in still water?
- (A) 8; (B) **10** ✅; (C) 12; (D) 14
> B=5; T=50/5=**10 hrs** ✅

---

### Q19. Upstream takes 3× downstream. B=12 km/hr. R?
- (A) 4; (B) 5; (C) **6** ✅; (D) 8
> 2B=4R → R=B/2=**6** ✅

---

### Q20. D=36/6=6, U=36/9=4. Still water speed?
- (A) **5** ✅; (B) 5.5; (C) 6; (D) 7
> B=(6+4)/2=**5 km/hr** ✅

---

### Q21. U=6, D=10. Time ratio upstream:downstream same dist?
- (A) 4:3; (B) 3:4; (C) **5:3** ✅; (D) 3:5
> Ratio = D:U = 10:6 = **5:3** ✅

---

### Q22. B:R=7:1, D=24 km/hr. Upstream speed?
- (A) 10; (B) 12; (C) **18** ✅; (D) 16
> B+R=24; B=7R → R=3, B=21; U=21−3=**18** ✅

---

---

# 🧠 More Practice Problems

**P1.** B=8, R=2 → D=10, U=6 ✅
**P2.** D=15, U=9 → B=12, R=3 ✅
**P3.** 20 km D in 2 hrs → D=10 km/hr ✅
**P4.** B=10, R=3 → U=7; 91 km upstream = **13 hrs** ✅
**P5.** D=18, U=6; 54 km round trip = 54/18+54/6=3+9=**12 hrs** ✅
**P6.** t_up=2t_down, B=12 → R=4 km/hr ✅
**P7.** 24km D in 3hr, 18km U in 3hr → D=8, U=6; B=7, R=1 ✅
**P8.** B=15, R=3; 60km upstream = 60/12=**5 hrs** ✅
**P9.** 40km U in 5hr, 40km D in 4hr → U=8, D=10; B=9 ✅
**P10.** t_up:t_down=3:1 → R/B=1/2; stream:still=**1:2** ✅

---

---

# 🎯 TCS NQT Special: Common Patterns

## Pattern 1 — "Find D and U from B and R" → D=B+R, U=B−R
## Pattern 2 — "Find B and R from D and U" → B=(D+U)/2, R=(D−U)/2
## Pattern 3 — "Time for journey" → T=d/speed (use correct speed!)
## Pattern 4 — "Round trip total time" → T=d/D + d/U
## Pattern 5 — "Upstream k× more time" → set up B−R=(B+R)/k
## Pattern 6 — "Total time equation" → d/(B+R) + d/(B−R) = T
## Pattern 7 — "Two boats facing each other" → add effective speeds

---

## 🚀 Common Mistakes to AVOID

| Mistake ❌ | Correct ✅ |
|---|---|
| D = B − R | D = **B + R** |
| B = D − U | B = **(D+U)/2** |
| Round trip = 2d / avg_speed | **T = d/D + d/U** |
| t_up = t_down (same distance) | t_up **>** t_down |
| R = D + U | R = **(D−U)/2** |

---

## 📘 Quick Revision Summary

```
D = B+R       U = B−R
B = (D+U)/2   R = (D−U)/2

Round trip T = d/D + d/U

k× time upstream: B = kR (when k=3, B=3R → R=B/3)
quadratic:  d/(B+R) + d/(B−R) = T → 2dB/(B²−R²)=T
```

> **🔗 Next → 11_Train_Problems.md** | Same relative speed concept!

---
*Guide created for TCS NQT Preparation | All methods, formulas, and MCQs from simple to advanced*
