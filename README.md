# Design and Analysis of Algorithms (DAA) — Complete Guide

> A structured, in-depth guide to **Designing and Analyzing Algorithms** — from mathematical foundations to advanced algorithm design paradigms.
> Every topic includes theory, proof intuition, visual examples, JavaScript implementations, and curated problems.

---

## 📌 Table of Contents

| # | Topic | Category |
|---|-------|----------|
| 1 | [Mathematical Foundations](#1-mathematical-foundations) | 🟢 Foundation |
| 2 | [Asymptotic Analysis — Big O, Θ, Ω](#2-asymptotic-analysis--big-o-θ-ω) | 🟢 Foundation |
| 3 | [Recurrence Relations](#3-recurrence-relations) | 🟢 Foundation |
| 4 | [Divide and Conquer](#4-divide-and-conquer) | 🟡 Paradigm |
| 5 | [Greedy Method](#5-greedy-method) | 🟡 Paradigm |
| 6 | [Dynamic Programming](#6-dynamic-programming) | 🟡 Paradigm |
| 7 | [Backtracking](#7-backtracking) | 🟡 Paradigm |
| 8 | [Branch and Bound](#8-branch-and-bound) | 🟠 Advanced |
| 9 | [Graph Algorithms — Design & Analysis](#9-graph-algorithms--design--analysis) | 🟠 Advanced |
| 10 | [Sorting Algorithms — Deep Dive](#10-sorting-algorithms--deep-dive) | 🟠 Advanced |
| 11 | [String Matching Algorithms](#11-string-matching-algorithms) | 🟠 Advanced |
| 12 | [Complexity Theory — P, NP, NP-Hard](#12-complexity-theory--p-np-np-hard) | 🔴 Theory |
| 13 | [Approximation Algorithms](#13-approximation-algorithms) | 🔴 Theory |
| 14 | [Randomized Algorithms](#14-randomized-algorithms) | 🔴 Theory |
| 15 | [Amortized Analysis](#15-amortized-analysis) | 🔴 Theory |

---

## 🧠 What is DAA?

**Design and Analysis of Algorithms** is the study of:

```
DESIGN    →  Creating efficient algorithms for a given problem
ANALYSIS  →  Mathematically proving how fast and memory-efficient they are
```

```
Three fundamental questions DAA answers:
─────────────────────────────────────────────────────
1. CORRECTNESS  — Does the algorithm always give the right answer?
2. EFFICIENCY   — How fast does it run? How much memory does it use?
3. OPTIMALITY   — Can we prove no algorithm can do better?
```

### Why DAA matters beyond coding interviews:

```
Software Engineering  →  Choosing the right algorithm for production systems
Research              →  Proving new algorithms are correct and efficient
Competitive Programming → Solving problems within strict time limits
System Design         →  Making architectural decisions based on complexity
Academia              →  Foundation of Computer Science theory
```

---

## 1. Mathematical Foundations

### 🔑 Key Mathematical Tools Used in DAA

Before analyzing algorithms, you need these mathematical building blocks:

---

### 1.1 Logarithms

```
Definition: log_b(n) = x  means  b^x = n

Common bases in algorithms:
  log₂(n)  — binary search, merge sort (halving)
  log₁₀(n) — digit-based algorithms
  ln(n)    — natural log, used in probability analysis

Key identities:
  log(ab)   = log(a) + log(b)
  log(a/b)  = log(a) - log(b)
  log(aⁿ)   = n × log(a)
  log_b(n)  = log(n) / log(b)   ← change of base

For algorithms, we usually write log n (base 2 implied):
  log₂(1024) = 10   →  binary search on 1024 elements takes 10 steps
  log₂(10⁶)  ≈ 20   →  binary search on 1 million takes only 20 steps!
```

---

### 1.2 Summations

```
Arithmetic series (1 + 2 + 3 + ... + n):
  Σ i = n(n+1)/2  ≈  n²/2  →  O(n²)

Geometric series (1 + 2 + 4 + ... + 2ⁿ):
  Σ 2ⁱ = 2ⁿ⁺¹ - 1  →  O(2ⁿ)

Harmonic series (1 + 1/2 + 1/3 + ... + 1/n):
  Σ 1/i ≈ ln(n)  →  O(log n)

Why this matters:
  Nested loop from 1 to n → n(n+1)/2 iterations → O(n²)
  Merge sort work per level → n operations for log n levels → O(n log n)
```

---

### 1.3 Proof Techniques Used in DAA

```
1. Proof by Induction
   Base case:   Prove true for n=1
   Inductive step: Assume true for n=k, prove for n=k+1
   Used for:    Proving correctness of recursive algorithms

2. Proof by Contradiction
   Assume the opposite is true → derive a contradiction
   Used for:    Proving lower bounds, optimality of greedy

3. Proof by Loop Invariant
   State a property that is true before, during, after every loop iteration
   Used for:    Proving iterative algorithm correctness (e.g., Insertion Sort)

4. Amortized Analysis
   Average cost over a sequence of operations (even if some are expensive)
   Used for:    Dynamic arrays, Union-Find, Splay Trees
```

---

### 1.4 Recurrences Preview

```
T(n) = aT(n/b) + f(n)

where:
  a = number of subproblems
  n/b = size of each subproblem
  f(n) = work done outside recursive calls

Examples:
  Binary Search:  T(n) = T(n/2) + O(1)       → O(log n)
  Merge Sort:     T(n) = 2T(n/2) + O(n)      → O(n log n)
  Strassen:       T(n) = 7T(n/2) + O(n²)     → O(n^2.807)
```

---

## 2. Asymptotic Analysis — Big O, Θ, Ω

### 🔑 The Three Notations

```
O(g(n))  — Upper Bound     →  algorithm runs AT MOST this fast (worst case)
Ω(g(n))  — Lower Bound     →  algorithm runs AT LEAST this fast (best case)
Θ(g(n))  — Tight Bound     →  algorithm runs EXACTLY this fast (both match)
```

### 📐 Visual — What They Mean

```
Actual running time: T(n)

O(g(n)):  T(n) ≤ c × g(n)   for all n ≥ n₀
          T(n) is bounded ABOVE by c×g(n)

Ω(g(n)):  T(n) ≥ c × g(n)   for all n ≥ n₀
          T(n) is bounded BELOW by c×g(n)

Θ(g(n)):  c₁×g(n) ≤ T(n) ≤ c₂×g(n)   for all n ≥ n₀
          T(n) is sandwiched between two constants × g(n)

Example — Merge Sort:
  Worst case:  O(n log n)   ← always bounded above by c×n×log n
  Best case:   Ω(n log n)   ← always bounded below by c×n×log n
  Tight bound: Θ(n log n)   ← both match, so tight bound exists
```

### 📊 Asymptotic Hierarchy

```
O(1) ⊂ O(log n) ⊂ O(√n) ⊂ O(n) ⊂ O(n log n) ⊂ O(n²) ⊂ O(n³) ⊂ O(2ⁿ) ⊂ O(n!)
      faster ←──────────────────────────────────────────────────────→ slower
```

### 🧩 Rules for Asymptotic Analysis

```javascript
// Rule 1 — Drop constants
// 5n² + 3n + 100 → O(n²)
function example(n) {
    let count = 0;
    for (let i = 0; i < 5 * n; i++) count++;  // O(5n) = O(n)
    return count;
}

// Rule 2 — Keep dominant term only
// O(n² + n log n + n) → O(n²)

// Rule 3 — Sequential steps ADD
// O(n) + O(n²) = O(n²)
function sequential(arr) {
    arr.sort((a, b) => a - b);              // O(n log n)
    for (let i = 0; i < arr.length; i++) { // O(n)
        console.log(arr[i]);
    }
    // Total: O(n log n) + O(n) = O(n log n)
}

// Rule 4 — Nested steps MULTIPLY
// O(n) × O(n) = O(n²)
function nested(n) {
    for (let i = 0; i < n; i++) {         // O(n)
        for (let j = 0; j < n; j++) {     // O(n)
            console.log(i, j);             // O(1)
        }
    }
    // Total: O(n × n × 1) = O(n²)
}
```

### Lower Bounds — Why They Matter

```
Lower bound for comparison-based sorting = Ω(n log n)

Proof (Decision Tree argument):
  Any sorting algorithm must distinguish between n! possible orderings.
  A binary decision tree must have height ≥ log₂(n!) ≈ n log n.
  → No comparison-based sort can beat O(n log n). Merge Sort is OPTIMAL.

This means:
  If you find an O(n log n) sort → it is asymptotically optimal.
  If someone claims O(n) comparison sort → it's WRONG by proof.
  (Unless they use non-comparison techniques like Counting Sort)
```

---

## 3. Recurrence Relations

### 🔑 What is a Recurrence Relation?

A recurrence expresses the running time of a **recursive algorithm** in terms of smaller inputs.

```
T(n) = work done at current level + work done in recursive calls
```

### Method 1 — Substitution Method

Guess the solution, then prove it by induction.

```
Example: T(n) = 2T(n/2) + n

Guess: T(n) = O(n log n)

Proof by induction:
  Assume T(k) ≤ c × k × log(k) for all k < n

  T(n) = 2T(n/2) + n
       ≤ 2 × c × (n/2) × log(n/2) + n
       = c × n × (log n - 1) + n
       = c × n × log n - cn + n
       ≤ c × n × log n   (when c ≥ 1)

  ✅ Proved: T(n) = O(n log n)
```

---

### Method 2 — Recursion Tree Method

Draw the recursion as a tree, sum work at each level.

```
T(n) = 2T(n/2) + n   (Merge Sort)

Level 0:          n              work = n
Level 1:      n/2  n/2           work = n/2 + n/2 = n
Level 2:   n/4 n/4 n/4 n/4      work = n
...
Level log n:  1 1 1 ... 1        work = n

Total levels = log n
Work per level = n
Total = n × log n = O(n log n) ✅
```

---

### Method 3 — Master Theorem

The most powerful method. Directly solves T(n) = aT(n/b) + f(n).

```
T(n) = aT(n/b) + f(n)

where a ≥ 1, b > 1, f(n) asymptotically positive

Compare f(n) with n^(log_b a):

Case 1: f(n) = O(n^(log_b(a) - ε))  for some ε > 0
        → T(n) = Θ(n^log_b(a))
        → Recursive work dominates

Case 2: f(n) = Θ(n^log_b(a))
        → T(n) = Θ(n^log_b(a) × log n)
        → Both contribute equally

Case 3: f(n) = Ω(n^(log_b(a) + ε))  for some ε > 0
        → T(n) = Θ(f(n))
        → Non-recursive work dominates
```

### Master Theorem Examples

```
Algorithm          Recurrence              Analysis           Result
──────────────────────────────────────────────────────────────────────
Binary Search      T(n) = T(n/2) + O(1)   a=1,b=2,f=O(1)
                                           n^log₂(1)=n⁰=1
                                           f=Θ(1)=Θ(n⁰) → Case 2  → O(log n)

Merge Sort         T(n) = 2T(n/2) + O(n)  a=2,b=2,f=O(n)
                                           n^log₂(2)=n¹=n
                                           f=Θ(n) → Case 2         → O(n log n)

Strassen Matrix    T(n) = 7T(n/2) + O(n²) a=7,b=2,f=O(n²)
                                           n^log₂(7)≈n^2.807
                                           f=O(n^(2.807-ε)) → Case 1 → O(n^2.807)

Binary Tree DFS    T(n) = 2T(n/2) + O(1)  a=2,b=2,f=O(1)
                                           n^log₂(2)=n
                                           f=O(n^(1-ε)) → Case 1   → O(n)
```

---

## 4. Divide and Conquer

### 🔑 Concept

Split the problem into **smaller subproblems**, solve them **recursively**, and **combine** the results.

```
Divide:   Break problem into a subproblems of size n/b
Conquer:  Solve each subproblem recursively
Combine:  Merge solutions of subproblems into final answer

Template:
  if (base case) → solve directly
  else:
    divide into subproblems
    recursively solve each
    combine results
```

### 📐 Classic Divide & Conquer Algorithms

---

#### 4.1 Merge Sort — O(n log n)

```javascript
function mergeSort(arr) {
    if (arr.length <= 1) return arr;           // base case

    const mid = Math.floor(arr.length / 2);
    const left  = mergeSort(arr.slice(0, mid)); // conquer left
    const right = mergeSort(arr.slice(mid));    // conquer right

    return merge(left, right);                  // combine
}

function merge(left, right) {
    const result = [];
    let i = 0, j = 0;

    while (i < left.length && j < right.length) {
        if (left[i] <= right[j]) result.push(left[i++]);
        else result.push(right[j++]);
    }

    return result.concat(left.slice(i)).concat(right.slice(j));
}

// Analysis:
// Divide:   O(1) — just find midpoint
// Conquer:  2T(n/2) — two recursive calls
// Combine:  O(n) — merge two halves
// Recurrence: T(n) = 2T(n/2) + O(n) → O(n log n) by Master Theorem
```

---

#### 4.2 Quick Sort — O(n log n) average, O(n²) worst

```javascript
function quickSort(arr, lo = 0, hi = arr.length - 1) {
    if (lo >= hi) return;

    const pivot = partition(arr, lo, hi);  // divide
    quickSort(arr, lo, pivot - 1);         // conquer left
    quickSort(arr, pivot + 1, hi);         // conquer right
}

function partition(arr, lo, hi) {
    const pivot = arr[hi];
    let i = lo - 1;

    for (let j = lo; j < hi; j++) {
        if (arr[j] <= pivot) {
            i++;
            [arr[i], arr[j]] = [arr[j], arr[i]];
        }
    }

    [arr[i + 1], arr[hi]] = [arr[hi], arr[i + 1]];
    return i + 1;
}

// Analysis:
// Best/Average: T(n) = 2T(n/2) + O(n)  → O(n log n)
// Worst (sorted input): T(n) = T(n-1) + O(n)  → O(n²)
// Space: O(log n) average (call stack)
```

---

#### 4.3 Binary Search — O(log n)

```javascript
function binarySearch(arr, target, lo = 0, hi = arr.length - 1) {
    if (lo > hi) return -1;                 // base case

    const mid = Math.floor((lo + hi) / 2);

    if (arr[mid] === target) return mid;    // found
    if (arr[mid] < target)                  // conquer right
        return binarySearch(arr, target, mid + 1, hi);
    return binarySearch(arr, target, lo, mid - 1); // conquer left
}

// Recurrence: T(n) = T(n/2) + O(1) → O(log n) by Master Theorem Case 2
```

---

#### 4.4 Strassen's Matrix Multiplication — O(n^2.807)

```
Naive matrix multiplication: O(n³)

Strassen's key insight:
  Standard: 8 multiplications + 4 additions per level
  Strassen: 7 multiplications + 18 additions per level

  T(n) = 7T(n/2) + O(n²)
  n^log₂(7) ≈ n^2.807  >  n² = f(n)  → Case 1 of Master Theorem
  → T(n) = O(n^2.807) — faster than O(n³) for large n
```

---

#### 4.5 Count Inversions — O(n log n)

```javascript
// Count pairs (i,j) where i < j but arr[i] > arr[j]
// Modified merge sort — count inversions during merge step

function countInversions(arr) {
    if (arr.length <= 1) return { sorted: arr, count: 0 };

    const mid = Math.floor(arr.length / 2);
    const left  = countInversions(arr.slice(0, mid));
    const right = countInversions(arr.slice(mid));

    let count = left.count + right.count;
    const merged = [];
    let i = 0, j = 0;

    while (i < left.sorted.length && j < right.sorted.length) {
        if (left.sorted[i] <= right.sorted[j]) {
            merged.push(left.sorted[i++]);
        } else {
            // All remaining left elements form inversions with right[j]
            count += left.sorted.length - i;
            merged.push(right.sorted[j++]);
        }
    }

    return {
        sorted: merged.concat(left.sorted.slice(i)).concat(right.sorted.slice(j)),
        count
    };
}
// Time: O(n log n) — same recurrence as Merge Sort
```

### 📚 Key Problems

| # | Problem | Difficulty |
|---|---------|------------|
| [912](https://leetcode.com/problems/sort-an-array/) | Sort an Array (Merge Sort) | 🟡 Medium |
| [315](https://leetcode.com/problems/count-of-smaller-numbers-after-self/) | Count of Smaller Numbers After Self | 🔴 Hard |
| [23](https://leetcode.com/problems/merge-k-sorted-lists/) | Merge K Sorted Lists | 🔴 Hard |
| [4](https://leetcode.com/problems/median-of-two-sorted-arrays/) | Median of Two Sorted Arrays | 🔴 Hard |
| [240](https://leetcode.com/problems/search-a-2d-matrix-ii/) | Search a 2D Matrix II | 🟡 Medium |
| [53](https://leetcode.com/problems/maximum-subarray/) | Maximum Subarray (D&C approach) | 🟡 Medium |

---

## 5. Greedy Method

### 🔑 Concept

Make the **locally optimal choice** at each step. Prove correctness using **exchange arguments** or **greedy stays ahead** proofs.

```
Greedy Algorithm Design Steps:
1. Identify the greedy choice at each step
2. Prove the greedy choice is safe (exchange argument)
3. Prove optimal substructure
4. Implement and analyze
```

### Proof Technique — Exchange Argument

```
Exchange Argument:
  Assume OPT is an optimal solution that differs from GREEDY.
  Show we can modify OPT step-by-step to match GREEDY
  without making it worse.
  → GREEDY solution is at least as good as OPT.
  → GREEDY is optimal.

Example — Activity Selection:
  OPT picks activity A (ends at time 5)
  GREEDY picks activity B (ends at time 3, earlier)

  Exchange: Replace A with B in OPT.
  Does this make OPT worse? NO — B ends earlier, leaving MORE room.
  → GREEDY is at least as good → GREEDY is optimal ✅
```

### 📐 Classic Greedy Algorithms

---

#### 5.1 Activity Selection — O(n log n)

```javascript
function activitySelection(activities) {
    // Sort by finish time — the greedy key
    activities.sort((a, b) => a[1] - b[1]);

    const selected = [activities[0]];
    let lastFinish = activities[0][1];

    for (let i = 1; i < activities.length; i++) {
        if (activities[i][0] >= lastFinish) {    // start after last finish
            selected.push(activities[i]);
            lastFinish = activities[i][1];
        }
    }

    return selected;
}
// Correctness: Proved by exchange argument
// Time: O(n log n) for sorting + O(n) scan = O(n log n)
```

---

#### 5.2 Huffman Encoding — O(n log n)

```
Optimal prefix-free code for data compression.
Greedy: always merge two trees with lowest frequency.

Example:
  chars:    a    b    c    d    e
  freq:     5    9    12   13   16

  Build min-heap: [5,9,12,13,16]
  Merge 5+9=14   → [12,13,14,16]
  Merge 12+13=25 → [14,16,25]
  Merge 14+16=30 → [25,30]
  Merge 25+30=55 → [55]

  Total encoding cost = 55 × ... (optimal!)
  Proof: Greedy merging of smallest frequencies minimizes total weighted depth.
```

---

#### 5.3 Fractional Knapsack — O(n log n)

```javascript
function fractionalKnapsack(items, W) {
    // Sort by value-to-weight ratio — greedy key
    items.sort((a, b) => (b.value / b.weight) - (a.value / a.weight));

    let totalValue = 0;
    let remaining = W;

    for (const item of items) {
        if (remaining <= 0) break;

        if (item.weight <= remaining) {
            totalValue += item.value;         // take whole item
            remaining -= item.weight;
        } else {
            totalValue += item.value * (remaining / item.weight); // take fraction
            remaining = 0;
        }
    }

    return totalValue;
}
// Note: Greedy works for FRACTIONAL knapsack but NOT 0/1 knapsack → use DP
// Time: O(n log n)
// Correctness: Exchange argument on value/weight ratio
```

### 📚 Key Problems

| # | Problem | Difficulty |
|---|---------|------------|
| [435](https://leetcode.com/problems/non-overlapping-intervals/) | Non-overlapping Intervals | 🟡 Medium |
| [452](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/) | Minimum Number of Arrows to Burst Balloons | 🟡 Medium |
| [621](https://leetcode.com/problems/task-scheduler/) | Task Scheduler | 🟡 Medium |
| [135](https://leetcode.com/problems/candy/) | Candy | 🔴 Hard |
| [45](https://leetcode.com/problems/jump-game-ii/) | Jump Game II | 🟡 Medium |
| [763](https://leetcode.com/problems/partition-labels/) | Partition Labels | 🟡 Medium |

---

## 6. Dynamic Programming

### 🔑 Concept

Solve problems by **breaking them into overlapping subproblems**, storing results to avoid recomputation.

```
DP applies when the problem has:
  1. Optimal Substructure  — optimal solution built from optimal subproblems
  2. Overlapping Subproblems — same subproblems solved multiple times

Approaches:
  Top-Down (Memoization) — recursive + cache
  Bottom-Up (Tabulation) — iterative, fill table from base cases up
```

### The 5-Step DP Framework

```
Step 1 — Define the subproblem
  "dp[i] = ___"  (clearly state what it stores)

Step 2 — Identify base cases
  Smallest inputs with known answers

Step 3 — Write the recurrence (transition)
  How does dp[i] relate to dp[i-1], dp[i-2], etc.?

Step 4 — Determine computation order
  Make sure dp[i] is computed after all its dependencies

Step 5 — Extract the answer
  Which dp value (or combination) gives the final answer?
```

### 📐 Classic DP Algorithms

---

#### 6.1 Fibonacci — O(n) time, O(1) space

```javascript
// Naive: O(2ⁿ) — exponential, terrible
// Memo:  O(n) time, O(n) space
// DP:    O(n) time, O(1) space ← optimal

function fibonacci(n) {
    if (n <= 1) return n;
    let prev2 = 0, prev1 = 1;

    for (let i = 2; i <= n; i++) {
        const curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }

    return prev1;
}
```

---

#### 6.2 0/1 Knapsack — O(nW)

```javascript
// dp[i][w] = max value using first i items with capacity w
function knapsack01(weights, values, W) {
    const n = weights.length;
    const dp = Array.from({ length: n + 1 }, () => new Array(W + 1).fill(0));

    for (let i = 1; i <= n; i++) {
        for (let w = 0; w <= W; w++) {
            dp[i][w] = dp[i-1][w];  // don't take item i

            if (weights[i-1] <= w) {
                dp[i][w] = Math.max(dp[i][w],
                    dp[i-1][w - weights[i-1]] + values[i-1]);  // take item i
            }
        }
    }

    return dp[n][W];
}
// Time:  O(nW)  — pseudo-polynomial (depends on W value, not just n)
// Space: O(nW)  → optimizable to O(W) using 1D array
```

---

#### 6.3 Longest Common Subsequence (LCS) — O(mn)

```javascript
// dp[i][j] = LCS length of s1[0..i-1] and s2[0..j-1]
function lcs(s1, s2) {
    const m = s1.length, n = s2.length;
    const dp = Array.from({ length: m + 1 }, () => new Array(n + 1).fill(0));

    for (let i = 1; i <= m; i++) {
        for (let j = 1; j <= n; j++) {
            if (s1[i-1] === s2[j-1]) {
                dp[i][j] = dp[i-1][j-1] + 1;         // characters match
            } else {
                dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]); // skip one
            }
        }
    }

    return dp[m][n];
}
// Time: O(mn), Space: O(mn) → O(min(m,n)) optimizable
```

---

#### 6.4 Matrix Chain Multiplication — O(n³)

```
Problem: Given matrices A₁×A₂×...×Aₙ, find the optimal parenthesization
         that minimizes the number of scalar multiplications.

dp[i][j] = minimum cost to multiply matrices i through j

Recurrence:
  dp[i][j] = min over all k in [i, j-1] of:
              dp[i][k] + dp[k+1][j] + p[i-1] × p[k] × p[j]

  where p[i] = dimensions (matrix i is p[i-1] × p[i])

Time: O(n³), Space: O(n²)
This is the classic "interval DP" pattern.
```

```javascript
function matrixChain(p) {
    const n = p.length - 1;  // number of matrices
    const dp = Array.from({ length: n }, () => new Array(n).fill(0));

    for (let len = 2; len <= n; len++) {         // chain length
        for (let i = 0; i <= n - len; i++) {
            const j = i + len - 1;
            dp[i][j] = Infinity;

            for (let k = i; k < j; k++) {        // split point
                const cost = dp[i][k] + dp[k+1][j] + p[i] * p[k+1] * p[j+1];
                dp[i][j] = Math.min(dp[i][j], cost);
            }
        }
    }

    return dp[0][n-1];
}
```

---

#### 6.5 Bellman-Ford (DP on Graphs) — O(VE)

```javascript
function bellmanFord(n, edges, source) {
    const dist = new Array(n).fill(Infinity);
    dist[source] = 0;

    // Relax all edges V-1 times (DP: dp[v][i] = shortest path using at most i edges)
    for (let i = 0; i < n - 1; i++) {
        for (const [u, v, w] of edges) {
            if (dist[u] !== Infinity && dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
            }
        }
    }

    // Detect negative cycles
    for (const [u, v, w] of edges) {
        if (dist[u] !== Infinity && dist[u] + w < dist[v]) return null;
    }

    return dist;
}
```

### 📚 Key Problems

| # | Problem | Difficulty |
|---|---------|------------|
| [70](https://leetcode.com/problems/climbing-stairs/) | Climbing Stairs | 🟢 Easy |
| [198](https://leetcode.com/problems/house-robber/) | House Robber | 🟡 Medium |
| [300](https://leetcode.com/problems/longest-increasing-subsequence/) | Longest Increasing Subsequence | 🟡 Medium |
| [1143](https://leetcode.com/problems/longest-common-subsequence/) | Longest Common Subsequence | 🟡 Medium |
| [72](https://leetcode.com/problems/edit-distance/) | Edit Distance | 🟡 Medium |
| [312](https://leetcode.com/problems/burst-balloons/) | Burst Balloons | 🔴 Hard |
| [10](https://leetcode.com/problems/regular-expression-matching/) | Regular Expression Matching | 🔴 Hard |

---

## 7. Backtracking

### 🔑 Concept

Systematically explore all possibilities by building solutions **incrementally** and **abandoning** (backtracking) when a partial solution cannot lead to a valid complete solution.

```
Backtracking Template:
  function solve(state):
    if state is a complete solution:
      record/return it
    for each valid next choice:
      make choice
      solve(updated state)   ← recurse
      undo choice            ← backtrack
```

```
Complexity: Usually O(b^d) where b = branching factor, d = depth
Pruning:    Reduce b by rejecting invalid choices early (key optimization)
```

### 📐 Classic Backtracking Problems

---

#### 7.1 N-Queens — O(n!)

```javascript
function solveNQueens(n) {
    const results = [];
    const board = Array(n).fill(null).map(() => Array(n).fill('.'));

    function isValid(row, col) {
        // Check column
        for (let r = 0; r < row; r++)
            if (board[r][col] === 'Q') return false;

        // Check upper-left diagonal
        for (let r = row - 1, c = col - 1; r >= 0 && c >= 0; r--, c--)
            if (board[r][c] === 'Q') return false;

        // Check upper-right diagonal
        for (let r = row - 1, c = col + 1; r >= 0 && c < n; r--, c++)
            if (board[r][c] === 'Q') return false;

        return true;
    }

    function backtrack(row) {
        if (row === n) {
            results.push(board.map(r => r.join('')));
            return;
        }

        for (let col = 0; col < n; col++) {
            if (isValid(row, col)) {
                board[row][col] = 'Q';   // choose
                backtrack(row + 1);       // explore
                board[row][col] = '.';   // unchoose (backtrack)
            }
        }
    }

    backtrack(0);
    return results;
}
// Time: O(n!) worst case, but pruning makes it much faster in practice
```

---

#### 7.2 Subset Sum

```javascript
function subsetSum(nums, target) {
    const results = [];

    function backtrack(start, current, remaining) {
        if (remaining === 0) {
            results.push([...current]);
            return;
        }
        if (remaining < 0) return;   // pruning

        for (let i = start; i < nums.length; i++) {
            current.push(nums[i]);
            backtrack(i + 1, current, remaining - nums[i]);
            current.pop();           // backtrack
        }
    }

    nums.sort((a, b) => a - b);
    backtrack(0, [], target);
    return results;
}
```

### 📚 Key Problems

| # | Problem | Difficulty |
|---|---------|------------|
| [51](https://leetcode.com/problems/n-queens/) | N-Queens | 🔴 Hard |
| [52](https://leetcode.com/problems/n-queens-ii/) | N-Queens II | 🔴 Hard |
| [78](https://leetcode.com/problems/subsets/) | Subsets | 🟡 Medium |
| [46](https://leetcode.com/problems/permutations/) | Permutations | 🟡 Medium |
| [37](https://leetcode.com/problems/sudoku-solver/) | Sudoku Solver | 🔴 Hard |
| [79](https://leetcode.com/problems/word-search/) | Word Search | 🟡 Medium |

---

## 8. Branch and Bound

### 🔑 Concept

An optimization technique for solving NP-Hard problems **exactly** by intelligently pruning the search space. Uses a **bound function** to discard branches that cannot contain a better solution than the current best.

```
Difference from Backtracking:
  Backtracking     → finds all feasible solutions (no bounding)
  Branch & Bound   → finds the optimal solution (uses bound to prune)

Key components:
  Branching:  Divide problem into subproblems (branch)
  Bounding:   Calculate upper/lower bound for each subproblem
  Pruning:    Discard branches where bound ≤ best found so far

Applications: TSP, 0/1 Knapsack (exact), Job Scheduling
```

### 📐 Branch and Bound for 0/1 Knapsack

```
State space tree: each node represents include/exclude decision for item i

Upper bound at each node:
  = value so far + greedy fractional value of remaining items

If upper_bound ≤ best_so_far → prune this branch

Example:
  Items: (w=2,v=40),(w=3.14,v=60),(w=1.98,v=30),(w=5,v=50)  W=10

  Root: bound=110 (greedy fractional), explore...
  Include item 1: value=40, bound=98 > 0 → explore
    Include item 2: value=100, bound=100 > 0 → explore
      Include item 3: value=130, bound=130 → feasible! best=130
      Exclude item 3: bound=105 < 130 → prune
    Exclude item 2: bound=90 < 130 → prune
  Exclude item 1: bound=80 < 130 → prune

  Answer: 130 (optimal!)
```

---

## 9. Graph Algorithms — Design & Analysis

### 9.1 BFS Analysis

```
BFS Correctness Proof (by induction):
  Claim: BFS finds shortest paths (fewest edges) in unweighted graphs.

  Base case: dist[source] = 0 ✅
  Inductive step: If all nodes at distance k are discovered correctly,
    then nodes at distance k+1 are their unvisited neighbors, which
    BFS adds to the queue at the next level. ✅

Time:  O(V + E) — each vertex enqueued once, each edge examined once
Space: O(V) — queue holds at most all vertices
```

### 9.2 Dijkstra's Correctness Proof

```
Invariant: When a node u is popped from the min-heap,
           dist[u] is the true shortest distance.

Proof by contradiction:
  Suppose dist[u] is NOT optimal when popped.
  Then there exists a shorter path u → ... → v → u.
  But dist[v] < dist[u], meaning v was popped BEFORE u.
  When v was processed, dist[u] was updated to dist[v] + w(v,u).
  This contradicts dist[u] being non-optimal when popped. ✅

Why it fails with negative weights:
  A negative edge discovered AFTER popping u could create
  a shorter path, violating the invariant.
  → Use Bellman-Ford for negative weights.
```

### 9.3 Topological Sort Correctness

```
Kahn's Algorithm Invariant:
  A node enters the queue only when all its prerequisites are processed.
  → Processing order respects all dependencies ✅

Cycle Detection:
  If |order| < V after Kahn's → some nodes never reached in-degree 0
  → These nodes form a cycle → no valid topological order exists ✅
```

### 📚 Key Problems

| # | Problem | Difficulty |
|---|---------|------------|
| [207](https://leetcode.com/problems/course-schedule/) | Course Schedule | 🟡 Medium |
| [743](https://leetcode.com/problems/network-delay-time/) | Network Delay Time | 🟡 Medium |
| [1584](https://leetcode.com/problems/min-cost-to-connect-all-points/) | Min Cost to Connect All Points | 🟡 Medium |
| [787](https://leetcode.com/problems/cheapest-flights-within-k-stops/) | Cheapest Flights Within K Stops | 🟡 Medium |

---

## 10. Sorting Algorithms — Deep Dive

### Comparison-Based Sorting Lower Bound Proof

```
Theorem: Any comparison-based sorting algorithm requires Ω(n log n) comparisons.

Proof (Decision Tree):
  Any sort can be modeled as a binary decision tree.
  Each internal node = one comparison (≤ or >).
  Each leaf = one of the n! possible permutations.

  A binary tree with n! leaves has height ≥ log₂(n!)

  By Stirling's approximation:
    log₂(n!) ≈ n log₂ n - n log₂ e ≈ n log₂ n

  → Any comparison sort needs Ω(n log n) comparisons. ✅
  → Merge Sort and Heap Sort are asymptotically OPTIMAL.
```

### Sorting Algorithm Analysis Table

```
Algorithm     Best        Average     Worst       Space   Stable
────────────────────────────────────────────────────────────────
Bubble        O(n)        O(n²)       O(n²)       O(1)    ✅
Selection     O(n²)       O(n²)       O(n²)       O(1)    ❌
Insertion     O(n)        O(n²)       O(n²)       O(1)    ✅
Merge         O(n log n)  O(n log n)  O(n log n)  O(n)    ✅
Quick         O(n log n)  O(n log n)  O(n²)       O(log n)❌
Heap          O(n log n)  O(n log n)  O(n log n)  O(1)    ❌
Counting      O(n+k)      O(n+k)      O(n+k)      O(k)    ✅
Radix         O(nk)       O(nk)       O(nk)       O(n+k)  ✅
Bucket        O(n+k)      O(n+k)      O(n²)       O(n+k)  ✅
Tim Sort      O(n)        O(n log n)  O(n log n)  O(n)    ✅
```

### Linear-Time Sorting (Beating Ω(n log n))

```
Key insight: Non-comparison sorts bypass the Ω(n log n) lower bound
             by using extra information about the data.

Counting Sort:
  Assumption: keys are integers in range [0..k]
  Count occurrences → compute positions → place elements
  Time: O(n + k), Space: O(k)
  Best when k = O(n)

Radix Sort:
  Sort digit by digit (least significant to most significant)
  Use stable sort (Counting Sort) for each digit
  Time: O(nk) where k = number of digits
  Best for integers with bounded digit count

Bucket Sort:
  Distribute n elements into n buckets (assuming uniform distribution)
  Sort each bucket (Insertion Sort)
  Time: O(n) average, O(n²) worst
  Best for uniformly distributed floating-point numbers
```

---

## 11. String Matching Algorithms

### 11.1 Naive String Matching — O(nm)

```javascript
function naiveSearch(text, pattern) {
    const n = text.length, m = pattern.length;
    const matches = [];

    for (let i = 0; i <= n - m; i++) {         // O(n)
        let j = 0;
        while (j < m && text[i + j] === pattern[j]) j++;  // O(m)
        if (j === m) matches.push(i);
    }

    return matches;
}
// Time: O(nm) worst case — e.g., text="aaa...a", pattern="aaa...ab"
```

---

### 11.2 KMP (Knuth-Morris-Pratt) — O(n + m)

```javascript
// Build failure function (prefix function)
function buildKMPTable(pattern) {
    const m = pattern.length;
    const fail = new Array(m).fill(0);
    let j = 0;

    for (let i = 1; i < m; i++) {
        while (j > 0 && pattern[i] !== pattern[j]) j = fail[j - 1];
        if (pattern[i] === pattern[j]) j++;
        fail[i] = j;
    }

    return fail;
}

function kmpSearch(text, pattern) {
    const n = text.length, m = pattern.length;
    const fail = buildKMPTable(pattern);
    const matches = [];
    let j = 0;

    for (let i = 0; i < n; i++) {
        while (j > 0 && text[i] !== pattern[j]) j = fail[j - 1]; // skip using table
        if (text[i] === pattern[j]) j++;
        if (j === m) {
            matches.push(i - m + 1);
            j = fail[j - 1];   // continue searching
        }
    }

    return matches;
}
// Time: O(n + m) — never backtracks in text
// Key idea: Failure function encodes the longest proper prefix that is also a suffix
```

---

### 11.3 Rabin-Karp (Rolling Hash) — O(n + m) average

```javascript
function rabinKarp(text, pattern) {
    const n = text.length, m = pattern.length;
    const BASE = 256, MOD = 1e9 + 7;
    const matches = [];

    let patHash = 0, winHash = 0;
    let h = 1;

    for (let i = 0; i < m - 1; i++) h = (h * BASE) % MOD;

    for (let i = 0; i < m; i++) {
        patHash = (BASE * patHash + pattern.charCodeAt(i)) % MOD;
        winHash = (BASE * winHash + text.charCodeAt(i)) % MOD;
    }

    for (let i = 0; i <= n - m; i++) {
        if (patHash === winHash) {   // hash match — verify character by character
            if (text.slice(i, i + m) === pattern) matches.push(i);
        }

        if (i < n - m) {
            winHash = (BASE * (winHash - text.charCodeAt(i) * h) + text.charCodeAt(i + m)) % MOD;
            if (winHash < 0) winHash += MOD;
        }
    }

    return matches;
}
// Average: O(n + m), Worst: O(nm) due to hash collisions
// Key idea: Rolling hash — remove leftmost char, add rightmost in O(1)
```

### 📚 Key Problems

| # | Problem | Difficulty |
|---|---------|------------|
| [28](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/) | Find the Index of the First Occurrence in a String | 🟢 Easy |
| [459](https://leetcode.com/problems/repeated-substring-pattern/) | Repeated Substring Pattern | 🟢 Easy |
| [686](https://leetcode.com/problems/repeated-string-match/) | Repeated String Match | 🟡 Medium |
| [1392](https://leetcode.com/problems/longest-happy-prefix/) | Longest Happy Prefix (KMP) | 🔴 Hard |
| [214](https://leetcode.com/problems/shortest-palindrome/) | Shortest Palindrome (KMP) | 🔴 Hard |

---

## 12. Complexity Theory — P, NP, NP-Hard

### 🔑 The Big Picture

```
P        = Problems solvable in polynomial time O(nᵏ)
           Examples: Sorting, BFS, Dijkstra, Binary Search

NP       = Problems whose solutions can be VERIFIED in polynomial time
           Examples: 3-SAT, Subset Sum, Traveling Salesman (decision)

NP-Hard  = At least as hard as any NP problem (may not be in NP)
           Examples: TSP (optimization), Halting Problem

NP-Complete = Both NP and NP-Hard
           Examples: 3-SAT, Knapsack, Graph Coloring, Vertex Cover

The big question: P = NP?
  If YES → every problem with verifiable solutions can be solved efficiently
  If NO  → there exist problems in NP that cannot be solved in polynomial time
  Status: UNSOLVED — the most famous open problem in computer science
```

### Complexity Class Diagram

```
                    ┌─────────────────────────┐
                    │         NP-Hard         │
                    │   ┌─────────────────┐   │
                    │   │   NP-Complete   │   │
                    │   │  ┌──────────┐  │   │
                    │   │  │    NP    │  │   │
                    │   │  │ ┌──────┐ │  │   │
                    │   │  │ │  P   │ │  │   │
                    │   │  │ └──────┘ │  │   │
                    │   │  └──────────┘  │   │
                    │   └─────────────────┘   │
                    └─────────────────────────┘
                    (assuming P ≠ NP)
```

### Reductions

```
Reduction: Transform problem A into problem B in polynomial time.
           If B is easy to solve, so is A.
           Notation: A ≤ₚ B (A reduces to B)

Why it matters:
  To prove X is NP-Complete:
  1. Show X is in NP (solution verifiable in polynomial time)
  2. Show a known NP-Complete problem reduces to X

First NP-Complete problem: 3-SAT (Cook-Levin Theorem, 1971)
From 3-SAT, many others were proved NP-Complete:
  3-SAT → Clique → Vertex Cover → Subset Sum → Knapsack → ...
```

### NP-Complete vs Polynomial Special Cases

```
Problem             General Case    Special Case (Polynomial)
──────────────────────────────────────────────────────────────
Knapsack            NP-Complete     Fractional Knapsack O(n log n)
Graph Coloring      NP-Complete     2-Coloring (Bipartite) O(V+E)
Shortest Path       P (Dijkstra)    With negative cycles NP-Hard
Traveling Salesman  NP-Hard         On trees O(n)
Vertex Cover        NP-Complete     On trees O(n) via DP
Satisfiability      NP-Complete     2-SAT O(V+E)
```

---

## 13. Approximation Algorithms

### 🔑 Concept

When a problem is NP-Hard, we can't find the optimal solution in polynomial time (unless P=NP). Instead, we find a solution **guaranteed to be within a factor** of the optimal.

```
ρ-approximation algorithm:
  Produces solution with cost ≤ ρ × OPT (for minimization)
  or solution with value ≥ (1/ρ) × OPT (for maximization)

  ρ = approximation ratio (closer to 1 = better)
```

### 13.1 Vertex Cover — 2-Approximation

```javascript
// 2-approximation: every edge must be covered by at least one endpoint
function vertexCover2Approx(edges) {
    const cover = new Set();
    const visited = new Set();

    for (const [u, v] of edges) {
        if (!visited.has(u) && !visited.has(v)) {
            cover.add(u);
            cover.add(v);
            visited.add(u);
            visited.add(v);
        }
    }

    return cover;
}
// Proof: Each selected edge (u,v) contributes 2 nodes to cover.
// OPT must include at least 1 of {u,v} per selected edge.
// → |our cover| ≤ 2 × OPT → 2-approximation ✅
```

### 13.2 TSP — 1.5-Approximation (Christofides)

```
For metric TSP (triangle inequality holds):
  Step 1: Find MST M                      O(E log V)
  Step 2: Find vertices with odd degree in M
  Step 3: Find minimum weight perfect matching on odd-degree vertices
  Step 4: Combine MST + matching = Eulerian multigraph
  Step 5: Find Euler tour, shortcut repeated vertices
  Result: ≤ 1.5 × OPT

Proof:
  MST cost ≤ OPT (removing any edge from optimal tour gives spanning tree)
  Matching cost ≤ OPT/2 (two perfect matchings partition the optimal tour)
  → Total ≤ OPT + OPT/2 = 1.5 × OPT ✅
```

### 13.3 Set Cover — O(log n) Approximation

```
Greedy: At each step, choose the set covering the most uncovered elements.

Approximation ratio: H(n) ≈ ln(n) + 1   (harmonic number)

Proof: After k steps, at most n × (1 - 1/k)ⁿ elements remain uncovered.
       After OPT × ln(n) steps → all covered.
       → Greedy uses at most OPT × ln(n) sets.
```

---

## 14. Randomized Algorithms

### 🔑 Concept

Use **randomness** to simplify algorithm design or improve expected performance.

```
Las Vegas:   Always correct, random in RUNNING TIME
             Example: Randomized QuickSort
             "It will finish, but we don't know exactly when"

Monte Carlo: Always fast, random in CORRECTNESS (with small error probability)
             Example: Miller-Rabin Primality Test, Karger's Min-Cut
             "It might be wrong, but probability of error is tiny"
```

### 14.1 Randomized QuickSort — O(n log n) Expected

```javascript
function randomizedQuickSort(arr, lo = 0, hi = arr.length - 1) {
    if (lo >= hi) return;

    // Random pivot — prevents O(n²) worst case
    const randIdx = lo + Math.floor(Math.random() * (hi - lo + 1));
    [arr[randIdx], arr[hi]] = [arr[hi], arr[randIdx]];

    const pivot = partition(arr, lo, hi);
    randomizedQuickSort(arr, lo, pivot - 1);
    randomizedQuickSort(arr, pivot + 1, hi);
}

// Expected Analysis:
// E[comparisons] = Σᵢ Σⱼ>ᵢ P(i compared with j) = Σᵢ Σⱼ>ᵢ 2/(j-i+1)
// = O(n log n) expected
// Key: Random pivot → each element equally likely to be chosen first
```

### 14.2 Karger's Min-Cut — O(n² log n) with repetition

```
Randomized contraction algorithm:
  While |V| > 2:
    Pick a random edge (u,v)
    Contract: merge u and v into one supernode
    Remove self-loops
  Return the remaining two sets as the cut

Single run probability of finding min-cut ≥ 2/n²
Repeat O(n² log n) times → probability of failure < 1/n

This gives a randomized O(n² log n) algorithm for min-cut.
```

### 14.3 Reservoir Sampling — O(n)

```javascript
// Sample k items from stream of unknown length n — each equally likely
function reservoirSample(stream, k) {
    const reservoir = stream.slice(0, k);

    for (let i = k; i < stream.length; i++) {
        const j = Math.floor(Math.random() * (i + 1));
        if (j < k) reservoir[j] = stream[i];
    }

    return reservoir;
}
// Proof: P(stream[i] in final reservoir) = k/n for all i ✅
```

---

## 15. Amortized Analysis

### 🔑 Concept

Amortized analysis finds the **average cost per operation** over a sequence of operations, even when some individual operations are expensive.

```
Three methods:
1. Aggregate  — total cost / number of operations
2. Accounting — assign "credits" to cheap ops to pay for expensive ones
3. Potential  — define a potential function Φ; amortized cost = actual + ΔΦ
```

### 15.1 Dynamic Array (ArrayList) — Amortized O(1) Push

```
Operations: n push() calls, some trigger O(n) resize

Aggregate Analysis:
  Total resizes at sizes: 1, 2, 4, 8, ..., n/2, n
  Total copy work = 1 + 2 + 4 + ... + n/2 + n = 2n - 1 = O(n)
  n operations total
  Amortized cost per push = O(n) / n = O(1) ✅

Accounting Method:
  Charge each push $3:
    $1 for the push itself
    $1 saved for future copy of this element
    $1 to copy another old element when resize happens
  → Each resize is fully paid for → amortized O(1) ✅
```

### 15.2 Union-Find with Path Compression — O(α(n))

```
Inverse Ackermann function α(n) ≈ 4 for all practical n
This means Union-Find is essentially O(1) amortized per operation.

Without optimizations:   O(n) per operation
With union by rank:      O(log n) per operation
With path compression:   O(log n) amortized
With BOTH optimizations: O(α(n)) amortized ≈ O(1)

Proof (Tarjan, 1975): A sequence of m operations takes O(m × α(n)) total.
This is the best possible for Union-Find structures.
```

### 15.3 Splay Tree — O(log n) Amortized

```
Splay trees: self-adjusting BST, recently accessed nodes moved to root.

Potential function: Φ = Σ rank(v) for all nodes v
  where rank(v) = log(size of subtree rooted at v)

Amortized cost of any operation ≤ 3(rank(root) - rank(v)) + 1 = O(log n)

Practical advantage:
  Accessed nodes stay near root → temporal locality → fast in practice
  Cache-friendly for real workloads
```

---

## 🗺️ Algorithm Design Paradigm Comparison

```
Paradigm        When to Use                           Key Insight
──────────────────────────────────────────────────────────────────────────
Divide & Conquer  Problem splits into independent parts  Recurrence + combine
Greedy            Local optimal = global optimal         Exchange argument proof
Dynamic Programming Overlapping subproblems               Memoize to avoid repeat
Backtracking      Enumerate all possibilities             Prune invalid branches
Branch & Bound    Optimal among NP-Hard solutions        Bound + prune
Approximation     NP-Hard, need near-optimal fast        Guaranteed ratio
Randomized        Simplify or improve expected case       Randomize to avoid worst case
```

---

## ⚡ Master Reference Table

```
Algorithm               Time            Space       Paradigm
─────────────────────────────────────────────────────────────────
Binary Search           O(log n)        O(1)        D&C
Merge Sort              O(n log n)      O(n)        D&C
Quick Sort (avg)        O(n log n)      O(log n)    D&C
Heap Sort               O(n log n)      O(1)        D&C
BFS / DFS               O(V + E)        O(V)        Graph
Dijkstra                O(E log V)      O(V)        Greedy
Prim / Kruskal (MST)    O(E log V)      O(V)        Greedy
Activity Selection      O(n log n)      O(1)        Greedy
0/1 Knapsack (DP)       O(nW)           O(nW)       DP
LCS                     O(mn)           O(mn)       DP
Bellman-Ford            O(VE)           O(V)        DP / Graph
Floyd-Warshall          O(V³)           O(V²)       DP / Graph
KMP String Match        O(n + m)        O(m)        String
Rabin-Karp              O(n + m) avg    O(1)        Hashing
Strassen Matrix Mult    O(n^2.807)      O(n²)       D&C
N-Queens                O(n!)           O(n)        Backtracking
Vertex Cover Approx     O(E)            O(V)        Approximation
Randomized QuickSort    O(n log n) exp  O(log n)    Randomized
Union-Find (both opt)   O(α(n))         O(n)        Amortized
```

---

## 📚 Study Resources

### Textbooks

```
"Introduction to Algorithms" (CLRS)    — The Bible of DAA. Rigorous proofs.
"Algorithm Design" — Kleinberg & Tardos — Excellent proofs, intuition-first.
"The Algorithm Design Manual" — Skiena  — Practical focus, real-world problems.
"Algorithms" — Sedgewick & Wayne        — Java-based, visual, beginner-friendly.
"Algorithms" — Dasgupta, Papadimitriou  — Free PDF, concise proofs.
```

### Online Courses

```
MIT 6.006 (Introduction to Algorithms) — Free on MIT OpenCourseWare
MIT 6.046 (Design and Analysis of Algorithms) — Advanced, free MIT OCW
Stanford Algorithms (Coursera) — Tim Roughgarden — Excellent explanations
Princeton Algorithms (Coursera) — Sedgewick — Java-based, visuals
```

---

## 🔗 This DSA + DAA Series

| Repo | Topic | Status |
|------|-------|--------|
| 📖 [DSA Fundamentals](https://github.com/lokeshcs25/Data-structures-and-Algorithms---decision-playbook) | Why DSA, Big O, How to Start | ✅ Done |
| 📐 **DAA — Design & Analysis** | Paradigms, Proofs, Complexity Theory | ← **You are here** |
| [Sliding Window](https://github.com/lokeshcs25/Sliding-Window-Patterns-From-One-to-N) | Fixed, Variable, Deque | ✅ Done |
|  [Two Pointers](https://github.com/lokeshcs25/Two-Pointer-Patterns-From-Zero-to-N) | Opposite, Same Direction, Linked List | ✅ Done |
|  [Binary Search](https://github.com/lokeshcs25/Binary-Search-Patterns-From-One-to-N) | Classic, On Answer, 2D Matrix | ✅ Done |
|  [Bit Manipulation](https://github.com/lokeshcs25/Bit-Manipulation-Patterns-From-One-to-N) | XOR, Bitmask, DP | ✅ Done |
|  [Greedy Algorithms](https://github.com/lokeshcs25/Greedy-Patterns-From-One-to-N) | Intervals, Jump Game, Heap | ✅ Done |
|  [Graph Algorithms](https://github.com/lokeshcs25/Graph-Patterns-From-One-to-N) | BFS, DFS, Dijkstra, MST | ✅ Done |
| 🌳 Tree Patterns | BFS, DFS, LCA, Segment Tree | 🔜 Soon |
| 📊 Dynamic Programming | 1D, 2D, Knapsack, LCS | 🔜 Soon |

---

## 🤝 Contributing

Contributions are welcome!
- Found a proof error? Please open an issue with a correction.
- Want to add a new algorithm with analysis? Open a PR.
- Spot a missing classic problem? Suggest it via issue.

---

## ⭐ Star this repo if it helped you!

> The theoretical backbone of the complete DSA patterns series.
> Understanding the WHY behind algorithms makes you unstoppable. 🚀
