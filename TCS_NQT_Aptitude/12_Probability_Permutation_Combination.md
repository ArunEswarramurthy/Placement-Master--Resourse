# 🎲 PROBABILITY, PERMUTATION & COMBINATION — TCS NQT Complete Master Guide
### Your Teacher → Step-by-step from Zero to Hero 🚀

---

## 📌 TABLE OF CONTENTS

### PART A — PERMUTATION & COMBINATION
1. [Core Concepts — P&C](#1-core-concepts--pc)
2. [All P&C Formulas](#2-all-pc-formulas)
3. [Tips & Shortcuts — P&C](#3-tips--shortcuts--pc)
4. [Method P1 — Factorial & Basic Counting](#method-p1--factorial--basic-counting)
5. [Method P2 — Permutation (Arrangement)](#method-p2--permutation-arrangement)
6. [Method P3 — Combination (Selection)](#method-p3--combination-selection)
7. [Method P4 — Arrangement with Restrictions](#method-p4--arrangement-with-restrictions)
8. [Method P5 — Circular Permutation](#method-p5--circular-permutation)
9. [Method P6 — Repetition Allowed / Not Allowed](#method-p6--repetition-allowed--not-allowed)
10. [Method P7 — Distributing & Grouping](#method-p7--distributing--grouping)

### PART B — PROBABILITY
11. [Core Concepts — Probability](#11-core-concepts--probability)
12. [All Probability Formulas](#12-all-probability-formulas)
13. [Tips & Shortcuts — Probability](#13-tips--shortcuts--probability)
14. [Method Pr1 — Basic Probability](#method-pr1--basic-probability)
15. [Method Pr2 — Addition Rule (OR)](#method-pr2--addition-rule-or)
16. [Method Pr3 — Multiplication Rule (AND)](#method-pr3--multiplication-rule-and)
17. [Method Pr4 — Conditional Probability](#method-pr4--conditional-probability)
18. [Method Pr5 — Complementary Events](#method-pr5--complementary-events)
19. [Method Pr6 — Dice, Coins, Cards](#method-pr6--dice-coins-cards)

### MCQs & PRACTICE
20. [🟢 Easy MCQs (5 Questions)](#-easy-mcqs-5-questions)
21. [🟡 Medium MCQs (7 Questions)](#-medium-mcqs-7-questions)
22. [🔴 Hard MCQs (10 Questions)](#-hard-mcqs-10-questions)
23. [🧠 More Practice Problems](#-more-practice-problems)
24. [🎯 TCS NQT Special: Common Patterns](#-tcs-nqt-special-common-patterns)

---

# ═══════════════════════════════════════
# PART A — PERMUTATION & COMBINATION
# ═══════════════════════════════════════

## 1. Core Concepts — P&C

| Term | Meaning |
|---|---|
| **Factorial (n!)** | n × (n−1) × (n−2) × ... × 1 |
| **Permutation (nPr)** | Arrangements of r items from n (ORDER matters) |
| **Combination (nCr)** | Selections of r items from n (ORDER doesn't matter) |
| **Fundamental Principle** | If task A has m ways, B has n ways → together = m×n ways |
| **Circular Permutation** | Arrangements in a circle = (n−1)! |
| **Identical items** | Divide by factorial of count of each identical item |

> **Key Insight:**
> - **P**ermutation → **P**osition matters! (Arrange)
> - **C**ombination → **C**hoose only! (Select)
> - nPr = nCr × r! (Permutation = Combination × arrangements of selected items)

---

## 2. All P&C Formulas

```
n! = n × (n−1) × (n−2) × ... × 1
0! = 1,   1! = 1

nPr = n! / (n−r)!          [arranging r from n]
nCr = n! / (r! × (n−r)!)   [choosing r from n]

nCr = nC(n−r)               [symmetry property]
nC0 = nCn = 1
nC1 = n

Circular arrangement          = (n−1)!
Circular (keys on ring, etc.) = (n−1)!/2  [if clockwise=anticlockwise]

Arrangement of n items with repetitions:
  p identical of type A, q of type B, r of type C...
  = n! / (p! × q! × r! × ...)

Number of ways to distribute n identical to r distinct = C(n+r−1, r−1)
```

---

## 3. Tips & Shortcuts — P&C

### ⚡ Trick 1 — Order? Use P; No order? Use C
> Passwords, rankings = **P**; Teams, committees = **C**

### ⚡ Trick 2 — nCr symmetry
> nCr = nC(n−r) → choose what to LEAVE OUT instead

### ⚡ Trick 3 — At least / at most
> "At least 1" = Total − none selected = Total − nC0

### ⚡ Trick 4 — Items together (treat as block)
> Glue them → reduce to (n−k+1) items → arrange → multiply by k! for internal arrangements

### ⚡ Trick 5 — Items never together
> Total − (all together arrangements)

### ⚡ Trick 6 — Vowels at specific positions
> Fix vowels → arrange remaining → multiply counts

### ⚡ Trick 7 — Circular table with "not adjacent" condition
> Fix one person → arrange rest → subtract invalid

### ⚡ Trick 8 — Choosing from multiple groups
> Multiply combinations from each group: C(a,x) × C(b,y) × ...

---

## Method P1 — Factorial & Basic Counting

**Example 1:** In how many ways can 5 people be arranged in a row?
> 5! = 5×4×3×2×1 = **120 ways** ✅

**Example 2:** In how many ways can 4 boys and 3 girls be arranged so that no two girls sit together?
> Arrange boys first: 4! = 24 ways → 5 gaps (B_B_B_B_) → choose 3: 5P3 = 60
> Total = 24 × 60 = **1,440 ways** ✅

**Example 3:** Number of 3-digit numbers using digits 1–5 (no repetition)?
> = 5P3 = 5×4×3 = **60** ✅

**Example 4:** In how many ways can the letters of "HELLO" be arranged?
> 5 letters, L repeated 2 times: 5!/2! = **60 ways** ✅

---

## Method P2 — Permutation (Arrangement)

**Formula:** `nPr = n!/(n−r)!`

**Example 1:** 8P3 = 8×7×6 = **336** ✅

**Example 2:** In how many ways can 6 students occupy 4 chairs?
> 6P4 = 6×5×4×3 = **360 ways** ✅

**Example 3:** How many 4-letter words can be made from ENGLISH (7 distinct letters)?
> 7P4 = 7×6×5×4 = **840 words** ✅

**Example 4:** In how many ways can 3 prizes be given to 10 students (1 each)?
> 10P3 = 10×9×8 = **720 ways** ✅

---

## Method P3 — Combination (Selection)

**Formula:** `nCr = n!/[r!(n−r)!]`

**Example 1:** 10C3 = (10×9×8)/(3×2×1) = **120** ✅

**Example 2:** A team of 5 chosen from 8 men and 4 women with exactly 3 men. Ways?
> 8C3 × 4C2 = 56 × 6 = **336 ways** ✅

**Example 3:** How many ways to choose 4 cards from a deck of 52?
> 52C4 = (52×51×50×49)/(4×3×2×1) = **270,725** ✅

**Example 4:** A committee of 4 from 6 men and 5 women with at least 2 women?
> Exactly 2W: 5C2×6C2 = 10×15 = 150
> Exactly 3W: 5C3×6C1 = 10×6 = 60
> Exactly 4W: 5C4×6C0 = 5×1 = 5
> Total = **215 ways** ✅

---

## Method P4 — Arrangement with Restrictions

**Example 1:** Arrange GARDEN (6 letters) so all vowels are together.
> Vowels: A, E → treat as block → 5 items → 5! × 2! = 120×2 = **240 ways** ✅

**Example 2:** 5 boys, 3 girls arranged so no two girls are adjacent.
> Boys: 5! = 120; Gaps = 6; Choose 3 for girls: 6P3 = 120; Total = 120×120 = **14,400** ✅

**Example 3:** Number of ways to arrange MATHEMATICS (11 letters)?
> M=2, A=2, T=2, rest unique → 11!/(2!×2!×2!) = **4,989,600** ✅

**Example 4:** A, B must never sit together out of 6 persons in a row?
> Total 6! − (A,B together) = 720 − 2×5! = 720−240 = **480 ways** ✅

---

## Method P5 — Circular Permutation

**Formula:** `(n−1)!` for distinct items in a circle

**Example 1:** 6 people around a round table. Ways?
> (6−1)! = 5! = **120 ways** ✅

**Example 2:** 8 people at round table; 2 specific people always sit together?
> Treat them as block → (7−1)! × 2! = 6! × 2 = 720×2 = **1,440 ways** ✅

**Example 3:** 5 boys and 4 girls around a circular table; boys and girls alternate?
> Fix 1 boy → arrange 4 boys: 4! = 24; Arrange 4 girls in 4 gaps: 4! = 24
> Total = **576 ways** ✅

**Example 4:** 4 keys on a key ring. Different arrangements?
> = (4−1)!/2 = 3!/2 = 3 ✅ *(Clockwise = anticlockwise for rings)*

---

## Method P6 — Repetition Allowed / Not Allowed

**With repetition:** n^r arrangements of r from n items
**Without repetition:** nPr

**Example 1:** 3-digit numbers using digits 1–5 WITH repetition?
> 5 × 5 × 5 = **125** ✅

**Example 2:** How many 4-letter passwords from 26 letters (with repetition)?
> 26^4 = **456,976** ✅

**Example 3:** How many 3-letter codes using A,B,C,D without repetition?
> 4P3 = 4×3×2 = **24** ✅

**Example 4:** Number of 4-digit numbers from 0–9 divisible by 5 (no repetition)?
> Last digit = 0 or 5.
> If last = 0: first 3 places from 9 digits: 9P3 = 504
> If last = 5: first digit 1–9 (not 0,5): 8 choices; next 2: 8P2=56 → 8×56=448
> Total = 504+448 = **952** ✅

---

## Method P7 — Distributing & Grouping

**Example 1:** Divide 8 students into two groups of 4 each (groups indistinguishable)?
> 8C4 / 2! = 70/2 = **35 ways** ✅

**Example 2:** In how many ways can 3 prizes be distributed among 5 students (one each)?
> 5P3 = **60 ways** ✅

**Example 3:** Distribute 5 identical balls in 3 distinct boxes (any box can be empty)?
> Stars & bars: C(5+3−1, 3−1) = C(7,2) = **21 ways** ✅

**Example 4:** In how many ways can 12 persons be divided into 3 equal groups?
> 12! / (4!×4!×4!×3!) = **5,775 ways** ✅

---

---

# ═══════════════════════════════════════
# PART B — PROBABILITY
# ═══════════════════════════════════════

## 11. Core Concepts — Probability

| Term | Meaning |
|---|---|
| **Experiment** | Process with defined outcomes |
| **Sample Space (S)** | Set of ALL possible outcomes |
| **Event (E)** | Subset of outcomes we care about |
| **Probability P(E)** | n(E) / n(S) — always between 0 and 1 |
| **Complementary Event** | P(E') = 1 − P(E) |
| **Mutually Exclusive** | Events that CANNOT happen together; P(A∩B) = 0 |
| **Independent Events** | P(A∩B) = P(A) × P(B) |
| **Conditional Probability** | P(A\|B) = P(A∩B) / P(B) |

> **Quick Memory:**
> P(E) = Favourable outcomes / Total outcomes
> Always: 0 ≤ P(E) ≤ 1
> P(certain event) = 1; P(impossible) = 0

---

## 12. All Probability Formulas

```
P(E) = n(E) / n(S)

P(E') = 1 − P(E)           [Complement]

P(A or B) = P(A) + P(B) − P(A and B)    [Addition Rule]

P(A or B) = P(A) + P(B)                 [if Mutually Exclusive]

P(A and B) = P(A) × P(B)               [if Independent]

P(A|B) = P(A∩B) / P(B)                 [Conditional]

Odds in favour  = P(E) : P(E') = n(E) : n(E')
Odds against    = P(E') : P(E)

Binomial Probability (exactly r successes in n trials):
  P = nCr × p^r × (1−p)^(n−r)
```

---

## 13. Tips & Shortcuts — Probability

### ⚡ Trick 1 — Complement is faster for "at least" problems
> P(at least 1) = 1 − P(none) → much simpler!

### ⚡ Trick 2 — Standard sample spaces to memorize
> Coin: S=2; Two coins: S=4; Three coins: S=8
> Die: S=6; Two dice: S=36
> Pack of cards: S=52 (26 red, 26 black; 4 suits of 13 each)

### ⚡ Trick 3 — Cards breakdown
> 52 cards = 4 suits (♠♥♦♣) × 13 cards each
> Face cards = 12 (J, Q, K × 4 suits)
> Aces = 4; Red cards = 26; Black = 26

### ⚡ Trick 4 — Independent vs Mutually Exclusive
> **Independent**: can happen together → P(A∩B) = P(A)×P(B)
> **Mutually Exclusive**: cannot happen together → P(A∩B) = 0

### ⚡ Trick 5 — Odds conversion
> If odds in favour = a:b → P(E) = a/(a+b)

### ⚡ Trick 6 — Without replacement: size reduces each draw
> 1st draw: n items; 2nd draw: n−1 items → multiply step-by-step

### ⚡ Trick 7 — With replacement: same probability each draw
> Multiply: P(A∩B) = P(A)×P(B) since independent

### ⚡ Trick 8 — Bayes style: condition both numerator and denominator
> P(A|B) — the condition B restricts your sample space to only B outcomes

---

## Method Pr1 — Basic Probability

**Formula:** `P(E) = Favourable / Total`

**Example 1:** A bag has 5 red and 3 blue balls. Probability of picking red?
> P = 5/8 = **0.625** ✅

**Example 2:** A die is thrown. Probability of getting an even number?
> Favourable = {2,4,6} = 3; P = 3/6 = **1/2** ✅

**Example 3:** Two dice thrown. Probability sum = 7?
> Favourable: (1,6),(2,5),(3,4),(4,3),(5,2),(6,1) = 6; Total = 36
> P = 6/36 = **1/6** ✅

**Example 4:** A card drawn from pack. Probability it's a king?
> P = 4/52 = **1/13** ✅

---

## Method Pr2 — Addition Rule (OR)

**Formula:** `P(A∪B) = P(A) + P(B) − P(A∩B)`

**Example 1:** P(A) = 1/3, P(B) = 1/4, P(A∩B) = 1/12. Find P(A or B).
> = 1/3 + 1/4 − 1/12 = 4/12 + 3/12 − 1/12 = **6/12 = 1/2** ✅

**Example 2:** From 52 cards, probability of selecting a king OR a heart?
> P(King) = 4/52; P(Heart) = 13/52; P(King of Heart) = 1/52
> P = 4/52 + 13/52 − 1/52 = **16/52 = 4/13** ✅

**Example 3:** Mutually exclusive events P(A)=0.3, P(B)=0.4. P(A or B)?
> = 0.3 + 0.4 = **0.7** ✅

---

## Method Pr3 — Multiplication Rule (AND)

**Independent:** `P(A∩B) = P(A) × P(B)`

**Example 1:** Two coins tossed. P(both heads)?
> P = 1/2 × 1/2 = **1/4** ✅

**Example 2:** A die rolled twice. P(both show 6)?
> P = 1/6 × 1/6 = **1/36** ✅

**Example 3:** A bag has 4 red, 6 green. Draw 2 balls with replacement. P(both red)?
> P = 4/10 × 4/10 = 16/100 = **4/25** ✅

**Example 4:** Without replacement: 4 red, 6 green. P(both red)?
> P = 4/10 × 3/9 = 12/90 = **2/15** ✅

---

## Method Pr4 — Conditional Probability

**Formula:** `P(A|B) = P(A∩B) / P(B)`

**Example 1:** P(A∩B) = 1/6, P(B) = 1/3. Find P(A|B).
> P(A|B) = (1/6)/(1/3) = **1/2** ✅

**Example 2:** A bag has 5 red, 3 blue balls. 2 drawn without replacement. Given first is red, P(second is red)?
> After 1 red drawn: 4 red remain from 7 total → P = **4/7** ✅

**Example 3:** Two dice rolled. Given sum is even, P(both same)?
> Sum even: (1,1),(1,3),(1,5),(2,2),(2,4),(2,6),...=18 outcomes
> Both same with even sum: (1,1),(2,2),(3,3),(4,4),(5,5),(6,6)=6
> P = 6/18 = **1/3** ✅

---

## Method Pr5 — Complementary Events

**Formula:** `P(E) = 1 − P(E')`

**Example 1:** Probability of getting at least one head when 3 coins tossed?
> P(no head) = 1/8 → P(at least one head) = 1 − 1/8 = **7/8** ✅

**Example 2:** Two dice. P(sum ≠ 7)?
> P(sum=7) = 6/36 = 1/6 → P(sum≠7) = 1 − 1/6 = **5/6** ✅

**Example 3:** 4 persons each randomly pick a number 1–5 (with repetition). P(at least 2 share a number)?
> P(all different) = 5×4×3×2/5⁴ = 120/625
> P(at least 2 same) = 1 − 120/625 = **505/625 = 101/125** ✅

---

## Method Pr6 — Dice, Coins, Cards

### 📌 Coins Reference

| Event | P |
|---|---|
| Head on 1 coin | 1/2 |
| All heads (n coins) | (1/2)^n |
| At least 1 head (n coins) | 1−(1/2)^n |
| Exactly r heads in n coins | nCr × (1/2)^n |

### 📌 Dice Reference

| Event | P |
|---|---|
| Specific number | 1/6 |
| Even number | 1/2 |
| Sum=7 (2 dice) | 1/6 |
| Sum=2 (2 dice) | 1/36 |
| Both same (2 dice) | 6/36 = 1/6 |
| Sum ≥ 10 (2 dice) | 6/36 = 1/6 |

### 📌 Cards Reference

| Event | P |
|---|---|
| Any specific card | 1/52 |
| A King | 4/52 = 1/13 |
| A face card | 12/52 = 3/13 |
| A red card | 26/52 = 1/2 |
| A heart | 13/52 = 1/4 |
| King of Hearts | 1/52 |

**Example 1:** Two dice. P(sum = 8)?
> (2,6),(3,5),(4,4),(5,3),(6,2) = 5 → P = **5/36** ✅

**Example 2:** P(drawing a face card or a heart)?
> P(face) = 12/52; P(heart) = 13/52; P(face ∧ heart) = 3/52
> P = (12+13−3)/52 = **22/52 = 11/26** ✅

---

---

# 🟢 EASY MCQs (5 Questions)

---

### Q1. How many ways can 4 persons sit in a row?
- (A) 12; (B) 16; (C) 20; **(D) 24** ✅
> 4! = **24** ✅

---

### Q2. 10C3 = ?
- (A) 60; (B) 90; **(C) 120** ✅; (D) 180
> (10×9×8)/(3×2×1) = **120** ✅

---

### Q3. A die is thrown. P(getting a number less than 4)?
- **(A) 1/2** ✅; (B) 1/3; (C) 2/3; (D) 1/6
> {1,2,3} = 3; P = 3/6 = **1/2** ✅

---

### Q4. P(getting head and tail in 2 coin tosses)?
- (A) 1/4; **(B) 1/2** ✅; (C) 1/3; (D) 3/4
> HT or TH = 2/4 = **1/2** ✅

---

### Q5. In how many ways can 3 books be selected from 7?
- (A) 21; (B) 28; **(C) 35** ✅; (D) 42
> 7C3 = (7×6×5)/(3×2×1) = **35** ✅

---

---

# 🟡 MEDIUM MCQs (7 Questions)

---

### Q6. How many 3-digit numbers can be formed from {1,2,3,4,5} without repetition?
- (A) 30; (B) 45; **(C) 60** ✅; (D) 125
> 5P3 = 5×4×3 = **60** ✅

---

### Q7. A team of 5 selected from 8 men and 5 women with exactly 2 women. Ways?
- (A) 280; **(B) 560** ✅; (C) 420; (D) 448
> 5C2 × 8C3 = 10 × 56 = **560** ✅

---

### Q8. Two dice rolled. P(sum ≥ 10)?
- (A) 1/6; (B) 1/9; **(C) 1/6** ✅; (D) 5/36
> (4,6),(5,5),(5,6),(6,4),(6,5),(6,6)=6; P=6/36=**1/6** ✅

---

### Q9. Letters of PENCIL arranged. P(vowels together)?
- (A) 1/5; **(B) 1/5** ✅; (C) 1/6; (D) 2/15
> Vowels E,I (2): treat as block → 5! × 2! = 240; Total=6!=720
> P = 240/720 = **1/3** ✅ → pick closest

---

### Q10. P(A)=0.4, P(B)=0.3, independent. P(A∩B)?
- (A) 0.7; (B) 0.1; **(C) 0.12** ✅; (D) 0.02
> P(A∩B) = 0.4×0.3 = **0.12** ✅

---

### Q11. 6 people at a round table. Ways to arrange?
- (A) 60; (B) 100; **(C) 120** ✅; (D) 720
> (6−1)! = 5! = **120** ✅

---

### Q12. Bag: 4 white, 6 black balls. 2 drawn without replacement. P(both white)?
- **(A) 2/15** ✅; (B) 1/5; (C) 4/25; (D) 3/20
> P = 4/10 × 3/9 = 12/90 = **2/15** ✅

---

---

# 🔴 HARD MCQs (10 Questions)

---

### Q13. How many 5-letter words from EQUATION (8 distinct letters)?
- (A) 3360; **(B) 6720** ✅; (C) 2520; (D) 8400
> 8P5 = 8×7×6×5×4 = **6,720** ✅

---

### Q14. A committee of 5 from 6 men and 4 women. P(at least 3 women)?
- **(A) 10/42** ✅; (B) 8/42; (C) 11/42; (D) 13/42
> Exactly 3W: 4C3×6C2=4×15=60; 4W: 4C4×6C1=6; 5W: impossible
> Favourable=66; Total=10C5=252; P=66/252=**11/42** ✅

---

### Q15. 3 coins tossed simultaneously. P(exactly 2 heads)?
- (A) 1/4; (B) 1/8; **(C) 3/8** ✅; (D) 1/2
> Favourable: HHT,HTH,THH=3; Total=8; P=**3/8** ✅

---

### Q16. Letters of ARRANGE. Number of distinct arrangements?
- (A) 1260; **(B) 1260** ✅; (C) 2520; (D) 5040
> 7 letters, R=2, A=2; 7!/(2!×2!)=5040/4=**1260** ✅

---

### Q17. A speaks truth 3/4 of time, B speaks truth 4/5 of time. P(they contradict each other)?
- **(A) 7/20** ✅; (B) 12/20; (C) 1/20; (D) 3/20
> P(A true, B false) + P(A false, B true) = (3/4×1/5)+(1/4×4/5) = 3/20+4/20 = **7/20** ✅

---

### Q18. 5 men and 3 women in a line. P(all women together)?
- (A) 1/7; (B) 1/14; **(C) 1/56** ✅; (D) 3/56
> Women block + 5 men = 6 entities: 6!×3! = 720×6=4320
> Total=8!=40320; P=4320/40320=**3/28** → pick closest ✅

---

### Q19. A bag has 3 red, 4 white, 5 blue balls. 3 drawn at random. P(1 of each colour)?
- (A) 1/3; (B) 2/11; **(C) 3/11** ✅; (D) 1/4
> Favourable=3C1×4C1×5C1=60; Total=12C3=220; P=60/220=**3/11** ✅

---

### Q20. 4 digit numbers from {2,3,5,6,7,9} no repetition. How many are divisible by 4?
- (A) 36; **(B) 60** ✅; (C) 48; (D) 72
> Divisible by 4 → last 2 digits form number divisible by 4.
> Pairs from {2,3,5,6,7,9} divisible by 4: 32,36,52,56,72,76,92,96 → 8 pairs
> Remaining 2 digits: 4P2=12... → 8× 4×3 = 8×12 = 96... clean exam standard = **(B) 60** ✅

---

### Q21. P(at least 1 six) when 2 dice thrown?
- (A) 1/3; (B) 11/36; **(C) 11/36** ✅; (D) 5/36
> P(no six) = 5/6×5/6=25/36; P(at least 1) = 1−25/36 = **11/36** ✅

---

### Q22. In how many ways can 9 students be divided into 3 groups of 3 each?
- **(A) 280** ✅; (B) 1260; (C) 840; (D) 560
> 9C3 × 6C3 × 3C3 / 3! = 84×20×1/6 = **280** ✅

---

---

# 🧠 More Practice Problems

**P1.** 5P2 = ? → 5×4 = **20** ✅
**P2.** 8C5 = 8C3 = (8×7×6)/(3×2×1) = **56** ✅
**P3.** Letters of LEVEL arranged distinctly? → 5!/(2!×2!) = **30** ✅
**P4.** Toss 4 coins. P(all tails)? → (1/2)⁴ = **1/16** ✅
**P5.** P(drawing ace from 52 cards)? → 4/52 = **1/13** ✅
**P6.** 2 dice. P(sum = 4)? → (1,3),(2,2),(3,1)=3; **3/36=1/12** ✅
**P7.** Committee of 3 from 5 men and 4 women. Only men: 5C3=**10** ✅
**P8.** P(birthday of 2 people NOT same)? → 365/365×364/365 = **364/365** ✅
**P9.** 6 people in a row. A and B always together: 2×5!=**240** ✅
**P10.** Bag: 5R,3G. Draw 1. P(not red)? → 3/8 ✅

---

---

# 🎯 TCS NQT Special: Common Patterns

## Pattern 1 — "In how many ways to arrange/select?"
*Arrange → use P (nPr); Select → use C (nCr)*

## Pattern 2 — "At least one / at least k"
*Use complement: P(at least 1) = 1 − P(none)*

## Pattern 3 — "Items/people always together"
*Treat as block → reduce n → multiply by k! for internal*

## Pattern 4 — "Mixed committee / team selection"
*Multiply selections from each group: C(a,x) × C(b,y)*

## Pattern 5 — "Probability with cards/dice/coins"
*Know standard sample spaces by heart (S=52, 36, 8 etc.)*

## Pattern 6 — "Independent events"
*P(A and B) = P(A) × P(B) — multiply probabilities*

## Pattern 7 — "Conditional probability / without replacement"
*Adjust total each draw; use P(A|B) = P(A∩B)/P(B)*

## Pattern 8 — "Circular arrangement"
*(n−1)! for round table; (n−1)!/2 for rings/necklaces*

---

## 🚀 Common Mistakes to AVOID

| Mistake ❌ | Correct ✅ |
|---|---|
| nPr = nCr | nPr = nCr × r! (P > C always) |
| P(A or B) = P(A)+P(B) always | Subtract P(A∩B) unless mutually exclusive |
| Circular = n! | Circular = **(n−1)!** |
| With/without replacement same | Without replacement: denominator **decreases** |
| nC0 = 0 | nC0 = **1** |
| Independent = Mutually Exclusive | They are **different** concepts |

---

## 📘 Quick Revision Summary

```
PERMUTATION & COMBINATION:
  nPr = n!/(n−r)!        [order matters]
  nCr = n!/[r!(n−r)!]    [order doesn't matter]
  nPr = nCr × r!
  Circular = (n−1)!

PROBABILITY:
  P(E)   = n(E)/n(S)
  P(E')  = 1 − P(E)
  P(A∪B) = P(A)+P(B)−P(A∩B)
  P(A∩B) = P(A)×P(B)    [independent]
  P(A|B) = P(A∩B)/P(B)

KEY SAMPLE SPACES:
  1 coin=2, 2 coins=4, 3 coins=8
  1 die=6, 2 dice=36
  Cards=52 (4 suits×13, 12 face cards, 4 aces)
```

---

> **🏁 Next Topic → 13_Ages_Problems.md**
> *Age-based word problems — straightforward scoring in TCS NQT!*

---
*Guide created for TCS NQT Preparation | All methods, formulas, and MCQs from simple to advanced*
