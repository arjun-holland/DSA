# 🚀 Max Sum of Non-Adjacent Elements – Dynamic Programming Explained!

> Understanding this problem builds a rock-solid foundation for mastering **Dynamic Programming (DP)**!  
> (Trust me, it *clicked* for me with this exact one 😊)
 
---

## 🧠 Problem Statement

You're given an array of integers (which can include both **positive** and **negative** numbers).

Your task is to choose a **subset** of elements such that:
1. The **sum** of the selected elements is **maximum**.
2. **No two selected elements are adjacent** in the original array.

---

## 🔍 Example

```plaintext
Input:  [2, 4, 6, 7, 8]
Output: 16

Explanation:
Choose elements 2, 6, and 8.
(2 + 6 + 8 = 16)
```
---
## 🛠️ Core DP Insight
We use a dp array where:
    dp[i] represents the maximum sum we can get considering elements from index 0 to i.

---
## 🧩 Step-by-Step Breakdown
Let’s walk through how dp[i] builds up:
For the array [2, 4, 6, 7, 8]:
| Index | Element | Maximum Sum (dp\[i]) | Subset Chosen |
| ----- | ------- | -------------------- | ------------- |
| 0     | 2       | 2                    | \[2]          |
| 1     | 4       | 4                    | \[4]          |
| 2     | 6       | 8                    | \[2, 6]       |
| 3     | 7       | 11                   | \[4, 7]       |
| 4     | 8       | 16                   | \[2, 6, 8]    |


## 💡 For each i, we have two choices:
```
Include arr[i]
→ Can't include arr[i-1] due to adjacency rule
→ So: dp[i] = arr[i] + dp[i-2]

Exclude arr[i]
→ Use previous result is greater then as-is
→ So: dp[i] = dp[i-1]
```

## 🧾 Final DP Formula:
 `dp[i] = max(dp[i-1], arr[i] + dp[i-2])` 
 take max of previous dp value or add the current value to previous of previous dp value.

## ✅ C++ Implementation
```
#include <bits/stdc++.h>
using namespace std;

int maxSumNonAdjacent(vector<int>& arr) {
    int n = arr.size();
    if (n == 0) return 0;
    if (n == 1) return arr[0];

    vector<int> dp(n);
    dp[0] = arr[0];
    dp[1] = max(arr[0], arr[1]);

    for (int i = 2; i < n; ++i) {
        dp[i] = max(arr[i] + dp[i - 2], dp[i - 1]);
    }

    return dp[n - 1];
}

int main() {
    int n;
    cin >> n;
    vector<int> arr(n);
    for (int& x : arr) cin >> x;

    cout << "Max sum with no adjacent elements: " << maxSumNonAdjacent(arr) << endl;
    return 0;
}
```

