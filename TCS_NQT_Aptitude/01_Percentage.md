# 📊 PERCENTAGE — TCS NQT Complete Master Guide
### Your Teacher → Step-by-step from Zero to Hero 🚀

---

## 📌 TABLE OF CONTENTS
1. [What is Percentage?](#1-what-is-percentage)
2. [Core Formulas & Methods](#2-core-formulas--methods)
3. [Fraction ↔ Percentage Conversion Table](#3-fraction--percentage-conversion-table)
4. [Tips, Tricks & Shortcuts](#4-tips-tricks--shortcuts)
5. [Method 1 — Basic % Calculation](#method-1--basic--calculation)
6. [Method 2 — % Increase / Decrease](#method-2--increase--decrease)
7. [Method 3 — Successive % Change](#method-3--successive--change)
8. [Method 4 — % of a % (Two-step %)](#method-4--of-a--two-step-)
9. [Method 5 — % Comparison & Ratio-to-%](#method-5--comparison--ratio-to-)
10. [Method 6 — Population & Depreciation](#method-6--population--depreciation)
11. [Method 7 — Marks & Exam Problems](#method-7--marks--exam-problems)
12. [🟢 Easy MCQs (5 Questions)](#-easy-mcqs-5-questions)
13. [🟡 Medium MCQs (7 Questions)](#-medium-mcqs-7-questions)
14. [🔴 Hard MCQs (10 Questions)](#-hard-mcqs-10-questions)
15. [🧠 More Practice Problems](#-more-practice-problems)
16. [TCS NQT Special: Common Question Patterns](#-tcs-nqt-special-common-question-patterns)

---

## 1. What is Percentage?

> **Percentage** means **"per hundred"** — Latin: *per centum*.
>
> So **50%** simply means **50 out of 100**.

$$\text{Percentage} = \frac{\text{Part}}{\text{Whole}} \times 100$$

**Example:** In a class of 40 students, 10 passed. What % passed?
$$= \frac{10}{40} \times 100 = 25\%$$

---

## 2. Core Formulas & Methods

| Formula | Use When... |
|---|---|
| `% = (Part / Whole) × 100` | Finding what % one number is of another |
| `Part = (% / 100) × Whole` | Finding the actual value |
| `Whole = Part × (100 / %)` | Finding the original total |
| `New = Original × (1 + r/100)` | Increase by r% |
| `New = Original × (1 - r/100)` | Decrease by r% |
| `% Change = (Change / Original) × 100` | Finding % increase or decrease |
| `Net % = a + b + ab/100` | Two successive % changes |

---

## 3. Fraction ↔ Percentage Conversion Table

> **🔑 Memorize this table — it saves 30–40 seconds per question in TCS NQT!**

| Fraction | Percentage | Decimal |
|---|---|---|
| 1/2 | 50% | 0.5 |
| 1/3 | 33.33% | 0.333 |
| 2/3 | 66.66% | 0.666 |
| 1/4 | 25% | 0.25 |
| 3/4 | 75% | 0.75 |
| 1/5 | 20% | 0.20 |
| 2/5 | 40% | 0.40 |
| 3/5 | 60% | 0.60 |
| 4/5 | 80% | 0.80 |
| 1/6 | 16.66% | 0.1666 |
| 5/6 | 83.33% | 0.8333 |
| 1/7 | 14.28% | 0.1428 |
| 1/8 | 12.5% | 0.125 |
| 3/8 | 37.5% | 0.375 |
| 5/8 | 62.5% | 0.625 |
| 7/8 | 87.5% | 0.875 |
| 1/9 | 11.11% | 0.1111 |
| 1/10 | 10% | 0.10 |
| 1/11 | 9.09% | 0.0909 |
| 1/12 | 8.33% | 0.083 |

---

## 4. Tips, Tricks & Shortcuts

### ⚡ Trick 1 — "x% of y = y% of x"
> **25% of 80 = 80% of 25 = 20** ✅ (Pick whichever is easier to calculate!)

### ⚡ Trick 2 — Finding % quickly using 10%
> To find 35% of 460:
> - 10% of 460 = 46
> - 30% = 3 × 46 = 138
> - 5% = 46/2 = 23
> - 35% = 138 + 23 = **161** ✅

### ⚡ Trick 3 — Successive % using Net formula
> Price increased by 20% and then 10%:
> Net % = 20 + 10 + (20×10)/100 = 30 + 2 = **32%** ✅ (not 30%!)

### ⚡ Trick 4 — % Decrease to recover original
> If something decreases by R%, to recover you need to **increase by** `R/(100-R) × 100 %`
> Example: Salary cut by 20% → need **25% hike** to recover original (20/80 × 100 = 25%)

### ⚡ Trick 5 — Population problems: Multiply factors
> Population = P × (1 + r1/100) × (1 - r2/100) × ...
> Just chain-multiply the factors!

### ⚡ Trick 6 — Quick Division for % Change
> "A is what % more than B?" → `(A-B)/B × 100`
> "A is what % less than B?" → `(B-A)/B × 100`
> **⚠️ Always divide by the BASE (the reference/original value)!**

### ⚡ Trick 7 — Two candidates election trick
> If one candidate gets x% of votes and wins by N votes:
> Winner gets x%, loser gets (100-x)%
> Difference % = (2x - 100)%
> Total votes = N / (2x - 100) × 100

---

## Method 1 — Basic % Calculation

**Concept:** Convert percentages into fractions or use proportions.

**Formula:**
```
Part = (Percentage / 100) × Whole
Percentage = (Part / Whole) × 100
Whole = Part × 100 / Percentage
```

**Example 1:** What is 15% of 240?
> = (15/100) × 240 = 0.15 × 240 = **36** ✅

**Example 2:** 45 is what percent of 180?
> = (45/180) × 100 = 0.25 × 100 = **25%** ✅

**Example 3:** 30% of what number is 72?
> = 72 × (100/30) = 72 × 10/3 = **240** ✅

---

## Method 2 — % Increase / Decrease

**Formula:**
```
% Increase = (New - Old) / Old × 100
% Decrease = (Old - New) / Old × 100
New Value after R% increase  = Old × (100 + R) / 100
New Value after R% decrease  = Old × (100 - R) / 100
```

**Example 1:** Price rose from ₹400 to ₹480. Find % increase.
> = (480 - 400)/400 × 100 = 80/400 × 100 = **20%** ✅

**Example 2:** A number is decreased by 25%. It becomes 150. Find original.
> 150 = Original × (75/100)
> Original = 150 × 100/75 = **200** ✅

**Example 3 — TRAP QUESTION:** If A is 20% more than B, by what % is B less than A?
> A = 1.2B → B = A/1.2 = 5A/6
> B is less than A by: (A - 5A/6)/A × 100 = (A/6)/A × 100 = **16.67%** ✅
> *(NOT 20% — This is a very common TCS NQT trap!)*

---

## Method 3 — Successive % Change

**Formula (Two changes a% and b%):**
```
Net % Change = a + b + (a × b) / 100
```
> Note: Use **negative** values for decreases!

**Example 1:** A number is first increased by 30%, then decreased by 20%. Net change?
> = 30 + (-20) + (30 × -20)/100
> = 10 - 6 = **+4%** (overall increase of 4%) ✅

**Example 2:** Price increased by 10%, then again by 10%. Find net % increase.
> = 10 + 10 + (10×10)/100 = 20 + 1 = **21%** ✅

**Example 3:** A's salary was cut by 40%, then increased by 40%. Net change?
> = -40 + 40 + (-40 × 40)/100 = 0 - 16 = **-16%** (he is at a loss of 16%) ✅

---

## Method 4 — % of a % (Two-step %)

**Concept:** Convert each % to a fraction and multiply.

**Example 1:** Find 20% of 30% of 500.
> = (20/100) × (30/100) × 500
> = 0.20 × 0.30 × 500 = 0.06 × 500 = **30** ✅

**Example 2:** A article's price is first reduced by 10% and then by a further 10% of the reduced price. Overall reduction?
> Original = 100
> After 1st: 100 × 0.90 = 90
> After 2nd: 90 × 0.90 = 81
> Reduction = 100 - 81 = **19%** ✅

---

## Method 5 — % Comparison & Ratio-to-%

**Concept:** Express ratios as percentages, or compare two quantities.

**Formula:**
```
If ratio is a : b
a% of total = a/(a+b) × 100
b% of total = b/(a+b) × 100
```

**Example 1:** In a mixture of milk and water in ratio 3:2, what % is milk?
> = 3/(3+2) × 100 = 3/5 × 100 = **60%** ✅

**Example 2:** A is 25% of B. What % of A is B?
> A = 0.25B → B = A/0.25 = 4A
> B is 400% of A → B is **300% more** than A ✅

---

## Method 6 — Population & Depreciation

**Formula:**
```
After n years:
Value = P × (1 + r/100)ⁿ   [Growth]
Value = P × (1 - r/100)ⁿ   [Depreciation]
```

**Example 1:** A town's population is 50,000. It grows at 4% p.a. Find population after 2 years.
> = 50000 × (1.04)² = 50000 × 1.0816 = **54,080** ✅

**Example 2:** A machine costs ₹80,000, depreciates at 10% p.a. Value after 3 years?
> = 80000 × (0.9)³ = 80000 × 0.729 = **₹58,320** ✅

**Example 3:** Population increases 5% in year 1 and decreases 3% in year 2. If current = 40000, find after 2 years.
> = 40000 × 1.05 × 0.97 = 40000 × 1.0185 = **40,740** ✅

---

## Method 7 — Marks & Exam Problems

**Classic TCS NQT Exam Pattern!**

**Example 1:** A student scored 75% in an exam and got 450 marks. Total marks?
> 450 = 75% of T → T = 450 × 100/75 = **600** ✅

**Example 2:** Pass marks = 40%. A student got 185 marks, failed by 15. Find max marks.
> Pass marks = 185 + 15 = 200
> 40% of Max = 200 → Max = 200 × 100/40 = **500** ✅

**Example 3:** A student who gets 30% fails by 10 marks. Another who gets 40% gets 15 more than the minimum. Find max marks.
> Let max = M
> 0.3M + 10 = 0.4M - 15
> 25 = 0.1M → M = **250** ✅

---

---

# 🟢 EASY MCQs (5 Questions)

---

### Q1. What is 12% of 650?
- (A) 78
- (B) 72
- (C) 68
- (D) 75

> **✅ Answer: (A) 78**
> **Solution:**
> 12% of 650 = (12/100) × 650 = 0.12 × 650 = **78**
> *Shortcut: 10% of 650 = 65, 2% of 650 = 13 → 65+13=78*

---

### Q2. If 25% of a number is 75, what is the number?
- (A) 250
- (B) 300
- (C) 350
- (D) 400

> **✅ Answer: (B) 300**
> **Solution:**
> 25% × N = 75
> N = 75 × (100/25) = 75 × 4 = **300**

---

### Q3. What percent of 80 is 20?
- (A) 20%
- (B) 25%
- (C) 30%
- (D) 40%

> **✅ Answer: (B) 25%**
> **Solution:**
> (20/80) × 100 = 0.25 × 100 = **25%**
> *Fraction: 20/80 = 1/4 = 25%* ✅

---

### Q4. A price increases from ₹200 to ₹250. What is the % increase?
- (A) 20%
- (B) 25%
- (C) 30%
- (D) 50%

> **✅ Answer: (B) 25%**
> **Solution:**
> % increase = (250 - 200)/200 × 100 = 50/200 × 100 = **25%**

---

### Q5. A student scored 360 marks out of 600. What percentage did he score?
- (A) 55%
- (B) 60%
- (C) 65%
- (D) 70%

> **✅ Answer: (B) 60%**
> **Solution:**
> (360/600) × 100 = 0.6 × 100 = **60%**

---

---

# 🟡 MEDIUM MCQs (7 Questions)

---

### Q6. A number is increased by 20% and then decreased by 20%. The net change is:
- (A) 0%
- (B) -4%
- (C) +4%
- (D) -2%

> **✅ Answer: (B) -4%**
> **Solution (using net % formula):**
> Net % = 20 + (-20) + (20 × -20)/100 = 0 - 4 = **-4%**
> *Verify: 100 → ×1.2 = 120 → ×0.8 = 96 → loss of 4%* ✅
> *(TCS NQT TRAP — students often say 0%!)*

---

### Q7. In an election, candidate A got 55% of valid votes. Total valid votes = 8000. Candidate B got rest. By how many votes did A win?
- (A) 600
- (B) 800
- (C) 900
- (D) 1000

> **✅ Answer: (B) 800**
> **Solution:**
> A got = 55% of 8000 = 4400 votes
> B got = 45% of 8000 = 3600 votes
> Difference = 4400 - 3600 = **800** ✅

---

### Q8. If A is 40% more than B, then B is what % less than A?
- (A) 40%
- (B) 28.57%
- (C) 33.33%
- (D) 30%

> **✅ Answer: (B) 28.57%**
> **Solution:**
> A = 1.40 B → B = A / 1.40 = 5A/7
> B is less than A by: (A - 5A/7)/A × 100 = (2A/7)/A × 100 = 2/7 × 100 = **28.57%**
> *(TCS NQT favourite trap — answer is NOT 40%!)*

---

### Q9. The population of a city is 1,00,000. If it increases at 5% p.a., what will it be after 2 years?
- (A) 1,10,000
- (B) 1,10,250
- (C) 1,05,000
- (D) 1,02,500

> **✅ Answer: (B) 1,10,250**
> **Solution:**
> P = 1,00,000 × (1.05)²
> = 1,00,000 × 1.1025 = **1,10,250** ✅

---

### Q10. A student needs 40% to pass. He gets 200 marks and fails by 40 marks. What are the maximum marks?
- (A) 550
- (B) 600
- (C) 650
- (D) 700

> **✅ Answer: (B) 600**
> **Solution:**
> Pass marks = 200 + 40 = 240
> 40% of Max = 240
> Max = 240 × 100/40 = **600** ✅

---

### Q11. Two successive discounts of 20% and 10% are given on an item. What is the net discount?
- (A) 28%
- (B) 30%
- (C) 25%
- (D) 32%

> **✅ Answer: (A) 28%**
> **Solution:**
> Net % = -20 + (-10) + (-20 × -10)/100 = -30 + 2 = **-28%**
> *Verify: SP = 100 × 0.8 × 0.9 = 72 → Discount = 28%* ✅

---

### Q12. Ramesh's salary increased from ₹15,000 to ₹18,000. By what % did it increase?
- (A) 15%
- (B) 16.67%
- (C) 20%
- (D) 25%

> **✅ Answer: (C) 20%**
> **Solution:**
> % increase = (18000-15000)/15000 × 100 = 3000/15000 × 100 = 1/5 × 100 = **20%** ✅

---

---

# 🔴 HARD MCQs (10 Questions)

---

### Q13. A mixture contains 20% alcohol. If 10 litres of water is added, alcohol becomes 15%. Find the original quantity of mixture.
- (A) 30 L
- (B) 40 L
- (C) 50 L
- (D) 60 L

> **✅ Answer: (A) 30 L**
> **Solution:**
> Let original quantity = x litres
> Alcohol = 20% of x = 0.2x (unchanged when water is added)
> New total = x + 10
> New % of alcohol = 15%
> 0.2x = 15% × (x + 10)
> 0.2x = 0.15x + 1.5
> 0.05x = 1.5
> x = 1.5/0.05 = **30 litres** ✅

---

### Q14. Seena's income is 25% more than Reena's. Reena's income is what % less than Seena's?
- (A) 20%
- (B) 22%
- (C) 25%
- (D) 16.67%

> **✅ Answer: (A) 20%**
> **Solution:**
> Seena = 1.25 × Reena
> Reena = Seena / 1.25 = 4/5 × Seena
> Reena is less than Seena by 1/5 = **20%** ✅

---

### Q15. A, B, C got 40%, 35%, 25% of 1200 votes respectively. What is the difference between highest and lowest votes?
- (A) 150
- (B) 160
- (C) 180
- (D) 200

> **✅ Answer: (C) 180**
> **Solution:**
> A = 40% × 1200 = 480
> B = 35% × 1200 = 420
> C = 25% × 1200 = 300
> Difference (A - C) = 480 - 300 = **180** ✅

---

### Q16. The price of oil increases by 25%. By how much % must a family reduce its consumption so that the expenditure remains the same?
- (A) 20%
- (B) 22%
- (C) 25%
- (D) 23%

> **✅ Answer: (A) 20%**
> **Solution (using the trick):**
> Reduction = R/(100+R) × 100 = 25/125 × 100 = 1/5 × 100 = **20%** ✅
> *Formula: If price rises by R%, reduce consumption by R/(100+R) × 100*

---

### Q17. In an exam, 60% of students passed in English and 70% passed in Math. 20% failed in both. What % passed in both?
- (A) 30%
- (B) 40%
- (C) 50%
- (D) 60%

> **✅ Answer: (C) 50%**
> **Solution:**
> Failed in both = 20%, so at least one subject passed = 80%
> By inclusion-exclusion:
> P(E ∪ M) = P(E) + P(M) - P(E ∩ M)
> 80 = 60 + 70 - P(both)
> P(both) = 130 - 80 = **50%** ✅

---

### Q18. A person spends 30% on food, 25% on rent, 15% on education. He saves ₹3,000 from remaining. Find his income.
- (A) ₹10,000
- (B) ₹12,000
- (C) ₹15,000
- (D) ₹20,000

> **✅ Answer: (A) ₹10,000**
> **Solution:**
> Total spent % = 30 + 25 + 15 = 70%
> Remaining = 30%
> 30% of income = 3000
> Income = 3000 × 100/30 = **₹10,000** ✅

---

### Q19. If 20% of (A + B) = 40% of B, then A is what % of B?
- (A) 50%
- (B) 75%
- (C) 100%
- (D) 120%

> **✅ Answer: (C) 100%**
> **Solution:**
> 20(A + B) = 40B
> 20A + 20B = 40B
> 20A = 20B
> A = B → A/B × 100 = **100%** ✅

---

### Q20. A shopkeeper marks his goods 30% above cost price and gives a 10% discount. His profit %?
- (A) 15%
- (B) 17%
- (C) 18%
- (D) 20%

> **✅ Answer: (B) 17%**
> **Solution:**
> Let CP = 100
> MP = 130 (30% above)
> SP = 130 × 0.90 = 117
> Profit % = (117 - 100)/100 × 100 = **17%** ✅

---

### Q21. An employee's salary is first increased by 10% and then decreased by 10%. If original salary is ₹20,000, find the final salary.
- (A) ₹19,800
- (B) ₹18,000
- (C) ₹20,000
- (D) ₹21,000

> **✅ Answer: (A) ₹19,800**
> **Solution:**
> = 20000 × 1.10 × 0.90 = 20000 × 0.99 = **₹19,800** ✅
> *(Net: 10 + (-10) + (10×-10)/100 = 0 - 1 = -1% → 20000 × 0.99 = 19800)*

---

### Q22. In a class, 40% are girls. 50% of boys and 60% of girls pass an exam. What % of the class passed?
- (A) 52%
- (B) 54%
- (C) 56%
- (D) 58%

> **✅ Answer: (C) 56%**
> **Solution:**
> Girls = 40%, Boys = 60%
> Passed = (60% of boys) + (60% of girls)
>        = (50% × 60%) + (60% × 40%)
>        = 30% + 24% = **54%**
>
> Wait, recalculate:
> = 0.50 × 0.60 + 0.60 × 0.40
> = 0.30 + 0.24 = 0.54 = **54%** ✅
> **Correct Answer: (B) 54%**

---

---

# 🧠 More Practice Problems

> *The more you practice, the faster you get!*

---

**P1.** A number, when increased by 20% gives 360. Find the original number.
> **Answer:** 360 × 100/120 = **300** ✅

**P2.** Ram scored 70% in an exam. If the total marks is 800, how many marks did he score?
> **Answer:** 0.7 × 800 = **560** ✅

**P3.** Out of 500 students, 60% are boys. How many girls?
> Girls = 40% of 500 = 0.4 × 500 = **200** ✅

**P4.** A price increased by 10% and then by a further 10%. Effective % increase?
> Net = 10 + 10 + 1 = **21%** ✅

**P5.** By what % is 200 more than 150?
> = (200 - 150)/150 × 100 = 50/150 × 100 = **33.33%** ✅

**P6.** By what % is 150 less than 200?
> = (200 - 150)/200 × 100 = 50/200 × 100 = **25%** ✅

**P7.** If salary is cut by 30%, what % hike is needed to restore original?
> = 30/70 × 100 = **42.86%** ✅

**P8.** What is 150% of 80?
> = 1.5 × 80 = **120** ✅

**P9.** 30% of 40% of a number is 36. Find the number.
> 0.3 × 0.4 × N = 36 → 0.12N = 36 → N = **300** ✅

**P10.** In a village, 64% are literate. If 2304 people are illiterate, find total population.
> Illiterate = 36%
> 36% of Total = 2304
> Total = 2304 × 100/36 = **6400** ✅

**P11.** A factory's production increased by 20% in the 1st year and decreased by 10% in the 2nd year. Net % change?
> Net = 20 + (-10) + (20 × -10)/100 = 10 - 2 = **+8%** ✅

**P12.** A's income = 80% of B's. B's income = 75% of C's. A's income as % of C's?
> A = 0.80B = 0.80 × 0.75C = 0.60C = **60%** ✅

---

---

# 🎯 TCS NQT Special: Common Question Patterns

> TCS NQT repeats these **five patterns** the most in Percentage!

## Pattern 1 — "What % is X of Y / Y of X?"
*Watch base carefully!*
- X is what % of Y → (X/Y) × 100
- Y is what % of X → (Y/X) × 100

## Pattern 2 — "Salary/Price increase then decrease"
*Always use Net % formula or multiply factors!*
- Successive changes: Net = a + b + ab/100 (negative for decrease)

## Pattern 3 — "Exam pass/fail"
*Set up equation using pass marks!*
- Pass marks = scored + fail-by (if failed)
- Pass marks = scored - excess (if passed by N marks)

## Pattern 4 — "A is X% more/less than B — then B is ?% more/less than A"
*TCS TRAP! Always recalculate from B's perspective!*
- If A = (1 + r/100) × B → B is less than A by r/(100+r) × 100 %

## Pattern 5 — "Population growth"
*Use compound % formula: P × (1 ± r/100)^n*

---

## 🚀 Common Mistakes to AVOID in TCS NQT

| Mistake ❌ | Correct Approach ✅ |
|---|---|
| If salary rises 20% + 20% = 40% increase | Use net formula: 20+20+4 = **44%** |
| A is 30% more than B → B is 30% less than A | B is **23.07%** less (not 30%) |
| Price rose 25%, cut consumption by 25% to maintain | Cut by **20%** (not 25%) |
| Two discounts 20%+10% = 30% total | Net discount = **28%** |
| 25% of 80 ≠ 80% of 25 (different) | They ARE equal = **20** |

---

## 📘 Quick Revision Summary

```
Basic     : Part/Whole × 100
Find Part : (%) / 100 × Whole
Find Whole: Part × 100 / (%)
% Change  : (Change / Original) × 100
Successive: a + b + ab/100
Comp/Dep  : P × (1 ± r/100)^n
```

---

> **🏁 Next Topic → 02_Profit_and_Loss.md**
> *Build on % concepts — profit/loss percentage, marked price, discount!*

---
*Guide created for TCS NQT Preparation | All methods, formulas, and MCQs from simple to advanced*
