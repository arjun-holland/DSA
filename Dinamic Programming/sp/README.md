# 🔁 Dynamic Programming (DP)

---

## 📖 Definition

**Dynamic Programming** is an optimization technique used to solve problems by breaking them down into overlapping subproblems and storing the results of these subproblems to avoid redundant computation.

> “DP is not just about solving problems—it's about solving them *efficiently*.”

---

## 🧩 Types of Dynamic Programming

Dynamic Programming problems generally fall into two categories:

1. **Top-Down (Memoization)**
   - Uses recursion + caching results.
   - Starts from the main problem and breaks it down recursively.
   - Stores solutions to subproblems in a table (usually a hashmap or array).

2. **Bottom-Up (Tabulation)**
   - Uses iteration.
   - Builds solutions starting from the smallest subproblems up to the main problem.
   - Usually more space/time efficient than top-down.

---

## 📌 When to Use Dynamic Programming

Use DP when:
- The problem can be broken into **subproblems**.
- Subproblems **overlap** (i.e., you solve the same problem multiple times).
- There’s **optimal substructure**: Optimal solution to the main problem depends on optimal solutions to subproblems.

**Clues:**
- "Find the number of ways..."
- "Find the minimum/maximum..."
- "Make a choice at each step..."
- Recursive brute-force gives TLE (Time Limit Exceeded)

---

## 🛠️ How to Use Each Type

### 🔹 Top-Down (Memoization)

**Steps:**
1. Write a recursive solution.
2. Identify repeated subproblems.
3. Store intermediate results in a memo table (usually an array or map).

```cpp
int fib(int n, vector<int>& memo) {
    if (n <= 1) return n;
    if (memo[n] != -1) return memo[n];
    return memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
}
```
### 🔸 Bottom-Up (Tabulation)

**Steps:**
1. Identify the order of computation.
2. Create a DP table.
3. Fill the table iteratively.
```
int fib(int n) {
    vector<int> dp(n + 1, 0);
    dp[0] = 0;
    dp[1] = 1;
    for (int i = 2; i <= n; i++)
        dp[i] = dp[i - 1] + dp[i - 2];
    return dp[n];
}
```
---

## 🧠 How to Identify DP Problems
✅ Patterns to Look For:
| Clue                             | Meaning                             |
| -------------------------------- | ----------------------------------- |
| Problem asks for min/max/count   | Likely needs optimization           |
| Choices at each step             | Use recursion with memoization      |
| Repeating subproblems            | Store and reuse solutions           |
| Grid, sequence, subsets involved | Often DP (like paths, LCS, subsets) |

