# Problem
<img width="650" height="491" alt="image" src="https://github.com/user-attachments/assets/53919b65-5745-4fe2-bf5e-3ad8645c5b95" />

# Intuition
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/ae8c074d-2777-4ce3-853f-05b692b4a9d4" />

# Code
```
#include <iostream>
#include <vector>
 
using namespace std;
 
int main() {
    int n;
    cin >> n;
    vector<int> cost(n + 1);
    vector<int> dp(n + 1, 0);
 
    for (int i = 1; i <= n; ++i) {
        cin >> cost[i];
    }

    //BASE CASE
    dp[1] = 0;
    dp[2] = abs(cost[2] - cost[1]);
         cout<<dp[2]<<'\n';
    dp[3] = dp[2] + abs(cost[2]-cost[3]);
         cout<<dp[3]<<'\n';

    for (int i = 4; i <= n; ++i) {
        dp[i] = min(abs(cost[i] - cost[i - 1]) + dp[i - 1], abs(cost[i] - cost[i - 3]) + dp[i - 3]);
        cout<<dp[i];
        cout<<'\n';
    }

    cout << dp[n] << endl;
    return 0;
}
```
