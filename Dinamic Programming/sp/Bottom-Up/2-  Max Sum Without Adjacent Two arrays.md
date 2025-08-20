# 🔥 Max Sum from Two Arrays Without Adjacent Elements

> A powerful Dynamic Programming (DP) problem that builds deep intuition for handling constraints across **multiple arrays**.   
> (This one *clicked* for me, and it’ll help you too! 😊)

---

## 📌 Problem Statement

Given **two arrays** of size `n`, select a subset of elements such that:

1. The **sum is maximized**.
2. **No two selected elements are adjacent**, meaning:
   - You **cannot** pick elements from the **same or opposite array at adjacent indices**.
   - For example, if you pick `a1[3]`, you can't pick:
     - `a1[2]`, `a1[4]`
     - `a2[2]`, `a2[3]`, or `a2[4]`

---

## 🧠 Example

```plaintext
Array 1:  [1, 5, 3, 21234]
Array 2:  [-4509, 200, 3, 40]

Pick 200 from ar2[1] and 21234 from ar1[3].

Result: 200 + 21234 = 21434 ✅
```
## 💡 DP Strategy
We define a DP array where:
 `dp[i] = max sum we can get considering index 0 to i` (from either array)
 
---
# How it works
```
For any index i, we have 2 choices:
Include max of a1[i] or a2[i] + previous  of previous dp value
→ But skip i-1, so:
dp[i] = max(ar1[i], ar2[i]) + dp[i-2]
Exclude index i when the previous dp valus is greater 
→ Just carry forward:
dp[i] = dp[i-1]
```
## 🧾 Final Recurrence Relation
` dp[i] = max(dp[i - 1], max(ar1[i], ar2[i]) + dp[i - 2]) `

## Code in CPP
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n; // Read size of the arrays

    vector<int> ar1(n); // First array
    for (int &i : ar1) cin >> i; // Input elements for ar1

    vector<int> ar2(n); // Second array
    for (int &i : ar2) cin >> i; // Input elements for ar2

    vector<int> dp(n); // dp[i] stores the max sum till index i

    // Base case: Only one element to choose from (index 0)
    dp[0] = max(ar1[0], ar2[0]);

    // Base case: Choose max of either first or second elements
    if (n > 1) {
        dp[1] = max(dp[0], max(ar1[1], ar2[1]));
    }

    // Fill dp array from index 2 to n-1
    for (int i = 2; i < n; i++) {
        // Two choices:
        // 1. Take the max of ar1[i] or ar2[i], then add dp[i - 2]
        // 2. Skip current index and take dp[i - 1]

        dp[i] = max(dp[i - 1], max(ar1[i], ar2[i]) + dp[i - 2]);
    }

    // Final answer is max sum without adjacent elements
    cout << "Max sum in subarray without adjacent: " << dp[n - 1] << endl;

    return 0;
}

```
# Tip
- If we solve this using simple recursion, the time complexity is O(2^n)
- Because for each index, we have two choices (pick or skip) → exponential growth
- But with Dynamic Programming (DP), we reduce it to O(n)
- by storing previous results and avoiding repeated work
