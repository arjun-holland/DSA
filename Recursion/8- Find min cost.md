# PROBLEM
<img width="482" height="780" alt="image" src="https://github.com/user-attachments/assets/4a8c58a7-6389-4431-bbec-d9bb4e7b13a9" />


# CODE
```
#include <bits/stdc++.h>
using namespace std;

long long bruteRecursion(int i, vector<int>& cost, int k, int n) {
    if (i == n) return cost[n];   // Reached last point, include its cost
    if (i > n) return LLONG_MAX;  // Invalid move
    
    long long ans = LLONG_MAX;
    for (int jump = 1; jump <= k; ++jump) {
        if (i + jump <= n) { 
            long long res = bruteRecursion(i + jump, cost, k, n);
            if (res != LLONG_MAX)
                ans = min(ans, cost[i] + res);
        }
    }
    return ans;
}

int main() {
    int n; cin >> n;
    vector<int> cost(n + 1);    // 1-based
    for (int i = 1; i <= n; ++i) cin >> cost[i];
    int k; cin >> k;
    cost[0] = 0;    // cost of starting at 0
    cout << bruteRecursion(0, cost, k, n) << endl;
    return 0;
}
```

```
But the question require to be optmized 
```

```
WE can also write the solve() as

int solve(int i, int n, int k, vector<int>& cost) {
    // Base case: reached last point
    if (i == n) return cost[n];

    int ans = INT_MAX;
    for (int jump = 1; jump <= k; jump++) {
        if (i + jump <= n) {
            ans = min(ans, cost[i] + solve(i + jump, n, k, cost));
        }
    }
    return ans;
}

```


# OPTIMAL CODE
```
#include <bits/stdc++.h>
using namespace std;

long long solve(int i, vector<int>& cost, int k, int n, vector<long long>& dp) {
    if (i == n) return cost[n];          // base case
    if (i > n) return LLONG_MAX;         // invalid
    if (dp[i] != -1) return dp[i];       // already computed

    long long ans = LLONG_MAX;
    for (int jump = 1; jump <= k; ++jump) {
        if (i + jump <= n) {
            long long res = solve(i + jump, cost, k, n, dp);
            if (res != LLONG_MAX)
                ans = min(ans, cost[i] + res);
        }
    }
    return dp[i] = ans;   // store and return
}

int main() {
    int n; cin >> n;
    vector<int> cost(n + 1);    // 1-based
    for (int i = 1; i <= n; ++i) cin >> cost[i];
    int k; cin >> k;
    cost[0] = 0;    // cost of starting at 0

    vector<long long> dp(n + 1, -1);
    cout << solve(0, cost, k, n, dp) << endl;
    return 0;
}

```
