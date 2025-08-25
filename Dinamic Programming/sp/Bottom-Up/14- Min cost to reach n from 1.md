# PROBLEM
<img width="958" height="232" alt="image" src="https://github.com/user-attachments/assets/8e7a9585-2418-4fbb-8f79-306b2b9189e0" />
<img width="958" height="377" alt="image" src="https://github.com/user-attachments/assets/8bfd15cf-f66f-428c-b6e6-c9246bf0551e" />

# INTUITIOON
<img width="835" height="257" alt="image" src="https://github.com/user-attachments/assets/0d43c564-97f8-4a63-8dcf-33e11dcf67d7" />
<img width="760" height="226" alt="image" src="https://github.com/user-attachments/assets/7b37a8bb-50a9-46c7-9ce4-d2284da6a0d8" />
<img width="977" height="460" alt="image" src="https://github.com/user-attachments/assets/21f26efd-610f-4905-9503-baa350987f71" />

<img width="759" height="477" alt="image" src="https://github.com/user-attachments/assets/7a402f1f-4095-4ee3-bf76-6975b78638a1" />
<img width="747" height="258" alt="image" src="https://github.com/user-attachments/assets/19668d77-013a-4817-9158-05db3162ec4c" />

<img width="917" height="444" alt="image" src="https://github.com/user-attachments/assets/3fa8973d-6308-4ccb-856e-12226bf7f18f" />



<img width="793" height="406" alt="image" src="https://github.com/user-attachments/assets/1140d240-552a-4cae-88ae-64ebbc61f9a8" />
<img width="791" height="329" alt="image" src="https://github.com/user-attachments/assets/8448d145-ff37-49b5-a35d-c26b9a3ae9d8" />
<img width="652" height="424" alt="image" src="https://github.com/user-attachments/assets/b4485743-719f-46d5-b9ec-1067f6c28d46" />
<img width="799" height="575" alt="image" src="https://github.com/user-attachments/assets/2c04f314-e06a-4fc1-a767-ff260a3f9b27" />


## DP TIPS APPLY ON THIS PROBLEM
```
—---> Whichever thing is creating a problem for you in the question l directly make a state for it

dp[i][forward] = dp[i][2] = someone is coming from index i-2 to index i tell me the best answer in that case. 

dp[i][backward] = dp[i][1] = someone is coming from index i+1 to i -> best answer in that case.

```

# CODE
```
#include <bits/stdc++.h>
using namespace std;
const int INF = 1e9; // large value (used for invalid cases)

// dp[i][2] = min cost to reach index i by a forward jump (i-2 -> i)
// dp[i][1] = min cost to reach index i by a backward jump (i+1 -> i)

int main() {
    int n;
    cin >> n;              // size of array
    vector<int> b(n+2, 0); // costs, using 1-based indexing (n+2 to avoid out-of-bounds)

    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    // DP table
    vector<vector<int>> dp(n+2, vector<int>(3, INF));

    // Base case: starting at index 1
    dp[1][2] = b[1];  // we "start" here, so consider it as coming from a forward move
    dp[1][1] = INF;   // can't reach index 1 by backward jump

    // Special case: index 2 can only be reached by backward from index 3 (if exists),
    // but forward is not possible since we only jump +2
    if (n >= 2) {
        dp[2][2] = INF; // can't jump from -0 to 2
        if (n >= 3) {
            // To reach index 2 via backward: (3 -> 2)
            // Means we must have reached index 3 by forward from 1
            dp[2][1] = b[2] + b[3] + dp[1][2]; 
        }
    }

    // Fill DP for indices 3..n
    for (int i = 3; i <= n; i++) {
        // Case 1: forward jump (i-2 -> i)
        dp[i][2] = b[i] + min(dp[i-2][1], dp[i-2][2]);

        // Case 2: backward jump (i+1 -> i)
        if (i+1 <= n) {
            // To reach i from i+1, we must first reach i+1 by forward from i-1
            dp[i][1] = b[i] + b[i+1] + dp[i-1][2];
        }
    }

    // Final answer:
    // You can leave the array by jumping forward from:
    // - last index n
    // - second last index n-1
    int ans = min({dp[n][2], dp[n-1][2], dp[n-1][1]});

    cout << ans << "\n";
    return 0;
}

```
