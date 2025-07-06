# 🐸 Frog 2 – Minimum Jump Cost (DP)

This repository solves the classic **Frog 2** problem using **Dynamic Programming** from **AtCoder**, where a frog must jump across stones with **minimum cost** using **variable jump distance `K`**.
> If you're new to DP, this problem is a perfect next step after Frog 1. It builds on the same ideas but adds flexibility. Great for learning state transitions with variable ranges! ✅

---

## 📘 Problem Statement

There are `N` stones, each with a given **height**. A frog starts at **stone 1**, and wants to reach **stone N**.

From any stone `i`, the frog can:
- Jump to any stone from `i + 1` to `i + K`

### 💸 Cost of a Jump:
The cost is the **absolute difference** in heights:
```plaintext
        cost = |height[i] - height[j]|
Where i is the current stone and j is the destination stone (i+1 to i+K).
```
## 🧠 Dynamic Programming Approach
```
We define a dp[i] array where:
      dp[i] = minimum cost to reach the i-th stone
```

## 🟢 Base Case:
dp[1] = 0
→ The frog starts at stone 1, so the cost is 0.

dp[2] = |h[2] - h[1]|
→ First actual jump to stone 2, cost is just the difference in heights.

## 🔁 Recurrence Relation:
From any stone i, the frog may have arrived from up to K stones behind.

We try all possible previous stones j = i-1, i-2, ..., i-K, and take the minimum total cost:

```
    dp[i] = min(
        dp[i-j] + abs(height[i] - height[i-j]) for all j = 1 to K
    )
This captures all the ways to reach stone i from any of the K previous steps.
```

## 🧑‍💻 Full C++ Code
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, k;
    cin >> n >> k;  // Number of stones and max jump distance

    vector<int> height(n + 1); // 1-based index: height[1] to height[n]
    for (int i = 1; i <= n; i++) {
        cin >> height[i];
    }

    vector<int> dp(n + 1, 0); // 1-based index: dp[1] to dp[n]

    dp[1] = 0; // Cost to reach first stone is 0

    if (n >= 2) {
        dp[2] = abs(height[2] - height[1]);
    }

    for (int i = 3; i <= n; i++) {    //current stone
        int minCost = INT_MAX;

        // Try all jumps from i-1, i-2, ..., i-k
        for (int j = 1; j <= k; j++) {   
            if (i - j >= 1) {   // the stones from where we can jump to current stone has to be upto k stones, Example: To reach stone 3, valid previous stones are 2 and 1, not beyond that stone
                int cost = dp[i - j] + abs(height[i] - height[i - j]);
                minCost = min(minCost, cost);
            }
        }

        dp[i] = minCost;
    }

    cout << dp[n] << endl; // Minimum total cost to reach last stone
    return 0;
}
```

## 🧠 Dry Run — Step-by-Step DP Table
| Stone i | Can Jump From | Jump Costs \|hi - hj\|                            | Total Costs dp[j] + \|hi - hj\|                                  | dp[i]   |
|---------|---------------|---------------------------------------------------|------------------------------------------------------------------|---------|
| 1       | –             | –                                                 | –                                                                | 0       |
| 2       | 1             | \|30 - 10\| = 20                                   | 0 + 20 = 20                                                      | 20      |
| 3       | 2, 1          | \|40 - 30\| = 10, \|40 - 10\| = 30                 | 20 + 10 = 30, 0 + 30 = 30                                        | 30      |
| 4       | 3, 2, 1       | \|50 - 40\| = 10, \|50 - 30\| = 20, \|50 - 10\| = 40 | 30 + 10 = 40, 20 + 20 = 40, 0 + 40 = 40                          | 40      |
| 5       | 4, 3, 2       | \|20 - 50\| = 30, \|20 - 40\| = 20, \|20 - 30\| = 10 | 40 + 30 = 70, 30 + 20 = 50, 20 + 10 = 30                        | ✅ 30   |

If we have 6th stone then we can reach the 6th stone from 5,4,3 stones only because the K value is only three.
✅ Final dp array (1-based):
```
 i	  1	 2	3	  4	   5
 dp	0	20	30	40	✅30
```
✅ So the minimum cost to reach stone 5 is 30.



