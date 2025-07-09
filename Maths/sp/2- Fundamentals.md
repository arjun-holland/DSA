# 📘 Combinatorics in DSA, OA & Competitive Programming

This document provides essential **combinatorial formulas and insights** commonly used in algorithm problems, online assessments, and coding contests. Concepts include **nCr, permutations, stars and bars**, and **sequence arrangements**.

---

## 🔢 1. Combinations – nCr

### ✅ Formula :  nCr = n! / (r! * (n - r)!)

### 📌 Meaning:
- **Select `r` items from `n` distinct items** without caring about the **internal order**.
- Example: Select 3 fruits from 5 types — order doesn't matter => 5C3 = 5!/((5!-3!)*3!) => 10 ways

---

## 🔁 2. Permutations from Combinations

> If **internal ordering matters**, multiply by `r!`:
### ✅ Formula :  nPr = [n! / (r! * (n - r)!)]*r!

### 📌 Example:
- Choosing and arranging 3 books from a shelf of 5: 5C3 * 3! = number of permutations


---

## 📈 3. Strictly Increasing Arrays

**Problem**:  
Find the number of strictly increasing arrays of size `N`, where each number is in range `1` to `M`.

### ✅ Insight:
To form a strictly increasing array:
- You must choose `N` unique numbers from `1` to `M`.
- Since order is increasing, no permutations allowed.
- mCn

### ✅ Solution:

> This also answers: *"How many ways to select `N` numbers from `1...M` such that they are in strictly increasing order?"*

---

## 🎯 4. Stars and Bars (Balls & Boxes)


![image](https://github.com/user-attachments/assets/0fbb17bc-9070-416b-af87-2f4de113eb04)

### Problem:
Distribute `n` **identical balls** into `k` **distinct boxes**, allowing zero balls in a box.

### ✅ Formula:
(n + k - 1) C (k - 1)

### Example:
Put 5 balls in 2 boxes:
- (5,0), (4,1), (3,2), (2,3), (1,4), (0,5)
- Total ways: `6`

(5 + 2 - 1) C (2 - 1) = 6C1 = 6

### Interpretation:
Solving for:
x1 + x2 = 5, where x1, x2 ≥ 0

General form:
x1 + x2 + x3 + ... + xk = n
=> (n + k - 1) C (k - 1)

![image](https://github.com/user-attachments/assets/5d50698e-4777-44e8-8711-6314e4b168a0)


---

## 🔗 5. Merge Sequences (Order-Preserving)

**Problem**:  
Given two sequences of sizes `N` and `M`, how many ways can you interleave them **without changing the order** within each?

### ✅ Formula:
(N + M) C M

### Example:
Sequences: `[1, 2]` and `[3, 4]`

Possible interleavings (6 total):
- [1,2,3,4]
- [1,3,2,4]
- [1,3,4,2]
- [3,1,2,4]
- [3,1,4,2]
- [3,4,1,2]

> Useful in **DP problems**, **interleaving strings**, **sequence alignment**, etc.

---

## ⚙️ 6. Efficient nCr % MOD (Big Prime)

In coding assessments, you often need to compute:
nCr % MOD

Where:
- `n, r ≤ 100000`
- `MOD = 10^9 + 7` (a large prime)

### ✅ Precomputation Template (C++-like Logic)

```cpp
const int MOD = 1e9 + 7;
const int MAX = 1e5 + 5;

long long fact[MAX], invFact[MAX];

// Fast power for modular inverse
long long modPow(long long a, long long b) {
    long long res = 1;
    while (b) {
        if (b & 1) res = res * a % MOD;
        a = a * a % MOD;
        b >>= 1;  // >>	Right shift operator b >>= 1	Shift b one bit to the right like d =  d/2
    }
    return res;
}

// Precompute factorials and inverse factorials
void precompute() {
    fact[0] = invFact[0] = 1;
    for (int i = 1; i < MAX; i++) {
        fact[i] = fact[i - 1] * i % MOD;
        invFact[i] = modPow(fact[i], MOD - 2);
    }
}

long long nCr(int n, int r) {
    if (r > n) return 0;
    return fact[n] * invFact[r] % MOD * invFact[n - r] % MOD;
}
```
⚡ Precomputing factorials avoids TLE during test cases!

# Techniques
| Concept             | Formula                        | Description                                  |
| ------------------- | ------------------------------ | -------------------------------------------- |
| Combinations (nCr)  | `n! / (r! * (n - r)!)`         | Ways to choose r items from n, order ignored |
| Permutations (nPr)  | `nCr * r!`                     | Ways to choose and arrange r items           |
| Strictly Increasing | `M C N`                        | Select N increasing numbers from 1 to M      |
| Stars and Bars      | `(n + k - 1) C (k - 1)`        | Distribute n identical balls into k boxes    |
| Merge Sequences     | `(N + M) C M`                  | Interleave sequences while preserving order  |
| Efficient nCr % MOD | Precompute factorials + modInv | For large n and r with MOD (big prime)       |

