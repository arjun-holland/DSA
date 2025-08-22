# PROBLEM
<img width="484" height="754" alt="image" src="https://github.com/user-attachments/assets/34a8889e-e83a-427a-bbcf-620c799c2be0" />


# INTUITION
```
Here we have to observe that we need to find the minimum cost to reach the N value from 0'th value and we given that we can perform K in regarding to that
So we simply need to check when we are at the i'th index we can come from (i-1),(i-2),(i-3)------ up to where (i-(i-x)) >= 0

We solve this kind of sum earlier the sum name is frog 2 and it is the 6th problem there but the problem statement is like 
 the frog is present at the one index (not 0 index like this current problem) and it has K jumps
 so we need to check that (i-(i-x)) >= 1 when frog is at i'th index as it come from those valid jumps only
```

<img width="549" height="458" alt="image" src="https://github.com/user-attachments/assets/7a9ce9d7-e8d7-46eb-b7dc-4fdd3c995218" />

# CODE
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, k;
    cin >> n;
    vector<long long> cost(n + 1);    // 1-based
    for (int i = 1; i <= n; ++i) cin >> cost[i];
    cin >> k;

    vector<long long> dp(n + 1, LLONG_MAX);
    dp[0] = 0;    // cost to reach start

    for (int i = 1; i <= n; ++i) {
        for (int jump = 1; jump <= k; ++jump) {
            if (i - jump >= 0) {
                dp[i] = min(dp[i], dp[i - jump] + cost[i]);
            }
        }
    }

    cout << dp[n] << endl;
    return 0;
}
```

# RUN HERE
https://ideone.com/X8MevS
