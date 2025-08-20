# 🐸 Frog  – Minimum Jump Cost (DP)

This repository solves the classic **Frog** problem using **Dynamic Programming** from ATCODERS, where a frog must jump across stones with minimum cost.
> If you're new to DP, this problem is a perfect place to start. It’s short, clean, and teaches the basics of state transitions! ✅
---

## 📘 Problem Statement
 
There are `N` stones, each with a given **height**. A frog starts at stone `1`, and wants to reach stone `N`.

From any stone `i`, the frog can:
- Jump to stone `i + 1`
- Or jump to stone `i + 2`

### 💸 Cost of a Jump:
The cost is the **absolute difference** in heights:
```plaintext
cost = |height[i] - height[j]|
```
### 🧠 Dynamic Programming Approach
```
We define a dp[i] array:
      dp[i] represents the minimum cost to reach stone i'th stone
```
## Base Case:
- dp[0] = 0 (starting point)          //as frong already present at 1'st stone so the cost is 0
- dp[1] = |h[1] - h[0]|   (first possible jump)     //cost to reach the stone 2 is the diff in stone 1 and 2 height

## Recurrence Relation:
From stone 3,
The cost to reach the stone 3 is in two ways and need to tak ethe min of them:
- we can go to stone 3 from stone 2, cost to reach stone 3 is cost at stone 2 + cost taken to reach the stone 3 from stone 2 (i.e|stone 3 - stone 2|)
- we can go to stone 3 from stone 1, cost to reach stone 3 is cost at stone 1 + cost taken to reach the stone 3 from stone 1 (i.e|stone 3 - stone 1|)

```
dp[i] = min(
    dp[i-1] + abs(height[i] - height[i-1]),
    dp[i-2] + abs(height[i] - height[i-2])
)
```
## 🧑‍💻 Full C++ Code
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    vector<int> ar(n);
    for (int &i : ar) cin >> i;

    vector<int> dp(n, 0);

    // Base case: first jump
    dp[1] = abs(ar[1] - ar[0]);

    for (int i = 2; i < n; i++) {
    //We can jump to current stone from previous 2 stone only
        dp[i] = min(
            abs(ar[i] - ar[i - 1]) + dp[i - 1],
            abs(ar[i] - ar[i - 2]) + dp[i - 2]
        );
    }

    cout << dp[n - 1] << endl;
    return 0;
}
```


