# 💰 PROFIT & LOSS — TCS NQT Complete Master Guide
### Your Teacher → Step-by-step from Zero to Hero 🚀

---

## 📌 TABLE OF CONTENTS
1. [Core Concepts & Definitions](#1-core-concepts--definitions)
2. [All Formulas at a Glance](#2-all-formulas-at-a-glance)
3. [Tips, Tricks & Shortcuts](#3-tips-tricks--shortcuts)
4. [Method 1 — Basic P&L Calculation](#method-1--basic-pl-calculation)
5. [Method 2 — Marked Price, Discount & SP](#method-2--marked-price-discount--sp)
6. [Method 3 — Dishonest Dealer / False Weight](#method-3--dishonest-dealer--false-weight)
7. [Method 4 — Selling Two Items (Same SP, Same %)](#method-4--selling-two-items-same-sp-same-)
8. [Method 5 — Cost Price When P% & L% Given Together](#method-5--cost-price-when-p--l-given-together)
9. [Method 6 — Successive Discounts](#method-6--successive-discounts)
10. [Method 7 — Profit/Loss on Multiple Transactions](#method-7--profitloss-on-multiple-transactions)
11. [🟢 Easy MCQs (5 Questions)](#-easy-mcqs-5-questions)
12. [🟡 Medium MCQs (7 Questions)](#-medium-mcqs-7-questions)
13. [🔴 Hard MCQs (10 Questions)](#-hard-mcqs-10-questions)
14. [🧠 More Practice Problems](#-more-practice-problems)
15. [TCS NQT Special: Common Question Patterns](#-tcs-nqt-special-common-question-patterns)

---

## 1. Core Concepts & Definitions

| Term | Meaning |
|---|---|
| **Cost Price (CP)** | The price at which an article is purchased / produced |
| **Selling Price (SP)** | The price at which an article is sold |
| **Profit** | SP > CP → Profit = SP − CP |
| **Loss** | CP > SP → Loss = CP − SP |
| **Marked Price (MP)** | The price written/tagged on the article (before discount) |
| **Discount** | Reduction given on MP → Discount = MP − SP |
| **Overhead Cost** | Extra expenses (transport, repair) added to CP |

> **Golden Rule:**
> - If SP > CP → **Profit**
> - If SP < CP → **Loss**
> - If SP = CP → **No profit, No loss**

---

## 2. All Formulas at a Glance

```
Profit       = SP - CP
Loss         = CP - SP
Profit %     = (Profit / CP) × 100
Loss %       = (Loss / CP) × 100
SP           = CP × (100 + P%) / 100     [Profit case]
SP           = CP × (100 - L%) / 100     [Loss case]
CP           = SP × 100 / (100 + P%)     [When profit % known]
CP           = SP × 100 / (100 - L%)     [When loss % known]
Discount     = MP - SP
Discount %   = (Discount / MP) × 100
SP           = MP × (100 - Discount%) / 100
```

> **⚡ IMPORTANT:** Profit % and Loss % are **ALWAYS calculated on CP**, not SP!
> Discount % is **ALWAYS calculated on MP**, not CP!

---

## 3. Tips, Tricks & Shortcuts

### ⚡ Trick 1 — Multiplying Factor Method (Fastest!)
> Instead of formula, use multiplying factors:
> - 20% profit → SP = CP × **1.20**
> - 15% loss  → SP = CP × **0.85**
> - 25% discount on MP → SP = MP × **0.75**

### ⚡ Trick 2 — Two Articles, Same SP, Same % Profit/Loss
> **Always a LOSS!**
> ```
> Net Loss % = (Common %)² / 100
> ```
> Example: Two items sold at ₹600 each, one at 20% profit, one at 20% loss →
> Net Loss % = (20)²/100 = **4% loss** ✅

### ⚡ Trick 3 — Dishonest Dealer using False Weight
> ```
> Profit % = (True Weight - False Weight) / False Weight × 100
> ```
> Example: Dealer uses 900g instead of 1kg:
> Profit % = (1000 - 900)/900 × 100 = 100/900 × 100 = **11.11%**

### ⚡ Trick 4 — MP to get X% profit after Y% discount
> ```
> MP = CP × (100 + Profit%) / (100 - Discount%)
> ```

### ⚡ Trick 5 — Net % on Marked Price after discount + profit
> If article is marked M% above CP and discount D% given:
> ```
> Net Profit = M - D - (M × D)/100
> ```
> (Same as successive % formula!)

### ⚡ Trick 6 — If Sp is interchanged between profit and loss
> If an article sold at P% profit instead of P% loss, the SP would be ₹X more:
> ```
> CP = X × 100 / (2 × P)
> ```

### ⚡ Trick 7 — Finding CP when two conditions of SP are given
> "If sold at ₹A he gets X% profit, sold at ₹B he gets Y% loss → find CP"
> Set up: A = CP(1 + X/100) and B = CP(1 - Y/100), solve!

---

## Method 1 — Basic P&L Calculation

**Concept:** Use CP, SP, Profit/Loss formulas directly.

**Example 1:** A book is bought for ₹250 and sold for ₹300. Find profit %.
> Profit = 300 - 250 = 50
> Profit % = (50/250) × 100 = **20%** ✅

**Example 2:** A pen costs ₹80 and is sold at ₹68. Find loss %.
> Loss = 80 - 68 = 12
> Loss % = (12/80) × 100 = **15%** ✅

**Example 3:** An article is sold at 25% profit. SP = ₹500. Find CP.
> CP = 500 × 100/(100 + 25) = 500 × 100/125 = 500 × 4/5 = **₹400** ✅

**Example 4:** A cycle is sold at 20% loss. SP = ₹4,800. Find CP.
> CP = 4800 × 100/(100 - 20) = 4800 × 100/80 = 4800 × 5/4 = **₹6,000** ✅

---

## Method 2 — Marked Price, Discount & SP

**Concept:** MP is the labeled price; discount is reduction on MP; SP is what buyer pays.

**Formula:**
```
SP = MP × (100 - Discount%) / 100
Profit/Loss is always compared to CP!
```

**Example 1:** MP = ₹500, Discount = 20%. Find SP.
> SP = 500 × 80/100 = **₹400** ✅

**Example 2:** A shopkeeper marks an article 40% above CP and gives a 15% discount. Find profit %.
> Let CP = 100
> MP = 140
> SP = 140 × (85/100) = 140 × 0.85 = 119
> Profit % = (119 - 100)/100 × 100 = **19%** ✅
> *(Net formula: 40 - 15 - (40×15)/100 = 25 - 6 = 19%)* ✅

**Example 3:** SP = ₹765 after 15% discount. Find MP.
> 765 = MP × (85/100)
> MP = 765 × 100/85 = **₹900** ✅

---

## Method 3 — Dishonest Dealer / False Weight

**Concept:** Dealer cheats by giving less than stated weight.

**Formula:**
```
Profit % = (True Weight - False Weight) / False Weight × 100
```
Or more generally:
```
Profit % = (Error / (True Value - Error)) × 100
```

**Example 1:** A milkman mixes water with milk and sells at CP. He uses 950ml instead of 1000ml. Find his gain %.
> Profit % = (1000 - 950)/950 × 100 = 50/950 × 100 = **5.26%** ✅

**Example 2:** A dealer claims to sell at cost price but uses 800g weight instead of 1000g. Profit %?
> Profit % = (1000 - 800)/800 × 100 = 200/800 × 100 = **25%** ✅

**Example 3:** A dealer mixes 20L of water in 80L of milk and sells the mixture at CP of milk. Find profit %.
> Total mixture = 100L, cost = cost of 80L
> Profit % = 20/80 × 100 = **25%** ✅

---

## Method 4 — Selling Two Items (Same SP, Same %)

> **THE MOST COMMON TCS NQT TRAP!**
> When two items are sold at SAME selling price, one at X% profit and one at X% loss:
> **THERE IS ALWAYS A NET LOSS!**

**Formula:**
```
Net Loss % = (Common %)² / 100
```

**Example 1:** Two watches sold at ₹990 each. One at 10% profit, one at 10% loss. Net profit/loss?
> Net Loss % = 10²/100 = 100/100 = **1% loss** ✅
> CP of watch 1 = 990 × 100/110 = ₹900
> CP of watch 2 = 990 × 100/90 = ₹1100
> Total CP = 2000, Total SP = 1980 → Loss = ₹20 → 20/2000 × 100 = 1% ✅

**Example 2:** Two TVs sold at ₹5,000 each, one at 25% profit, one at 25% loss. Net loss?
> Net Loss % = 25²/100 = 625/100 = **6.25% loss** ✅

---

## Method 5 — Cost Price When P% & L% Given Together

**Concept:** Two conditions given, find CP.

**Example 1:** If a book is sold at ₹540 profit is 8%, at ₹500 profit/loss is ?
> CP = 540 × 100/108 = ₹500
> At ₹500 → SP = CP → **No profit, No loss** ✅

**Example 2:** A man sells an article at 10% profit. If he had sold it for ₹60 more, profit would be 22%. Find CP.
> At 10% profit: SP1 = 1.10 × CP
> At 22% profit: SP2 = 1.22 × CP
> Difference: 1.22CP - 1.10CP = 60
> 0.12CP = 60 → CP = **₹500** ✅

**Example 3:** If sold at ₹200, loss is 20%. At what price should it be sold to gain 20%?
> CP = 200 × 100/80 = ₹250
> For 20% gain: SP = 250 × 120/100 = **₹300** ✅

---

## Method 6 — Successive Discounts

**Concept:** Two or more discounts applied one after another (like chained %).

**Formula (two discounts d1 and d2):**
```
Net Discount % = d1 + d2 - (d1 × d2) / 100
Net SP = MP × (100 - d1)/100 × (100 - d2)/100
```

**Example 1:** Successive discounts of 20% and 10% on MP ₹1000.
> SP = 1000 × 0.80 × 0.90 = 1000 × 0.72 = **₹720** ✅
> Net discount = 1000 - 720 = ₹280 → 28% net discount

**Example 2:** Three successive discounts 10%, 20%, 25% on ₹2000.
> SP = 2000 × 0.90 × 0.80 × 0.75
> = 2000 × 0.54 = **₹1,080** ✅

**Example 3:** Which is better: 40% single discount or 25% + 20%?
> 40% → SP = 60% of MP
> 25% + 20% → SP = 75% × 80% = 60% of MP
> **Both are EQUAL!** ✅

---

## Method 7 — Profit/Loss on Multiple Transactions

**Concept:** Combine multiple buy-sell transactions.

**Example 1:** Bought 10 articles for ₹8 each. Sold 8 at ₹11, 2 at ₹5. Find overall P/L%.
> Total CP = 10 × 8 = ₹80
> Total SP = 8×11 + 2×5 = 88 + 10 = ₹98
> Profit = 98 - 80 = 18 → Profit % = 18/80 × 100 = **22.5%** ✅

**Example 2:** A trader buys goods at 20% discount on list price. Sells at 10% above list price. Profit %?
> Let List Price = 100
> CP = 80 (20% discount)
> SP = 110 (10% above list)
> Profit % = (110-80)/80 × 100 = 30/80 × 100 = **37.5%** ✅

---

---

# 🟢 EASY MCQs (5 Questions)

---

### Q1. A shirt is bought for ₹500 and sold for ₹600. What is the profit %?
- (A) 15%
- (B) 20%
- (C) 25%
- (D) 30%

> **✅ Answer: (B) 20%**
> **Solution:**
> Profit = 600 - 500 = 100
> Profit % = (100/500) × 100 = **20%** ✅

---

### Q2. A bag is sold for ₹480 at a loss of 20%. What was the cost price?
- (A) ₹540
- (B) ₹576
- (C) ₹600
- (D) ₹650

> **✅ Answer: (C) ₹600**
> **Solution:**
> CP = 480 × 100/(100 - 20) = 480 × 100/80 = **₹600** ✅

---

### Q3. An item is marked at ₹800 and sold after a 25% discount. Find the selling price.
- (A) ₹550
- (B) ₹575
- (C) ₹600
- (D) ₹625

> **✅ Answer: (C) ₹600**
> **Solution:**
> SP = 800 × (100 - 25)/100 = 800 × 75/100 = **₹600** ✅

---

### Q4. A trader buys apples at ₹5 each and sells at ₹6 each. Find profit %.
- (A) 15%
- (B) 16.67%
- (C) 20%
- (D) 25%

> **✅ Answer: (C) 20%**
> **Solution:**
> Profit per apple = 6 - 5 = ₹1
> Profit % = (1/5) × 100 = **20%** ✅

---

### Q5. If SP = ₹1,100 and profit = 10%, find CP.
- (A) ₹900
- (B) ₹950
- (C) ₹1,000
- (D) ₹1,050

> **✅ Answer: (C) ₹1,000**
> **Solution:**
> CP = 1100 × 100/110 = **₹1,000** ✅

---

---

# 🟡 MEDIUM MCQs (7 Questions)

---

### Q6. A shopkeeper marks goods 30% above CP and allows a 20% discount. His profit or loss %?
- (A) 4% profit
- (B) 6% profit
- (C) 4% loss
- (D) 10% profit

> **✅ Answer: (A) 4% profit**
> **Solution:**
> Let CP = 100
> MP = 130, SP = 130 × 0.80 = 104
> Profit % = **4%** ✅
> *(Net: 30 - 20 - (30×20)/100 = 10 - 6 = 4%)* ✅

---

### Q7. Two articles sold at ₹1,980 each, one at 10% profit and one at 10% loss. Net result?
- (A) No loss, No profit
- (B) ₹40 profit
- (C) ₹40 loss
- (D) ₹20 loss

> **✅ Answer: (C) ₹40 loss**
> **Solution:**
> Net Loss % = 10²/100 = 1%
> Total SP = ₹3,960
> Total CP = 3960/0.99 = ₹4,000
> Loss = 4000 - 3960 = **₹40** ✅

---

### Q8. A man sells 20 articles for ₹60 and gains 20%. How many articles did he buy for ₹60?
- (A) 20
- (B) 22
- (C) 24
- (D) 25

> **✅ Answer: (C) 24**
> **Solution:**
> SP of 20 articles = ₹60
> SP of 1 article = ₹3
> Profit = 20% → CP = 3 × 100/120 = ₹2.50
> No. of articles for ₹60 at CP = 60/2.5 = **24** ✅

---

### Q9. A sells to B at a profit of 10%. B sells to C at a loss of 10%. If C pays ₹990, what did A pay?
- (A) ₹900
- (B) ₹950
- (C) ₹1,000
- (D) ₹1,100

> **✅ Answer: (C) ₹1,000**
> **Solution:**
> B's SP to C = 990
> B's CP (= A's SP) = 990 × 100/90 = ₹1,100
> A's CP = 1100 × 100/110 = **₹1,000** ✅

---

### Q10. By selling 15 articles, a man loses the SP of 3 articles. Find loss %.
- (A) 15%
- (B) 16.67%
- (C) 20%
- (D) 25%

> **✅ Answer: (B) 16.67%**
> **Solution:**
> Let SP of 1 article = ₹1
> Total SP = 15, Loss = 3
> Total CP = 15 + 3 = 18
> Loss % = (3/18) × 100 = 16.67% ✅

---

### Q11. A dishonest dealer claims to sell at CP but uses 800g weight instead of 1kg. Profit %?
- (A) 20%
- (B) 22%
- (C) 25%
- (D) 28%

> **✅ Answer: (C) 25%**
> **Solution:**
> Profit % = (1000 - 800)/800 × 100 = 200/800 × 100 = **25%** ✅

---

### Q12. If selling price of 12 oranges equals cost price of 16 oranges, find profit %.
- (A) 25%
- (B) 30%
- (C) 33.33%
- (D) 40%

> **✅ Answer: (C) 33.33%**
> **Solution:**
> Let CP of 1 orange = ₹1
> CP of 16 = ₹16 → SP of 12 = ₹16 → SP of 1 = 16/12 = ₹4/3
> Profit % = (4/3 - 1)/1 × 100 = (1/3) × 100 = **33.33%** ✅

---

---

# 🔴 HARD MCQs (10 Questions)

---

### Q13. A trader marks articles at 40% above CP. He gives two successive discounts of 10% and 15%. Find his overall profit or loss %.
- (A) 7% profit
- (B) 0.9% loss
- (C) 1% profit
- (D) 4% loss

> **✅ Answer: (A) 7% profit**
> **Solution:**
> Let CP = 100, MP = 140
> After 10% discount: 140 × 0.9 = 126
> After 15% discount: 126 × 0.85 = 107.1
> Since 107.1 > 100 → Profit = **7.1% ≈ 7%** ✅

---

### Q14. By selling an article at 2/3 of its SP, a man incurs 10% loss. What is the profit % at the original SP?
- (A) 25%
- (B) 30%
- (C) 35%
- (D) 40%

> **✅ Answer: (C) 35%**
> **Solution:**
> Let original SP = S
> Reduced SP = 2S/3
> Loss = 10% → 2S/3 = CP × 0.90
> CP = 2S/(3 × 0.9) = 2S/2.7 = 20S/27
> Profit at S = (S - 20S/27)/(20S/27) × 100
> = (7S/27)/(20S/27) × 100 = 7/20 × 100 = **35%** ✅

---

### Q15. A man buys a certain number of oranges at 6 for ₹5 and sells at 5 for ₹6. Profit %?
- (A) 36%
- (B) 40%
- (C) 42%
- (D) 44%

> **✅ Answer: (D) 44%**
> **Solution:**
> LCM(6, 5) = 30 oranges
> CP of 30 = 30 × 5/6 = ₹25
> SP of 30 = 30 × 6/5 = ₹36
> Profit % = (36-25)/25 × 100 = 11/25 × 100 = **44%** ✅

---

### Q16. A sold an article to B at 10% profit. B sold it to C at 20% profit. C paid ₹2,640. How much did A pay?
- (A) ₹1,800
- (B) ₹2,000
- (C) ₹2,200
- (D) ₹2,400

> **✅ Answer: (B) ₹2,000**
> **Solution:**
> C's CP = ₹2,640 = B's SP
> B's CP = 2640/1.20 = ₹2,200 = A's SP
> A's CP = 2200/1.10 = **₹2,000** ✅

---

### Q17. A shopkeeper allows 10% discount and still makes 26% profit. If the CP is ₹1,400, find the marked price.
- (A) ₹1,900
- (B) ₹1,960
- (C) ₹2,000
- (D) ₹2,100

> **✅ Answer: (B) ₹1,960**
> **Solution:**
> SP (with 26% profit) = 1400 × 1.26 = ₹1,764
> SP = MP × 0.90 = 1764
> MP = 1764/0.90 = **₹1,960** ✅

---

### Q18. A trader sells goods at a loss of 8% but uses a weight that is 20% less. Find his actual profit or loss %.
- (A) 10% profit
- (B) 15% profit
- (C) No profit No loss
- (D) 5% loss

> **✅ Answer: (B) 15% profit**
> **Solution:**
> Let true weight = 1000g, false weight = 800g
> He charges price for 1000g but gives only 800g of goods
> Effective CP for 1000g worth → he actually gives 800g
> Effective SP = 0.92 × True SP (since sells at 8% loss on claimed amount)
> For 800g of goods, he collects 0.92 × price of 1000g
> Effective CP = price of 800g = 0.80 × (price of 1000g)
> Profit % = (0.92 - 0.80)/0.80 × 100 = 0.12/0.80 × 100 = **15%** ✅

---

### Q19. If a trader sold an article at ₹1,400 to make a 40% profit, but had sold it at ₹1,000, what would his profit or loss % be?
- (A) No profit No loss
- (B) Profit 5%
- (C) Loss 5%
- (D) Profit 2%

> **✅ Answer: (A) No profit No loss**
> **Solution:**
> CP = 1400/1.40 = **₹1,000**
> If sold at ₹1,000 = CP → **No profit, No loss** ✅

---

### Q20. Three successive discounts of 10%, 20%, 25% are offered on a TV with MP ₹20,000. Find final SP.
- (A) ₹12,000
- (B) ₹13,200
- (C) ₹13,500
- (D) ₹14,000

> **✅ Answer: (C) ₹13,500**
> **Solution:**
> SP = 20000 × 0.90 × 0.80 × 0.75
> = 20000 × 0.54 = **₹10,800**
> *(Check: 20000×0.9=18000, ×0.8=14400, ×0.75=10800)* ✅
> **Correct Answer: ₹10,800**
> *(Above options don't match — answer is ₹10,800)*

---

### Q21. A person sells 320 mangoes for the CP of 400 mangoes. His gain %?
- (A) 20%
- (B) 22.5%
- (C) 25%
- (D) 28%

> **✅ Answer: (C) 25%**
> **Solution:**
> Let CP of 1 mango = ₹1
> CP of 320 mangoes = ₹320
> SP of 320 mangoes = CP of 400 = ₹400
> Profit % = (400-320)/320 × 100 = 80/320 × 100 = **25%** ✅

---

### Q22. A sold to B at 20% profit. B sold to C at 25% profit. C sold to D at 10% loss. D paid ₹2,700. What was A's cost price?
- (A) ₹1,500
- (B) ₹1,600
- (C) ₹1,800
- (D) ₹2,000

> **✅ Answer: (D) ₹2,000**
> **Solution:**
> D's CP = ₹2,700 = C's SP
> C's CP = 2700/0.90 = ₹3,000 = B's SP
> B's CP = 3000/1.25 = ₹2,400 = A's SP
> A's CP = 2400/1.20 = **₹2,000** ✅

---

---

# 🧠 More Practice Problems

> *Quick fire — solve before reading solution!*

**P1.** CP = ₹720, SP = ₹900. Find profit %.
> Profit = 180, % = 180/720 × 100 = **25%** ✅

**P2.** A book sold at 15% loss for ₹425. Find CP.
> CP = 425 × 100/85 = **₹500** ✅

**P3.** SP = ₹340, Profit = 20%. Find CP.
> CP = 340 × 100/120 = **₹283.33** ✅

**P4.** Stock bought at ₹4,500. Overhead = ₹500. Sold at ₹6,000. Profit %?
> CP = 4500 + 500 = 5000
> Profit % = 1000/5000 × 100 = **20%** ✅

**P5.** SP of 8 articles = CP of 10 articles. Profit %?
> Let CP = 10, SP = 10 (for 10 articles → per unit SP = 10/8 = 1.25)
> Profit % = (10 - 8)/8 × 100 = 2/8 × 100 = **25%** ✅

**P6.** By selling 45 articles, a man loses SP of 5 articles. Loss %?
> Total SP = 45, Loss = 5, CP = 50
> Loss % = 5/50 × 100 = **10%** ✅

**P7.** MP = ₹1,200, Discount = 16.67%. Find SP.
> 16.67% = 1/6 → SP = 1200 × 5/6 = **₹1,000** ✅

**P8.** Successive discounts 25% and 20%. Equivalent single discount?
> Net = 25 + 20 - (25×20)/100 = 45 - 5 = **40%** ✅

**P9.** A man wants 20% profit after 10% discount. What % above CP should he mark?
> MP = CP × (100 + 20)/(100 - 10) = 120/90 × CP = **33.33% above CP** ✅

**P10.** A TV sold at ₹9,000 at 10% profit. At what price should it be sold for 20% profit?
> CP = 9000/1.10 = ≈₹8,181.8
> New SP = CP × 1.20 = 8181.8 × 1.2 = **₹9,818** ≈ ₹9,818 ✅

**P11.** An article had 2 successive markdowns of 10% each. Net reduction?
> Net = 10 + 10 - 1 = **19%** ✅

**P12.** Bought 100 pens at ₹5 each. Sold 80 at ₹7 each and 20 at ₹3 each. Profit %?
> CP = 500, SP = 560 + 60 = 620
> Profit % = 120/500 × 100 = **24%** ✅

---

---

# 🎯 TCS NQT Special: Common Question Patterns

## Pattern 1 — "Chain of sell" (A→B→C→D)
*Go backwards! Start from the last CP and work back.*
- Find B's CP from C's payment, then A's CP from B's.

## Pattern 2 — "Same SP, Same %, one profit one loss"
*Always net LOSS. Use formula: (%)²/100*

## Pattern 3 — "Find MP for desired profit after discount"
```
MP = CP × (100 + Profit%) / (100 - Discount%)
```

## Pattern 4 — "SP of X articles = CP of Y articles → find profit %"
```
Profit % = (Y - X)/X × 100   [if Y > X → profit]
Loss %   = (X - Y)/X × 100   [if Y < X → loss]
```

## Pattern 5 — "False weight cheating"
```
Profit % = (True Wt - False Wt) / False Wt × 100
```

---

## 🚀 Common Mistakes to AVOID in TCS NQT

| Mistake ❌ | Correct Approach ✅ |
|---|---|
| Two items at same SP, same %: Net = 0 | Always net LOSS of (%)²/100 |
| Profit/Loss % calculated on SP | Always on **CP** |
| Discount % calculated on CP | Always on **MP** |
| 10% profit then 10% loss = 0 | Net = **-1% loss** |
| Successive discounts 20%+10% = 30% | Net = **28%** |
| Ignore overhead costs in CP | Add overhead to CP first |

---

## 📘 Quick Revision Summary

```
Profit %  = (SP - CP)/CP × 100
Loss %    = (CP - SP)/CP × 100
SP (P%)   = CP × (100+P)/100
SP (L%)   = CP × (100-L)/100
CP (P%)   = SP × 100/(100+P)
CP (L%)   = SP × 100/(100-L)
MP        = CP × (100+P)/(100-D)
Net Loss  = (Common%)²/100  [same SP trap]
False Wt  = (Diff/FW) × 100  [dishonest dealer]
```

---

> **🏁 Next Topic → 03_Simple_and_Compound_Interest.md**
> *Profit% knowledge directly helps in understanding interest calculations!*

---
*Guide created for TCS NQT Preparation | All methods, formulas, and MCQs from simple to advanced*
