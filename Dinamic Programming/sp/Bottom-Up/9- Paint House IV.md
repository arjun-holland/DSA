# PROBLEM
<img width="961" height="414" alt="image" src="https://github.com/user-attachments/assets/37e822dc-1233-4f0c-9684-7c96992ec518" />
<img width="780" height="298" alt="image" src="https://github.com/user-attachments/assets/8b6971e7-bc51-4b17-a937-92d4fcda7ecc" />
<img width="951" height="171" alt="image" src="https://github.com/user-attachments/assets/619c94fb-d656-4525-9063-5d42c9a8000a" />

# EASY VERSION PROBLEM OF MAIN PROBLEM
<img width="918" height="65" alt="image" src="https://github.com/user-attachments/assets/4d15cefa-d5da-455b-b1b2-658d31d0bdc0" />
<img width="813" height="257" alt="image" src="https://github.com/user-attachments/assets/d5074d3f-7b95-423d-b90c-7c4947eb68e1" />

## INTUITION
![WhatsApp Image 2025-08-21 at 06 25 14_0dc6b844](https://github.com/user-attachments/assets/ff829682-9e5d-4460-bb43-2a2d2c9510f4)
<img width="784" height="545" alt="image" src="https://github.com/user-attachments/assets/acdfe300-54fb-4ff4-8df2-f80f62ec80c9" />
<img width="1753" height="714" alt="image" src="https://github.com/user-attachments/assets/de0ecc2e-bbde-441e-a660-3424d2b18637" />
<img width="1692" height="808" alt="image" src="https://github.com/user-attachments/assets/a455e9c7-c3ec-4ca6-9cad-798cf7f87be3" />


## CODE
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    vector<vector<int>> cost(n, vector<int>(3)); //color cost
    for (int i = 0; i < n; i++) {
        cin >> cost[i][0] >> cost[i][1] >> cost[i][2];
    }

    vector<vector<int>> dp(n, vector<int>(3, 0));

    // Base case
    dp[0][0] = cost[0][0];
    dp[0][1] = cost[0][1];
    dp[0][2] = cost[0][2];

    // Fill dp table
    for (int i = 1; i < n; i++) {
        dp[i][0] = cost[i][0] + min(dp[i-1][1], dp[i-1][2]);
        dp[i][1] = cost[i][1] + min(dp[i-1][0], dp[i-1][2]);
        dp[i][2] = cost[i][2] + min(dp[i-1][0], dp[i-1][1]);
    }
    int ans = min({dp[n-1][0], dp[n-1][1], dp[n-1][2]});
    cout << ans << endl;
    return 0;
}
```

# Main Problem INTUITION
<img width="1762" height="829" alt="image" src="https://github.com/user-attachments/assets/7ab5c4e3-7aa4-4b5a-b8b6-f81ad956637d" />
![Uploading image.png…]()

```
-> dp[1][b][c] = select type “b” guy from row 1 and type “c” guy from row n = min answer to do it 
-> dp[2][b][c] = select type “b” guy from row 2 and type “c” guy from row n-1 + best answer possible for row 1 – n(9 possibilities = min(dp[1][a][a],dp[1][a][b],dp[1][b][b],...................) 
-> 9 possibilities :- min(dp[1][i1][j1])
-> where i1!=j1 and i1!=b and j1!=c as we are selecting the b and c fro 2nd row and n-1 row respectively

-> dp[i][j][k] = select type “j” guy from row i and type “k” guy from row n-i+1 = min answer to do it

-> Final answer = min(dp[n/2][i1][j1]) such that i1!=j1 
```

# Code
```
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

class Solution {
public:
    long long minCost(int n, vector<vector<int>>& cost) {
        // dp[row][i][j] = minimum cost of painting first 'row' pairs of houses
        // where house 'row' (from first) has color i
        // and house (n-row-1) (from last) has color j
        vector<vector<vector<ll>>> dp(n / 2, vector<vector<ll>>(3, vector<ll>(3, LLONG_MAX)));

        // ------------------------------------------------
        // Base Case (row = 0, i.e., house 0 and house n-1)
        // ------------------------------------------------
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (i != j) {  
                    // Constraint 1: Equidistant houses (0, n-1) must differ
                    dp[0][i][j] = cost[0][i] + cost[n-1][j];
                }
            }
        }

        // ----------------------
        // DP Transition
        // ----------------------
        for (int row = 1; row < n / 2; row++) {
            for (int i = 0; i < 3; i++) {        // color for house 'row' : from first
                for (int j = 0; j < 3; j++) {    // color for house (n-row-1) : from last
                    if (i == j) continue;        // Constraint 1: equidistant houses differ

                    ll minPrev = LLONG_MAX;

                    // Look at previous pair (row-1) as we should not select the same color as previous
                    for (int i1 = 0; i1 < 3; i1++) {   // prev left color
                        for (int j1 = 0; j1 < 3; j1++) { // prev right color
                            
                            // Constraints:
                            if (i1 == i) continue;   // Constraint 2: adjacent left houses differ
                            if (j1 == j) continue;   // Constraint 3: adjacent right houses differ
                            if (i1 == j1) continue;  // Constraint 1: previous equidistant pair differ

                            minPrev = min(minPrev, dp[row-1][i1][j1]);
                        }
                    }

                    dp[row][i][j] = minPrev + cost[row][i] + cost[n-row-1][j];
                }
            }
        }

        // ----------------------
        // Final Answer
        // ----------------------
        ll result = LLONG_MAX;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (i != j) {       // last equidistant pair must differ
                    result = min(result, dp[n/2 - 1][i][j]);
                }
            }
        }
        return result;
    }
};

```
