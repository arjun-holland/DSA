# PROBLEM
<img width="927" height="536" alt="image" src="https://github.com/user-attachments/assets/55724a7d-bda6-4738-a184-ef98811d7609" />

# INTUITION
```
Understanding :-> You are given 2 arrays ; travel from start to end;
make maximum dollars ; whenever you try to jump from Array “A” to Array “B” you make no money :) 
```

<img width="1269" height="673" alt="image" src="https://github.com/user-attachments/assets/0c3a052b-925e-4c4a-866e-e9686b0bd87e" />
<img width="823" height="463" alt="image" src="https://github.com/user-attachments/assets/3c5f9d99-f626-4631-b4a6-1210d7d7a4b4" />

## dp[i] = best answer to the question if the size of array was “i” 
<img width="798" height="431" alt="image" src="https://github.com/user-attachments/assets/498888aa-2720-42f8-af57-0ceead3c1243" />
<img width="748" height="429" alt="image" src="https://github.com/user-attachments/assets/22316c17-942a-4290-b9b2-029560322f2c" />


## Formula making
<img width="825" height="437" alt="image" src="https://github.com/user-attachments/assets/c9f97ba1-0148-45fa-bec4-9201c794da32" />
<img width="822" height="430" alt="image" src="https://github.com/user-attachments/assets/23835e3b-4128-4848-9be2-28e6061b3a2e" />

```
-> we really need information at ith index whether we have take element from array A or B   

-> dp[i][a] = best answer to the question if size of both array were “i” and the element picked at the ith index if for sure from array “a”

-> dp[i][b] = best answer to the question if size of both array were i and element picked at ith index is from B

dp[i][a] = max(a[i] + dp[i-1][a] Or a[i] + dp[i-2][b]) 

dp[i][b] = max(b[i] + dp[i-1][b] or b[i] + dp[i-2][a]) 

```

# CODE
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

// DP table where:
// dp[i][0] = best total sum if at position i we picked from array A
// dp[i][1] = best total sum if at position i we picked from array B
ll dp[100005][2];

int main() {
    ll n;
    cin >> n;

    // Arrays a and b are 1-indexed, so we initialize with size n+1
    ll a[n + 1] = {0};
    ll b[n + 1] = {0};

    // Read elements of array A
    for (ll i = 1; i <= n; i++) {
        cin >> a[i];
    }

    // Read elements of array B
    for (ll i = 1; i <= n; i++) {
        cin >> b[i];
    }

    // Base case: At i = 1
    // If we pick from A, total is just a[1]
    // If we pick from B, total is just b[1]
    dp[1][0] = a[1];
    dp[1][1] = b[1];

    // Iterate from i = 2 to n and fill the dp table
    for (ll i = 2; i <= n; i++) {
        // Case 1: Picking a[i] at index i
        // Two options:
        // 1. Previously picked from A (i-1), so we can pick from A again: dp[i-1][0] + a[i]
        // 2. Previously picked from B (i-2), so we skip i-1 and pick from A now: dp[i-2][1] + a[i]
        dp[i][0] = max(dp[i-1][0] + a[i], dp[i-2][1] + a[i]);

        // Case 2: Picking b[i] at index i
        // Two options:
        // 1. Previously picked from B (i-1), so we can pick from B again: dp[i-1][1] + b[i]
        // 2. Previously picked from A (i-2), so we skip i-1 and pick from B now: dp[i-2][0] + b[i]
        dp[i][1] = max(dp[i-1][1] + b[i], dp[i-2][0] + b[i]);
    }

    // Output the best totals for both possibilities at position n
    cout << dp[n][0] << " " << dp[n][1];

    return 0;
}

```
