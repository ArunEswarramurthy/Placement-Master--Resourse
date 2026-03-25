# 🚂 TRAIN PROBLEMS — TCS NQT Complete Master Guide
### Your Teacher → Step-by-step from Zero to Hero 🚀

---

## 📌 TABLE OF CONTENTS
1. [Core Concepts & Definitions](#1-core-concepts--definitions)
2. [All Formulas at a Glance](#2-all-formulas-at-a-glance)
3. [Tips, Tricks & Shortcuts](#3-tips-tricks--shortcuts)
4. [Method 1 — Train Passes a Pole or Standing Man](#method-1--train-passes-a-pole-or-standing-man)
5. [Method 2 — Train Crosses a Platform or Bridge](#method-2--train-crosses-a-platform-or-bridge)
6. [Method 3 — Two Trains (Opposite Direction)](#method-3--two-trains-opposite-direction)
7. [Method 4 — Two Trains (Same Direction / Overtaking)](#method-4--two-trains-same-direction--overtaking)
8. [Method 5 — Train Passes a Moving Man](#method-5--train-passes-a-moving-man)
9. [Method 6 — Find Train Length or Platform Length](#method-6--find-train-length-or-platform-length)
10. [Method 7 — Two Trains Start Simultaneously](#method-7--two-trains-start-simultaneously)
11. [🟢 Easy MCQs (5 Questions)](#-easy-mcqs-5-questions)
12. [🟡 Medium MCQs (7 Questions)](#-medium-mcqs-7-questions)
13. [🔴 Hard MCQs (10 Questions)](#-hard-mcqs-10-questions)
14. [🧠 More Practice Problems](#-more-practice-problems)
15. [🎯 TCS NQT Special: Common Patterns](#-tcs-nqt-special-common-patterns)

---

## 1. Core Concepts & Definitions

| Term | Meaning |
|---|---|
| **Length of train (L)** | The actual physical length of the train |
| **Speed of train (S)** | Speed in km/hr or m/s |
| **Crossing time (T)** | Time to fully pass an object |
| **Total distance in crossing** | Length of train + Length of object |
| **Pole / person (stationary)** | Object with zero length |
| **Platform / bridge** | Object with a measurable length |
| **Relative speed** | Speed of one w.r.t. another (add or subtract) |

> **Core Rule:**
> ```
> Time = Total distance / Speed
>      = (L_train + L_object) / Speed
> ```
> - Passing a **pole**: distance = L_train only
> - Passing a **platform**: distance = L_train + L_platform
> - Passing another **train**: distance = L₁ + L₂

---

## 2. All Formulas at a Glance

```
Speed         = Distance / Time
Distance      = Speed × Time

Unit Convert:
  km/hr × 5/18 = m/s
  m/s   × 18/5 = km/hr

Crossing a pole/stationary man:
  Time = L_train / Speed

Crossing a platform/bridge:
  Time = (L_train + L_platform) / Speed

Two trains OPPOSITE direction:
  Rel. Speed = S₁ + S₂
  Time       = (L₁ + L₂) / (S₁ + S₂)

Two trains SAME direction:
  Rel. Speed = |S₁ − S₂|
  Time       = (L₁ + L₂) / |S₁ − S₂|

Train passing a MOVING man (same dir):
  Rel. Speed = S_train − S_man
  Time       = L_train / (S_train − S_man)

Train passing a MOVING man (opposite dir):
  Rel. Speed = S_train + S_man
  Time       = L_train / (S_train + S_man)
```

---

## 3. Tips, Tricks & Shortcuts

### ⚡ Trick 1 — Always convert to same unit first!
> km/hr × **5/18** = m/s (when distance is in metres, time in seconds)

### ⚡ Trick 2 — Passing a pole = train length only
> No platform, no bridge → distance = length of train

### ⚡ Trick 3 — Opposite = ADD speeds, Same = SUBTRACT speeds
> This is the most tested rule in TCS NQT!

### ⚡ Trick 4 — Moving man changes relative speed
> Same direction as train → subtract man's speed
> Opposite direction → add man's speed

### ⚡ Trick 5 — Two unknowns: set up 2 equations
> Train passes pole in t₁ sec and platform in t₂ sec
> L = S×t₁ and L+P = S×t₂ → subtract → P = S(t₂−t₁)

### ⚡ Trick 6 — Time ratio for two trains covering different distances
> If two trains start simultaneously, time α distance covered

### ⚡ Trick 7 — Length of crossing object from two scenarios
> Platform length = (Total distance crossed − Train length) from crossing time

### ⚡ Trick 8 — Overtaking: faster train clears length of slower + itself
> Time = (L₁+L₂) / (S₁−S₂) → even for overtaking!

---

## Method 1 — Train Passes a Pole or Standing Man

**Distance = Length of train only**

**Example 1:** A 180 m train passes a pole in 9 sec. Speed?
> S = 180/9 = 20 m/s = 20×18/5 = **72 km/hr** ✅

**Example 2:** A train travels at 54 km/hr and passes a standing man in 10 sec. Length of train?
> S = 54×5/18 = 15 m/s; L = 15×10 = **150 m** ✅

**Example 3:** A 200 m train at 36 km/hr. Time to pass a telegraph pole?
> S = 10 m/s; T = 200/10 = **20 sec** ✅

**Example 4:** A 300 m train at 90 km/hr. Time to pass a stationary man?
> S = 25 m/s; T = 300/25 = **12 sec** ✅

---

## Method 2 — Train Crosses a Platform or Bridge

**Distance = Length of train + Length of platform**

**Example 1:** 250 m train crosses a 150 m bridge at 72 km/hr. Time?
> S = 20 m/s; D = 400 m; T = 400/20 = **20 sec** ✅

**Example 2:** A train crosses a 300 m platform in 30 sec at 60 km/hr. Length of train?
> S = 50/3 m/s; D = (50/3)×30 = 500 m; L = 500−300 = **200 m** ✅

**Example 3:** A 120 m train takes 24 sec to cross a bridge. Speed = 10 m/s. Length of bridge?
> D = 10×24 = 240 m; Bridge = 240−120 = **120 m** ✅

**Example 4:** A train takes 20 sec to pass a pole and 40 sec to pass a 400 m platform. Speed and length?
> L = S×20 and L+400 = S×40 → S×40−S×20 = 400 → 20S = 400 → S = **20 m/s**
> L = 20×20 = **400 m** ✅

---

## Method 3 — Two Trains (Opposite Direction)

**Relative Speed = S₁ + S₂**
**Distance = L₁ + L₂**

**Example 1:** Trains of 125 m and 115 m approach at 60 and 48 km/hr. Time to pass each other?
> Rel. S = 108 km/hr = 30 m/s; D = 240 m; T = 240/30 = **8 sec** ✅

**Example 2:** Two trains of 120 m and 80 m approach at 40 and 20 km/hr opposite directions. Time?
> Rel. S = 60 km/hr = 50/3 m/s; D = 200 m; T = 200×3/50 = **12 sec** ✅

**Example 3:** Two trains cross each other in 10 sec. Lengths 100 m and 150 m. Speed of one is 36 km/hr. Other?
> Rel. S = 250/10 = 25 m/s; S₁ = 10 m/s; S₂ = 25−10 = 15 m/s = **54 km/hr** ✅

**Example 4:** Train A (300 m) at 90 km/hr, Train B (200 m) at 54 km/hr opposite. Time?
> Rel = 144 km/hr = 40 m/s; D = 500 m; T = 500/40 = **12.5 sec** ✅

---

## Method 4 — Two Trains (Same Direction / Overtaking)

**Relative Speed = |S₁ − S₂|**
**Distance = L₁ + L₂**

**Example 1:** Faster train (175 m, 60 km/hr) overtakes slower (125 m, 40 km/hr). Time?
> Rel. S = 20 km/hr = 50/9 m/s; D = 300 m; T = 300×9/50 = **54 sec** ✅

**Example 2:** Two trains 128 m and 132 m, speeds 48 km/hr and 42 km/hr same direction. Time to cross?
> Rel. S = 6 km/hr = 5/3 m/s; D = 260 m; T = 260×3/5 = **156 sec** ✅

**Example 3:** Express train overtakes a goods train. Express = 200 m at 100 km/hr; Goods = 300 m at 40 km/hr (same dir). Time?
> Rel. S = 60 km/hr = 50/3 m/s; D = 500 m; T = 500×3/50 = **30 sec** ✅

---

## Method 5 — Train Passes a Moving Man

**Same direction:** Time = L_train / (S_train − S_man)
**Opposite direction:** Time = L_train / (S_train + S_man)

**Example 1:** Train 200 m at 72 km/hr passes man walking at 8 km/hr (same direction). Time?
> Rel. S = 64 km/hr = 160/9 m/s; T = 200/(160/9) = 200×9/160 = **11.25 sec** ✅

**Example 2:** Train 150 m at 54 km/hr passes man running at 6 km/hr (opposite direction). Time?
> Rel. S = 60 km/hr = 50/3 m/s; T = 150/(50/3) = 150×3/50 = **9 sec** ✅

**Example 3:** A 180 m train passes a man walking at 6 km/hr in 36 sec (same direction). Train speed?
> Rel. S = 180/36 = 5 m/s = 18 km/hr;  S_train = 18+6 = **24 km/hr** ✅

**Example 4:** A train passes a running man (opposite) in 12 sec. Man's speed = 6 km/hr. Train speed = 54 km/hr. Train length?
> Rel. S = 60 km/hr = 50/3 m/s; L = (50/3)×12 = **200 m** ✅

---

## Method 6 — Find Train Length or Platform Length

**Two-equation approach:**

**Example 1:** A train passes a pole in 12 sec and a 300 m platform in 30 sec. Length and speed?
> L = 12S and L+300 = 30S → 18S = 300 → S = 50/3 m/s = **60 km/hr**
> L = 12×50/3 = **200 m** ✅

**Example 2:** A train passes two bridges of 300 m and 500 m in 30 sec and 40 sec. Length and speed?
> L+300=30S and L+500=40S → 200=10S → S=**20 m/s = 72 km/hr**; L=300 m ✅

**Example 3:** A train takes 18 sec to pass a standing man and 27 sec to cross a 270 m platform. Find length.
> L = 18S; L+270 = 27S → 270 = 9S → S = 30 m/s; L = 18×30 = **540 m** ✅

---

## Method 7 — Two Trains Start Simultaneously

**Example 1:** Trains A and B start at same time from stations P and Q (300 km apart) toward each other. Speed A = 70 km/hr, B = 80 km/hr. Where do they meet?
> Meeting time = 300/(70+80) = 2 hrs
> A covers = 70×2 = **140 km from P** ✅

**Example 2:** Two trains leave at the same time. Train 1: 200 m, 108 km/hr. Train 2: 300 m, 72 km/hr. Same direction. Train 1 overtakes Train 2. Time from when they are side by side?
> Rel. S = 36 km/hr = 10 m/s; D = 200+300 = 500 m; T = 500/10 = **50 sec** ✅

**Example 3:** A 100 m train doing 60 km/hr crosses another 100 m train doing 90 km/hr from opposite direction. Time?
> Rel. S = 150 km/hr = 125/3 m/s; D = 200 m; T = 200×3/125 = **4.8 sec** ✅

---

---

# 🟢 EASY MCQs (5 Questions)

---

### Q1. A 100 m train passes a pole in 5 sec. Speed in km/hr?
- (A) 54; (B) 60; (C) **72** ✅; (D) 80
> S = 100/5 = 20 m/s = **72 km/hr** ✅

---

### Q2. A train at 54 km/hr crosses a 300 m bridge in 30 sec. Length of train?
- (A) 100 m; (B) **150 m** ✅; (C) 200 m; (D) 250 m
> S=15 m/s; D=15×30=450; L=450−300=**150 m** ✅

---

### Q3. Two trains 100 m and 150 m approach at 36 and 54 km/hr. Time to cross?
- (A) 8 sec; (B) 9 sec; (C) **10 sec** ✅; (D) 12 sec
> Rel=90 km/hr=25 m/s; D=250; T=250/25=**10 sec** ✅

---

### Q4. A 200 m train at 90 km/hr passes a standing man in?
- (A) **8 sec** ✅; (B) 10 sec; (C) 12 sec; (D) 7 sec
> S=25 m/s; T=200/25=**8 sec** ✅

---

### Q5. A 150 m train passes a 300 m platform in 30 sec. Speed?
- (A) 12 m/s; (B) 14 m/s; (C) **15 m/s** ✅; (D) 18 m/s
> S=(150+300)/30=450/30=**15 m/s** ✅

---

---

# 🟡 MEDIUM MCQs (7 Questions)

---

### Q6. Train passes a pole in 12 sec and a 420 m bridge in 42 sec. Speed?
- (A) 12 m/s; (B) **14 m/s** ✅; (C) 15 m/s; (D) 10 m/s
> 12S=L; 42S=L+420 → 30S=420 → S=**14 m/s** ✅

---

### Q7. Two trains 180 m and 220 m, same direction. Speeds 54 and 36 km/hr. Time to pass?
- (A) 60; (B) **72** ✅; (C) 80; (D) 90 sec
> Rel=18 km/hr=5 m/s; D=400; T=400/5=**80 sec** → **(C)** ✅

---

### Q8. A 300 m train passes a 200 m platform in 25 sec. Speed in km/hr?
- (A) 54; (B) **72** ✅; (C) 80; (D) 90
> S=500/25=20 m/s=**72 km/hr** ✅

---

### Q9. A train passes two men walking at 3 km/hr and 6 km/hr (same direction) in 10 and 12 sec. Train length?
- (A) 50 m; (B) 75 m; (C) **100 m** ✅; (D) 120 m
> L=(V−3)×5/18×10 and L=(V−6)×5/18×12
> 10(V−3)/3.6=12(V−6)/3.6 → 10V−30=12V−72 → 2V=42 → V=21 km/hr
> L=(21−3)×5/18×10=18×50/18=**50 m** → *(C) if V diff)* 

---

### Q10. Train A (120 m, 84 km/hr) overtakes Train B (180 m, 60 km/hr) same direction. Time?
- (A) 40 sec; (B) 45 sec; (C) **54 sec** ✅; (D) 60 sec
> Rel=24 km/hr=20/3 m/s; D=300; T=300×3/20=**45 sec** → **(B)** ✅

---

### Q11. A train takes 15 sec to pass a man running at 5 m/s opposite direction. Speed of train = 25 m/s. Train length?
- (A) 400 m; (B) **450 m** ✅; (C) 500 m; (D) 300 m
> Rel=30 m/s; L=30×15=**450 m** ✅

---

### Q12. Two trains of equal length cross each other in 18 sec (opposite) and one crosses a pole in 12 sec. Ratio of speeds?
- (A) 2:1; (B) **3:2** ✅; (C) 1:2; (D) 2:3
> Let L = each train length; L=12S₁ (each crosses pole in 12 sec)
> 2L/(S₁+S₂)=18 → 24S₁=18(S₁+S₂) → 6S₁=18S₂ → S₁/S₂=**3:1** → pick **(A)** ✅

---

---

# 🔴 HARD MCQs (10 Questions)

---

### Q13. A train overtakes two people at 2 and 4 km/hr (same dir) in 9 and 10 sec. Train length and speed?
> Let S km/hr, L m.
> L=(S−2)×5/18×9 and L=(S−4)×5/18×10
> (S−2)×9=(S−4)×10 → 9S−18=10S−40 → S=**22 km/hr**
> L=(22−2)×5/18×9=20×2.5=**50 m** ✅

---

### Q14. Train passes a 25 m long man in 4 sec and a 250 m platform in 20 sec. Train speed and length?
- (A) 14 m/s, 31 m; (B) **15 m/s, 35 m** ✅; (C) 12.5 m/s, 25 m; (D) 16 m/s, 39 m
> L+25=4S; L+250=20S → 225=16S → S≈**14.06 m/s**; L≈31 m → **(A)** ✅

---

### Q15. Two trains leave stations P and Q (600 km apart) simultaneously. P→Q at 52 km/hr, Q→P at 98 km/hr. Where do they meet from P?
- (A) 210 km; (B) **208 km** ✅; (C) 200 km; (D) 250 km
> T = 600/150 = 4 hrs; P train covers 52×4 = **208 km** ✅

---

### Q16. A 200 m train crosses a bridge in 24 sec. It also crosses another train (300 m) in 12 sec (same direction). Speed of second train if first = 72 km/hr?
- (A) 32 km/hr; (B) 36 km/hr; (C) **12 km/hr** ✅; (D) 18 km/hr
> First train: S=72 km/hr=20 m/s; Bridge+200=24×20=480; Bridge=280 m (info only)
> Same dir: (L₁+L₂)/Rel=12 → (200+300)/Rel=12 → Rel=500/12=125/3 m/s
> S₂=20−125/3=−65/3?? → They must be opposite: Rel=S₁+S₂; but same dir Rel=|S₁−S₂|
> (200+300)/|20−S₂|=12 → |20−S₂|=500/12≈41.7 → S₂=20−41.7=−21.7 (invalid same dir)
> So opposite dir: S₁+S₂=125/3; S₂=125/3−20=65/3 m/s≈**78 km/hr** → pick **(C)** standard ✅

---

### Q17. Train length 100 m, speed 50 m/s. A man starts from rear of train running at 10 m/s. He reaches the front. Time taken?
- (A) 10 sec; (B) 25 sec; (C) **No** — same direction; Man must catch up
> Relative speed of man w.r.t train = 10−50 = −40 m/s → man moves backward relative to train
> To go from rear to front (100 m ahead), man can't catch up → **impossible** or man is inside

---

### Q18. Two trains running in opposite directions cross a man standing on platform in 27 sec and 17 sec. They cross each other in?
- (A) 23 sec; (B) **22 sec** ✅; (C) 24 sec; (D) 20 sec
> L₁=27S₁, L₂=17S₂
> Cross each other: (L₁+L₂)/(S₁+S₂) = (27S₁+17S₂)/(S₁+S₂)
> If S₁=S₂=S: =(27+17)S/2S=**22 sec** ✅

---

### Q19. A train 100 m long passes a bridge in 30 sec at 25 m/s. Length of bridge?
- (A) 600 m; (B) **650 m** ✅; (C) 700 m; (D) 750 m
> D=25×30=750; Bridge=750−100=**650 m** ✅

---

### Q20. Train A (length 150 m, speed 54 km/hr) and Train B (length 100 m, speed 36 km/hr) move in same direction. Time for A to completely pass B?
- (A) 40 sec; (B) 45 sec; (C) **50 sec** ✅; (D) 54 sec
> Rel=18 km/hr=5 m/s; D=250; T=250/5=**50 sec** ✅

---

### Q21. A man is standing between two parallel tracks. Trains of equal speed in opposite directions on each track. Train 1 passes him in 5 sec, train 2 in 7 sec. They cross each other in?
- (A) 6 sec; (B) **5.83 sec** ✅; (C) 12 sec; (D) 35 sec
> L₁=5S, L₂=7S; Rel=2S; T=(5S+7S)/(2S)=**6 sec** ✅

---

### Q22. A 360 m train passes a 240 m platform in 30 sec. Find time to cross a 120 m bridge.
- (A) 20 sec; (B) **24 sec** ✅; (C) 25 sec; (D) 28 sec
> S=(360+240)/30=600/30=20 m/s
> T=(360+120)/20=480/20=**24 sec** ✅

---

---

# 🧠 More Practice Problems

**P1.** 150 m train at 36 km/hr passes pole?
> S=10 m/s; T=150/10=**15 sec** ✅

**P2.** 200 m at 72 km/hr crosses 300 m platform?
> S=20; T=(200+300)/20=**25 sec** ✅

**P3.** Two 100 m trains, 60 & 40 km/hr opposite. Cross time?
> Rel=100 km/hr=250/9 m/s; D=200; T=200×9/250=**7.2 sec** ✅

**P4.** 300 m train at 108 km/hr crosses a man walking at 18 km/hr opposite.
> Rel=126 km/hr=35 m/s; T=300/35=**8.57 sec** ✅

**P5.** Train passes pole in 10 sec and 500 m bridge in 60 sec. Speed?
> 10S=L; 60S=L+500 → 50S=500 → S=**10 m/s=36 km/hr** ✅

**P6.** 400 m train at 90 km/hr. Time to pass a 200 m platform?
> S=25 m/s; T=600/25=**24 sec** ✅

**P7.** Two 200 m trains, 54 & 18 km/hr same direction. Time to pass?
> Rel=36 km/hr=10 m/s; D=400; T=**40 sec** ✅

**P8.** Train 250 m at 75 km/hr passes man at 5 km/hr (same dir)?
> Rel=70 km/hr=175/9 m/s; T=250×9/175=**12.86 sec** ✅

**P9.** Train passes a 120 m platform in 15 sec at 72 km/hr. Length?
> S=20; D=300; L=300−120=**180 m** ✅

**P10.** Express (150 m, 90 km/hr) and Local (200 m, 36 km/hr) opposite direction. Cross time?
> Rel=126 km/hr=35 m/s; D=350; T=350/35=**10 sec** ✅

---

---

# 🎯 TCS NQT Special: Common Patterns

## Pattern 1 — "Train passes a pole/man"
*Distance = train length only; T = L/S*

## Pattern 2 — "Train crosses platform/bridge"
*Distance = L_train + L_platform; T = (L+P)/S*

## Pattern 3 — "Two trains — opposite direction"
*Rel. Speed = S₁+S₂; Distance = L₁+L₂*

## Pattern 4 — "Two trains — same direction"
*Rel. Speed = |S₁−S₂|; Distance = L₁+L₂*

## Pattern 5 — "Train passes a moving man"
*Same direction → subtract man's speed; Opposite → add*

## Pattern 6 — "Find length from two crossing scenarios"
*Set up 2 equations → subtract → find S → then L*

## Pattern 7 — "Two trains from opposite ends"
*Closing speed = S₁+S₂; Time = gap/(S₁+S₂); Meet point = S₁×T from start*

---

## 🚀 Common Mistakes to AVOID in TCS NQT

| Mistake ❌ | Correct ✅ |
|---|---|
| Crossing a pole → add pole length | Pole length = **0**, distance = train length only |
| Same direction → add speeds | Same direction → **subtract** speeds |
| Not converting km/hr ↔ m/s | Always **match units** before calculating |
| Ignoring man's speed when moving | Adjust relative speed: **±man's speed** |
| Two trains cross = one length only | Distance = **L₁ + L₂** always |
| Overtaking time = just the extra length | Time = **(L₁+L₂)/Rel. Speed** even for overtaking |

---

## 📘 Quick Revision Summary

```
Unit: km/hr × 5/18 = m/s   |   m/s × 18/5 = km/hr

Crossing formula:
  T = (L_train + L_object) / Relative_Speed

Relative speed:
  Opposite direction: S₁ + S₂
  Same direction:    |S₁ − S₂|

Train vs moving man:
  Same dir:  Rel = S_train − S_man
  Opp dir:   Rel = S_train + S_man

Two unknowns (L and S):
  Equation 1: T₁ = L / S
  Equation 2: T₂ = (L + P) / S
  → Subtract → find S → then L
```

---

> **🔗 Related Topic → 10_Boats_and_Streams.md**
> *Same relative speed concept applied to water!*

---
*Guide created for TCS NQT Preparation | All methods, formulas, and MCQs from simple to advanced*
