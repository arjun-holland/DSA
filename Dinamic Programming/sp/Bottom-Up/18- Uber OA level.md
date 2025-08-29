# PROBLEM 
<img width="830" height="734" alt="image" src="https://github.com/user-attachments/assets/2b11a137-32f2-4c2c-825e-219996d34820" />

# INTUITION
<img width="904" height="216" alt="image" src="https://github.com/user-attachments/assets/a95adf68-d08c-4d26-a5c2-7979d1ded6f9" />
<img width="1059" height="186" alt="image" src="https://github.com/user-attachments/assets/28e7b506-7785-4ba5-82a1-b9f7d3e41cd6" />
<img width="1048" height="590" alt="image" src="https://github.com/user-attachments/assets/597a4cd5-a4d1-462a-9829-0bc4bc2bf5e0" />
<img width="1037" height="585" alt="image" src="https://github.com/user-attachments/assets/699f3265-edec-45c1-afff-e23a8ad58c41" />
<img width="1065" height="736" alt="image" src="https://github.com/user-attachments/assets/3eb67e46-19e0-4f67-8733-defa90191396" />


![WhatsApp Image 2025-08-29 at 09 58 00_59eedeeb](https://github.com/user-attachments/assets/e18e5c97-7ebb-40da-a494-9ee9db5259f0)

# CODE
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll; 

// DP table: dp[i][x][y]
// i = index in arrays
// x = array chosen at i (1 = B, 2 = C)
// y = array chosen at i-1 (1 = B, 2 = C)
// Stores the maximum sum achievable up to index i
ll dp[100000+5][5][5];

// Utility function: returns max of three values
ll mxi(ll x, ll y, ll z) {
    return max(x, max(y, z));
}

// Utility function: returns max of four values
ll mx(ll x, ll y, ll z, ll g) {
    return max(max(x, g), max(y, z));
}

int main() {
    ll n; cin >> n; 
    
    // Arrays B and C (input arrays)
    ll b[n+1] = {0};
    ll d[n+1] = {0};

    // Reading input arrays
    for (ll i = 1; i <= n; i++) {
        cin >> b[i] >> d[i];
    }
    
    // Base cases for index = 1
    dp[1][1][1] = b[1]; // Pick B[1], prev was also B (though invalid forward, needed for DP transitions)
    dp[1][1][2] = b[1]; // Pick B[1], prev assumed C and C[-1] is not there so we take the B[1]
    dp[1][2][1] = d[1]; // Pick C[1], prev assumed B and B[-1] is not there so we take the C[1]
    dp[1][2][2] = d[1]; // Pick C[1], prev was C and C[-1] is not there so we take the C[1]

    // Fill DP table for indices from 2 → n
    for (ll i = 2; i <= n; i++) {
        // Case 1: Pick B[i] and also B[i-1]
        // Then previous (i-2) must have ended with C (to avoid 3 consecutive B’s)
        dp[i][1][1] = b[i] + b[i-1] + max(dp[i-2][2][2], dp[i-2][2][1]);

        // Case 2: Pick B[i] but C[i-1]
        // Then (i-2) could have been anything except invalid consecutive triples
        dp[i][1][2] = b[i] + d[i-1] + mxi(dp[i-2][1][1], dp[i-2][1][2], dp[i-2][2][1]);

        // Case 3: Pick C[i] but B[i-1]
        dp[i][2][1] = d[i] + b[i-1] + mxi(dp[i-2][2][1], dp[i-2][2][2], dp[i-2][1][2]);

        // Case 4: Pick C[i] and also C[i-1]
        // Then previous (i-2) must have ended with B
        dp[i][2][2] = d[i] + d[i-1] + max(dp[i-2][1][2], dp[i-2][1][1]);
    }

    // Final answer = max of all valid possibilities at index n
    cout << mx(dp[n][1][1], dp[n][1][2], dp[n][2][2], dp[n][2][1]);

    return 0; 
}

```

<img width="950" height="211" alt="image" src="https://github.com/user-attachments/assets/a2d2ccfd-0e2a-4fa6-90ef-1b36d4b93429" />
