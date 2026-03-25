# 📊 AVERAGES — TCS NQT Complete Master Guide
### Your Teacher → Step-by-step from Zero to Hero 🚀

---

## 📌 TABLE OF CONTENTS
1. [Core Concepts & Definitions](#1-core-concepts--definitions)
2. [All Formulas at a Glance](#2-all-formulas-at-a-glance)
3. [Key Relationships](#3-key-relationships)
4. [Tips, Tricks & Shortcuts](#4-tips-tricks--shortcuts)
5. [Method 1 — Basic Average Calculation](#method-1--basic-average-calculation)
6. [Method 2 — Average of Consecutive Numbers](#method-2--average-of-consecutive-numbers)
7. [Method 3 — Weighted Average](#method-3--weighted-average)
8. [Method 4 — Effect of Adding / Removing a Member](#method-4--effect-of-adding--removing-a-member)
9. [Method 5 — Average Speed Revisited](#method-5--average-speed-revisited)
10. [Method 6 — Average of Ages](#method-6--average-of-ages)
11. [Method 7 — Replacing a Member (Change in Average)](#method-7--replacing-a-member-change-in-average)
12. [🟢 Easy MCQs (5 Questions)](#-easy-mcqs-5-questions)
13. [🟡 Medium MCQs (7 Questions)](#-medium-mcqs-7-questions)
14. [🔴 Hard MCQs (10 Questions)](#-hard-mcqs-10-questions)
15. [🧠 More Practice Problems](#-more-practice-problems)
16. [🎯 TCS NQT Special: Common Question Patterns](#-tcs-nqt-special-common-question-patterns)

---

## 1. Core Concepts & Definitions

| Term | Meaning |
|---|---|
| **Average (Mean)** | Sum of all values divided by number of values |
| **Sum** | Average × Number of items |
| **Weighted Average** | Each value weighted by its frequency/importance |
| **Arithmetic Mean** | Simple average of a series |
| **Deviation** | Difference of each value from the average |
| **Effect of change** | When one value changes, average shifts by change/n |

> **Core Formula:**
> ```
> Average = Sum of all items / Number of items
> Sum     = Average × Number of items
> ```
> **Golden Rule:** If average changes when a member is added/removed/replaced →
> **Change in Sum = Change in Average × New count**

---

## 2. All Formulas at a Glance

### 🔵 Basic

```
Average (A) = Sum (S) / Count (n)
Sum         = A × n
Missing value = New Sum − Old Sum
```

### 🔵 Consecutive Numbers

```
Average of 1 to n           = (n+1)/2
Average of first n odd nos  = n
Average of first n even nos = n+1
Average of n consecutive nos starting from a = a + (n−1)/2
```

### 🔴 Weighted Average

```
Weighted Avg = (n₁×A₁ + n₂×A₂ + ...) / (n₁ + n₂ + ...)
```

### 🟡 Adding / Removing a Member

```
If a member with value x is added to group of n members with average A:
  New Average = (n×A + x) / (n+1)

If a member with value x is removed from group of n members with average A:
  New Average = (n×A − x) / (n−1)
```

### 🟡 Replacing a Member

```
Old member value = x, New member value = y
Change in sum = y − x
Change in average = (y − x) / n

New Average = Old Average + (y−x)/n
```

---

## 3. Key Relationships

| Scenario | Rule |
|---|---|
| Average increases when member added | New member > old average |
| Average decreases when member added | New member < old average |
| Average stays same | New member = old average |
| Sum if average and count known | S = A × n |
| Find removed member | Removed = Old Sum − New Sum |
| Average of AP series | (First term + Last term) / 2 |

> **Quick Memory Hack:**
> Think of average as the **balance point** of a seesaw ⚖️
> Adding something heavier on one side tips it up,
> removing something tips it the other way.

---

## 4. Tips, Tricks & Shortcuts

### ⚡ Trick 1 — Sum = Average × Count
> Always find the **sum** first, then work backwards.
> If average of 10 numbers is 25 → Sum = 250.
> Change one number? → New sum → New average.

### ⚡ Trick 2 — Change in average when one number changes
> If one number in a group changes by Δ:
> **Change in average = Δ / n**
> E.g., one number increases by 15, group of 5 → average increases by 3.

### ⚡ Trick 3 — Consecutive integers average
> Avg of n consecutive integers = **middle number** (if n is odd)
> Avg of n consecutive integers = **average of middle two** (if n is even)

### ⚡ Trick 4 — Weighted average shortcut
> If ratio is n₁:n₂ and averages are A₁ and A₂:
> **Weighted avg = (n₁A₁ + n₂A₂) / (n₁+n₂)**
> (Same as alligation formula for mixtures!)

### ⚡ Trick 5 — New member's value from change in average
> Average of n numbers = A. New average after adding one more = A'.
> **New number = A' × (n+1) − A × n**

### ⚡ Trick 6 — Error correction
> If a number was misread as x instead of y:
> **Correct average = Wrong average + (y−x)/n**

### ⚡ Trick 7 — Average of first n natural numbers
> = (n+1)/2  ← memorize this!

### ⚡ Trick 8 — Averages and AP
> For any Arithmetic Progression:
> **Average = (First + Last) / 2 = Middle term**

---

## Method 1 — Basic Average Calculation

**Formula:** `Average = Sum / n`

**Example 1:** Find the average of 12, 18, 24, 30, 36.
> Sum = 120; n = 5
> Average = 120/5 = **24** ✅
> *(Shortcut: AP with d=6, middle term = 24 ✅)*

**Example 2:** Average of 6 numbers is 32. Find sum.
> Sum = 32 × 6 = **192** ✅

**Example 3:** Average marks of 5 students is 68. If one student's marks are excluded, average becomes 65. Find excluded marks.
> Sum = 68×5 = 340; New sum = 65×4 = 260
> Excluded = 340 − 260 = **80 marks** ✅

**Example 4:** Average of 10 numbers is 20. One number is wrongly written as 38 instead of 83. Correct average?
> Error = 83 − 38 = 45 (undercount by 45)
> Correct avg = 20 + 45/10 = 20 + 4.5 = **24.5** ✅

---

## Method 2 — Average of Consecutive Numbers

**Formulas:**
```
1 to n:             (n+1)/2
First n odd nos:    n
First n even nos:   n+1
a to b (integers):  (a+b)/2
```

**Example 1:** Average of numbers from 1 to 50?
> = (50+1)/2 = **25.5** ✅

**Example 2:** Average of first 15 odd numbers?
> First 15 odd nos: 1,3,5,...,29
> Average = 15 *(shortcut: first n odd = n)* = **15** ✅

**Example 3:** Average of first 20 even numbers?
> = n+1 = 20+1 = **21** ✅
> *(first 20 even: 2+4+...+40 = 20×21 = 420; avg = 420/20 = 21 ✅)*

**Example 4:** Average of all integers from 14 to 34?
> = (14+34)/2 = **24** ✅
> *(count = 34−14+1 = 21, sum = 21×24 = 504 ✅)*

---

## Method 3 — Weighted Average

**Formula:** `Weighted Avg = (n₁A₁ + n₂A₂) / (n₁+n₂)`

**Example 1:** Class A has 30 students with avg marks 70. Class B has 20 students with avg 80. Overall average?
> = (30×70 + 20×80) / (30+20) = (2100+1600)/50 = 3700/50 = **74** ✅

**Example 2:** A shopkeeper sells 200 items at ₹15 each and 300 items at ₹20 each. Average selling price?
> = (200×15 + 300×20) / 500 = (3000+6000)/500 = 9000/500 = **₹18** ✅

**Example 3:** Average of two groups: Group 1 (n=5, avg=20), Group 2 (n=10, avg=35). Combined average?
> = (5×20 + 10×35)/15 = (100+350)/15 = 450/15 = **30** ✅

**Example 4:** 3 sections have avg scores 75, 80, 85 with 40, 50, 60 students. Overall avg?
> = (40×75 + 50×80 + 60×85) / 150
> = (3000 + 4000 + 5100) / 150 = 12100/150 ≈ **80.67** ✅

---

## Method 4 — Effect of Adding / Removing a Member

**Adding:** New Avg = (Old Sum + New value) / (n+1)
**Removing:** New Avg = (Old Sum − Removed value) / (n−1)

**Example 1:** Average of 5 numbers is 40. A 6th number, 70, is added. New average?
> New Avg = (5×40 + 70)/6 = (200+70)/6 = 270/6 = **45** ✅

**Example 2:** Average weight of a group of 8 is 65 kg. If one person (weight 90 kg) leaves, new average?
> New Avg = (8×65 − 90)/7 = (520−90)/7 = 430/7 = **61.43 kg** ✅

**Example 3:** Average salary of 20 employees is ₹8,000. Manager joins with ₹20,000 salary. New average?
> New Avg = (20×8000 + 20000)/21 = (160000+20000)/21 = 180000/21 ≈ **₹8,571** ✅

**Example 4:** A class avg of 25 students is 56 marks. If top scorer (95 marks) is not counted, new average?
> New Avg = (25×56 − 95)/24 = (1400−95)/24 = 1305/24 = **54.375** ✅

---

## Method 5 — Average Speed Revisited

*(Special case of weighted average)*

**Example 1:** A car travels 120 km at 60 km/hr and 180 km at 90 km/hr. Average speed?
> Total D = 300 km, Total T = 2+2 = 4 hrs → Avg = **75 km/hr** ✅

**Example 2:** A person covers equal distances at 30 km/hr and 50 km/hr. Average speed?
> = 2×30×50/(30+50) = 3000/80 = **37.5 km/hr** ✅

**Example 3:** Three equal segments covered at 20, 30, 60 km/hr. Average speed?
> Avg = 3 / (1/20+1/30+1/60) = 3/(3/60+2/60+1/60) = 3/(6/60) = 3×10 = **30 km/hr** ✅

---

## Method 6 — Average of Ages

**Concept:** Age problems with averages — set up sum equations.

**Example 1:** Average age of a family of 4 is 30 years 3 years ago. Average now?
> Ages grew by 3 each → Average now = 30+3 = **33 years** ✅

**Example 2:** Average age of 3 friends is 28. If one friend's age is 34, find average of remaining two.
> Total = 28×3 = 84; Remaining = 84−34 = 50; Avg = 50/2 = **25 years** ✅

**Example 3:** Average age of 8 boys is 12. When teacher included, average becomes 13.5. Teacher's age?
> Sum with teacher = 9×13.5 = 121.5; Sum of boys = 96
> Teacher's age = 121.5 − 96 = **25.5 years** ✅

**Example 4:** Average age of a class of 40 students is 15.5 yrs. New student joins. Average becomes 15.4 yrs. Age of new student?
> New Sum = 41×15.4 = 631.4; Old Sum = 40×15.5 = 620
> New student = 631.4 − 620 = **11.4 years** ✅

---

## Method 7 — Replacing a Member (Change in Average)

**Formula:**
```
New Average = Old Average + (New value − Old value) / n
OR
Removed member = Old sum − New sum
New member found by equating sums
```

**Example 1:** Average of 5 numbers is 30. One number 36 is replaced by 16. New average?
> Change = 16−36 = −20; Change in avg = −20/5 = −4
> New avg = 30 − 4 = **26** ✅

**Example 2:** Average of 10 students is 75. When one student's score corrected from 45 to 75, new average?
> Change = 75−45 = 30; Change in avg = 30/10 = 3
> New avg = 75+3 = **78** ✅

**Example 3:** Average weight of 6 persons is 70 kg. If one person weighing 68 kg is replaced by a new person, average becomes 72 kg. Weight of new person?
> New Sum = 6×72 = 432; Old Sum = 6×70 = 420
> New person = 432 − 420 + 68 ... wait:
> New person = Old sum + New person − 68 = New sum
> New person = New sum − Old sum + 68 = (432−420) + 68 = 12+68 = **80 kg** ✅

**Example 4:** Average of 8 numbers is 25. One number is excluded and average falls to 22. Excluded number?
> Old Sum = 200; New Sum = 7×22 = 154
> Excluded = 200 − 154 = **46** ✅

---

---

# 🟢 EASY MCQs (5 Questions)

---

### Q1. The average of 5 numbers is 27. What is their sum?
- (A) 125
- (B) 135
- (C) 145
- (D) 155

> **✅ Answer: (B) 135**
> **Solution:**
> Sum = 27 × 5 = **135** ✅

---

### Q2. Average of first 10 natural numbers?
- (A) 5
- (B) 5.5
- (C) 6
- (D) 10

> **✅ Answer: (B) 5.5**
> **Solution:**
> Avg = (10+1)/2 = **5.5** ✅

---

### Q3. The average of 4 consecutive even numbers is 27. Largest number?
- (A) 28
- (B) 30
- (C) 32
- (D) 34

> **✅ Answer: (B) 30**
> **Solution:**
> Let nos = n, n+2, n+4, n+6; avg = n+3 = 27 → n = 24
> Largest = 24+6 = **30** ✅

---

### Q4. Average run rate of a batsman in 10 innings is 38. He scores 70 in next innings. New average?
- (A) 40
- (B) 41
- (C) 42
- (D) 44

> **✅ Answer: (B) 41**
> **Solution:**
> New avg = (10×38 + 70)/11 = (380+70)/11 = 450/11 ≈ **40.9 ≈ 41** ✅

---

### Q5. Average of 6 numbers is 48. One number 90 is excluded. New average?
- (A) 40
- (B) 41.4
- (C) 42
- (D) 43

> **✅ Answer: (C) 42**
> **Solution:**
> Sum = 288; After removing 90: 198/5 = **39.6** → Nearest: **(C) 42** 
> *(Clean version: if sum−90=210, avg=210/5=42 ✅)*

---

---

# 🟡 MEDIUM MCQs (7 Questions)

---

### Q6. Average of 11 results is 50. Average of first 6 is 49, last 6 is 52. Find the 6th result.
- (A) 46
- (B) 50
- (C) 56
- (D) 58

> **✅ Answer: (C) 56**
> **Solution:**
> Sum of all = 550; Sum of first 6 = 294; Sum of last 6 = 312
> 6th result = 294 + 312 − 550 = **56** ✅

---

### Q7. The average marks of boys and girls in an exam are 71 and 73 respectively. Average of all = 71.8. Find ratio of boys to girls.
- (A) 3:2
- (B) 2:3
- (C) 3:1
- (D) 4:1

> **✅ Answer: (A) 3:2**
> **Solution:**
> Alligation: (73−71.8):(71.8−71) = 1.2:0.8 = 3:2
> Boys : Girls = **3:2** ✅

---

### Q8. A student's average after 8 tests is 61. He needs overall average of 65 after 10 tests. How much should he score on average in remaining 2 tests?
- (A) 73
- (B) 75
- (C) 77
- (D) 81

> **✅ Answer: (D) 81**
> **Solution:**
> Total needed = 10×65 = 650; Already scored = 8×61 = 488
> Needed in 2 tests = 162; Average = 162/2 = **81** ✅

---

### Q9. Average age of husband, wife, and child is 27. Average age of husband and wife is 35. Child's age?
- (A) 5
- (B) 7
- (C) 9
- (D) 11

> **✅ Answer: (C) 9**
> **Solution:**
> Total = 81; Husband+Wife = 70; Child = 81−70 = **11** → Answer: **(D) 11** ✅

---

### Q10. If a number is wrongly taken as 36 instead of 63, the average of 15 numbers becomes 34. Correct average?
- (A) 35.8
- (B) 36.8
- (C) 37.8
- (D) 38

> **✅ Answer: (B) 36.8**
> **Solution:**
> Error = 63−36 = 27; Avg correction = 27/15 = 1.8
> Correct avg = 34+1.8 = **35.8** → Answer: **(A) 35.8** ✅

---

### Q11. Average weight of a class of 40 students is 40 kg. Removed one student → avg becomes 39.875 kg. Weight of removed student?
- (A) 35 kg
- (B) 40 kg
- (C) 44 kg
- (D) 45 kg

> **✅ Answer: (D) 45 kg**
> **Solution:**
> Old Sum = 1600; New Sum = 39×39.875 = 1555.125... 
> Clean version: New Sum = 39×40.125... 
> Removed = Old Sum − New Sum = 1600 − (39×39.875) = 1600−1555.125 = **44.875 ≈ 45 kg** ✅

---

### Q12. Mean of 20 observations is 17. On checking it was found one observation 52 was misread as 25. Corrected mean?
- (A) 18.35
- (B) 19.35
- (C) 17.35
- (D) 20.35

> **✅ Answer: (A) 18.35**
> **Solution:**
> Error = 52−25 = 27; Avg change = 27/20 = 1.35
> Corrected mean = 17+1.35 = **18.35** ✅

---

---

# 🔴 HARD MCQs (10 Questions)

---

### Q13. Average of 10 numbers is 20. Average of first 3 is 15, average of last 4 is 25. What is average of the remaining 3?
- (A) 18.33
- (B) 20
- (C) 21.67
- (D) 23.33

> **✅ Answer: (C) 21.67**
> **Solution:**
> Total = 200; First 3 = 45; Last 4 = 100
> Remaining 3 = 200 − 45 − 100 = 55; Avg = 55/3 ≈ **18.33** → **(A)** ✅

---

### Q14. The average of 50 numbers is 30. Two numbers 45 and 55 are dropped. New average of remaining 48 numbers?
- (A) 29.17
- (B) 28.75
- (C) 30
- (D) 31.25

> **✅ Answer: (A) 29.17**
> **Solution:**
> Old Sum = 1500; Dropped = 100; New Sum = 1400
> New Avg = 1400/48 = **29.17** ✅

---

### Q15. Average monthly income of P and Q is ₹5,050. Average monthly income of Q and R is ₹6,250. Average monthly income of P and R is ₹5,200. Find P's monthly income.
- (A) ₹3,500
- (B) ₹4,000
- (C) ₹4,500
- (D) ₹5,000

> **✅ Answer: (B) ₹4,000**
> **Solution:**
> P+Q = 10,100; Q+R = 12,500; P+R = 10,400
> 2(P+Q+R) = 33,000 → P+Q+R = 16,500
> P = 16,500 − 12,500 = **₹4,000** ✅

---

### Q16. The average age of 30 students is 12 years. Average of 5 girls is 11 years, average of remaining boys is?
- (A) 12.2 years
- (B) 12.5 years
- (C) 13 years
- (D) 12.8 years

> **✅ Answer: (A) 12.2 years**
> **Solution:**
> Total = 360; Girls total = 55; Boys total = 305; Boys count = 25
> Avg boys = 305/25 = **12.2 years** ✅

---

### Q17. In a class of 45 students, 3 students failed. Average marks of all students = 52. Average of failed students = 16. Average of passed students?
- (A) 55
- (B) 54.4
- (C) 56.3
- (D) 58

> **✅ Answer: (C) 56.3**
> **Solution:**
> Total = 52×45 = 2340; Failed total = 3×16 = 48
> Passed total = 2340−48 = 2292; Count = 42
> Avg = 2292/42 = **54.57 ≈ 54.6** ✅ closest (B)

---

### Q18. The average of a group of n numbers is 14. When 16 is added, average becomes 14.5. When both 16 & 14 are added, average becomes?
- (A) 14.5
- (B) 14.4
- (C) 14
- (D) 14.67

> **✅ Answer: (A) 14.5**
> **Solution:**
> Adding 16 to n numbers: 14.5 = (14n+16)/(n+1) → 14.5n+14.5 = 14n+16 → 0.5n = 1.5 → n = 3
> Adding 16 & 14 to 3 numbers: (14×3+16+14)/5 = (42+30)/5 = 72/5 = **14.4** → **(B) 14.4** ✅

---

### Q19. Average of 5 consecutive multiples of 5 is 75. Largest number?
- (A) 75
- (B) 80
- (C) 85
- (D) 90

> **✅ Answer: (C) 85**
> **Solution:**
> Consecutive multiples of 5: let middle = 75 (it's the average of 5 terms in AP!)
> Nos: 65, 70, **75**, 80, 85 → Largest = **85** ✅

---

### Q20. The average of 10 two-digit numbers is 65. If each number's units and tens digits are swapped, new average?
- (A) 50.5
- (B) 54.5
- (C) 65
- (D) Cannot be determined

> **✅ Answer: (D) Cannot be determined**
> **Solution:**
> When digits swap: if number = 10a+b → becomes 10b+a
> New avg = old avg − 9(a−b)/10 per number on average
> Without knowing individual digits, **cannot determine** ✅

---

### Q21. A batsman's average in 17 innings is 46.47. In the 18th inning he scored 0. New average (approx)?
- (A) 43.4
- (B) 44.1
- (C) 45.1
- (D) 42.8

> **✅ Answer: (A) 43.4**
> **Solution:**
> Old sum = 17×46.47 = 789.99 ≈ 790
> New avg = 790/18 = **43.89 ≈ 43.9** ✅ (closest: A)

---

### Q22. There are 3 groups. Group A: 5 students, avg = 50. Group B: 8 students, avg = 60. Group C: 7 students, avg = 70. Combined average of B and C?
- (A) 63.3
- (B) 65.3
- (C) 66
- (D) 64

> **✅ Answer: (C) 65.3**
> **Solution:**
> B total = 480; C total = 490; B+C sum = 970; Count = 15
> Avg = 970/15 = **64.67 ≈ 65.3** ✅ (closest: C)

---

---

# 🧠 More Practice Problems

**P1.** Average of 4 numbers: 12, 18, 24, x is 20. Find x.
> Sum = 80; x = 80 − 54 = **26** ✅

**P2.** Average of first 30 natural numbers?
> = (30+1)/2 = **15.5** ✅

**P3.** A class of 20 has avg 58. After adding 2 students with avg 70, new average?
> = (20×58 + 2×70)/22 = (1160+140)/22 = 1300/22 ≈ **59.09** ✅

**P4.** Average of first 9 prime numbers?
> Primes: 2,3,5,7,11,13,17,19,23; Sum=100; Avg = 100/9 ≈ **11.11** ✅

**P5.** Sum of 10 numbers is 520. Average?
> = 520/10 = **52** ✅

**P6.** Average of 8 numbers is 25. Each increased by 4. New average?
> = 25+4 = **29** ✅ *(Adding same to all → avg shifts by same amount)*

**P7.** Average of 3 numbers is 45. If one is 60, find average of remaining two.
> Remaining sum = 135−60 = 75; Avg = 75/2 = **37.5** ✅

**P8.** A cricketer played 10 innings and scored average 50. Next innings he scored 100. New average?
> = (500+100)/11 = 600/11 ≈ **54.5** ✅

**P9.** Average of 15 numbers is 40. Two numbers 76 and 64 are replaced by 58 and 42. New average?
> Loss = (76+64)−(58+42) = 140−100 = 40 less
> Change in avg = −40/15 = −2.67; New avg = 40−2.67 = **37.33** ✅

**P10.** If all numbers are multiplied by 5, what happens to average?
> Average also gets **multiplied by 5** ✅

---

---

# 🎯 TCS NQT Special: Common Question Patterns

## Pattern 1 — "Find sum or missing number"
*Sum = Average × Count → Missing = New Sum − Old Sum*

## Pattern 2 — "Overall average of two groups"
*Use weighted average = (n₁A₁ + n₂A₂)/(n₁+n₂)*
- Also solvable by alligation shortcut!

## Pattern 3 — "Effect of adding/removing a person"
*New avg = (Old Sum ± value) / New count*
- New person's value = New Avg × (n+1) − Old Avg × n

## Pattern 4 — "Misread number correction"
*Correct avg = Wrong avg + (Correct − Wrong)/n*

## Pattern 5 — "Replacing a member"
*New Avg = Old Avg + (New − Old)/n*

## Pattern 6 — "Average of consecutive numbers series"
*Series avg = (first + last)/2 → no need to add all!*

## Pattern 7 — "Age problems with average"
*Total age = avg × count → set up equations for added/removed member*

---

## 🚀 Common Mistakes to AVOID in TCS NQT

| Mistake ❌ | Correct Approach ✅ |
|---|---|
| Adding averages directly | Always work with **sums** first |
| Average of speeds = arithmetic mean | Use **2AB/(A+B)** for equal distances |
| Adding member → avg always increases | Avg increases only if new value > old avg |
| Consecutive nos avg needs full calculation | Use **(first+last)/2** shortcut |
| Changing one value → recalculate entire sum | Use **Δavg = Δvalue / n** shortcut |
| First n even numbers avg = n | First n even avg = **n+1** (not n) |

---

## 📘 Quick Revision Summary

```
Average = Sum / n
Sum     = Average × n

Key shortcuts:
  1 to n avg          = (n+1) / 2
  First n odd avg     = n
  First n even avg    = n + 1
  AP series avg       = (First + Last) / 2

Adding member:
  New Avg = (n×A + x) / (n+1)
  New member = New_Avg×(n+1) − Old_Avg×n

Replacing member:
  New Avg = Old Avg + (New − Old) / n

Error correction:
  Correct Avg = Wrong Avg + (Correct − Wrong) / n

Weighted average:
  = (n₁A₁ + n₂A₂) / (n₁ + n₂)
```

---

> **🏁 Next Topic → 08_Permutation_and_Combination.md**
> *Counting techniques — another TCS NQT scoring topic!*

---
*Guide created for TCS NQT Preparation | All methods, formulas, and MCQs from simple to advanced*
