# 🔧 Bottom-Up Dynamic Programming (Tabulation)

Welcome to the **Bottom-Up DP** section! This is where we build our understanding of dynamic programming from the ground up—literally.

---

## 🪜 Steps to Follow for Bottom-Up DP

1. **Initialize the DP array** of size `n` (or as needed).
2. **Define the meaning of `dp of first element`**  
   → `dp[i]` typically means the best answer to the problem **up to index `i`**.
3. **Break the main problem into subproblems** like `dp[1]`, `dp[2]`, ..., `dp[n]`.
4. **Find a Base Case** we get answers for dp[0], dp[1] by observing and analysing the question
5. **Find a relation (recurrence)** that solves `dp[i]` using smaller subproblems.
6. **Compute the final answer as `dp[n]`** (or whatever index the problem asks for).

---

## 💡 Problem 1: Prefix Sum Queries

**Problem Statement:**  
Given an array of integers `a[n]`, answer multiple queries of the form:  
`(1, i)` → Output the sum of all elements from index 1 to `i` (inclusive).

**Naive Approach:**  
Use a loop for each query → Time: **O(N * Q)**  
Not efficient when both N and Q are large.

---

### ✅ Optimized DP Solution (Prefix Sum)

We can precompute the prefix sum using a **bottom-up DP** array.

**Define:**  
- `dp[i] = sum of a[1] to a[i]`  
(Assuming 1-based indexing)

Let us create a dp-array of size ‘n’.
-->dp[1]=sum of all numbers from (1,1)
-->dp[2]=sum of all numbers from (1,2)…

---

### 🧮 Example:

Let:  
```cpp
a[5] = {4, 5, 3, 2, 1}

Then:
dp[1] = 4 {if we have only 1 ele in arry then that is our answer}
dp[2] = dp[1] + a[2] = 4 + 5 = 9 {if we have 2 elements then we need to add the previous sum to tha curr ele}
dp[3] = dp[2] + a[3] = 9 + 3 = 12
and so on...

Recurrence Relation:
        dp[i] = a[i] + dp[i - 1]
```
### code
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n = 5; // size of the array
    int a[5] = {6, 7, 3, 2, 2}; 

    int dp[n + 1] = {0}; // dp array to store prefix sums

    dp[0] = a[0];

    // Step 1: Precompute prefix sums
    for (int i = 1; i < n; ++i) {
        dp[i] = a[i] + dp[i - 1];
    }

    // Step 2: Answer queries in O(1)
    int q = 4; 
    int queries[4] = {0, 3, 4, 2};

    for (int i = 0; i < q; ++i) {
        int idx = queries[i];
        // 'idx' is 0-based; idx + 1 is shown for clarity (1-based display)
        cout << "Sum from index 1 to " << idx + 1 << " = " << dp[idx] << endl;
    }
    return 0;
}

```

### 🧠 Key Takeaways
- We precomputed prefix sums in O(N) time.
- Each query was answered in O(1).
- Total time: O(N + Q) — efficient and fast!


