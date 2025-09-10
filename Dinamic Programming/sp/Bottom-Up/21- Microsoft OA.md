# PROBLEM EASY VERSION 
<img width="735" height="175" alt="image" src="https://github.com/user-attachments/assets/d76b5858-fff2-4153-a57a-93bbeec2375f" />

## EASY PROBLEM
<img width="910" height="520" alt="image" src="https://github.com/user-attachments/assets/0365ae8d-b32e-4b8c-b494-e2d5d2607de3" />
<img width="763" height="598" alt="image" src="https://github.com/user-attachments/assets/9b38eadc-12e7-403c-93ed-dc704227786a" />
<img width="858" height="355" alt="image" src="https://github.com/user-attachments/assets/0a9ed703-95b9-43c7-a5ae-23768b69c33d" />
<img width="874" height="511" alt="image" src="https://github.com/user-attachments/assets/6d8cfb65-f2c1-41a4-b9c7-0277f9fe498e" />


## CODE
```
#include <iostream>
using namespace std;

int main() {
    int n; cin >> n;
    long long dp[n + 1] = {0};
    dp[0] = 1;
    dp[1] = 1;

    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
        if(i>=4) dp[i] += dp[i-4];
    	  if(i>=6) dp[i] += dp[i-6];
    }
    cout << dp[n] << endl;
    return 0;
}
```

## ACTUAL PROBLEM
<img width="852" height="544" alt="image" src="https://github.com/user-attachments/assets/34cc6989-767d-47d2-8693-2832179aa9eb" />

## INTUITION
<img width="832" height="409" alt="image" src="https://github.com/user-attachments/assets/39f2f26d-45ce-46d5-8bc3-00247ab983e9" />
<img width="894" height="404" alt="image" src="https://github.com/user-attachments/assets/75370c01-a3ff-441b-a901-a0ad950f4d7a" />


## CODE
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; cin >> n;

    // dp[i][j] → number of ways to make sum i using exactly j 4's (j = 0, 1, 2)
    vector<vector<int>> dp(n + 1, vector<int>(3, 0));

    // Base case: there's 1 way to make sum 0 using 0 4s (do nothing)
    dp[0][0] = 1;

    for (int i = 1; i <= n; ++i) {
        // Case 1: use 1 or 2 (they don't affect count of 4s)

        // For 4s used = 0
        if (i >= 1) dp[i][0] += dp[i - 1][0];
        if (i >= 2) dp[i][0] += dp[i - 2][0];
        if (i >= 6) dp[i][0] += dp[i - 6][0];

        // For 4s used = 1
        if (i >= 1) dp[i][1] += dp[i - 1][1];
        if (i >= 2) dp[i][1] += dp[i - 2][1];
        if (i >= 6) dp[i][1] += dp[i - 6][1];

        // For 4s used = 2
        if (i >= 1) dp[i][2] += dp[i - 1][2];
        if (i >= 2) dp[i][2] += dp[i - 2][2];
        if (i >= 6) dp[i][2] += dp[i - 6][2];

        // Now handle 4s specifically:

        // Using one 4
        if (i >= 4) dp[i][1] += dp[i - 4][0]; // adding one 4 to previous 0-fours state

        // Using second 4
        if (i >= 4) dp[i][2] += dp[i - 4][1]; // adding one 4 to previous 1-four state
    }

    // Final result: sum of all ways to make n using at most 2 4s (i.e., 0,1,2 fours)
    int ans = dp[n][0] + dp[n][1] + dp[n][2];
    cout << ans << endl;

    return 0;
}

```

## Folow UP
<img width="811" height="192" alt="image" src="https://github.com/user-attachments/assets/4e084440-4a0a-45db-b6f8-e9c83d8a61ec" />
![Uploading image.png…]()

## CDOE 1
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    // Allowed numbers: 1, 2 (unlimited), 4 (max 2 times), 6 (max 2 times)

    // dp[i][j][k] → number of ways to make sum = i using j 4s and k 6s
    // j ∈ {0,1,2} and k ∈ {0,1,2}
    vector<vector<vector<int>>> dp(n + 1, vector<vector<int>>(3, vector<int>(3, 0)));

    // Base case: There is 1 way to make sum 0 with 0 4s and 0 6s — by choosing nothing
    dp[0][0][0] = 1;

    // Edge case for sum = 1: Only possible with one 1
    if (n > 0) dp[1][0][0] = 1;

    // Iterate through all sums from 2 to n
    for (int i = 2; i <= n; i++) {

        // ----------------------
        // Transitions using 1 and 2 — unlimited use, doesn't affect 4s or 6s count
        // ----------------------

        // No 4s, No 6s
        dp[i][0][0] = dp[i - 1][0][0] + dp[i - 2][0][0];

        // No 4s, 1 or 2 sixes
        dp[i][0][1] = dp[i - 1][0][1] + dp[i - 2][0][1];
        dp[i][0][2] = dp[i - 1][0][2] + dp[i - 2][0][2];

        // 1 four, 0, 1, 2 sixes
        dp[i][1][0] = dp[i - 1][1][0] + dp[i - 2][1][0];
        dp[i][1][1] = dp[i - 1][1][1] + dp[i - 2][0][1];  // note: 4 added in past step
        dp[i][1][2] = dp[i - 1][1][2] + dp[i - 2][1][2];

        // 2 fours, 0, 1, 2 sixes
        dp[i][2][0] = dp[i - 1][2][0] + dp[i - 2][2][0];
        dp[i][2][1] = dp[i - 1][2][1] + dp[i - 2][2][1];
        dp[i][2][2] = dp[i - 1][2][2] + dp[i - 2][2][2];

        // ----------------------
        // Transitions using 6 — add 6 only if total 6s used ≤ 2
        // ----------------------
        if (i >= 6) {
            // From 0 sixes → to 1 six
            dp[i][0][1] += dp[i - 6][0][0];

            // From 1 six → to 2 sixes
            dp[i][0][2] += dp[i - 6][0][1];

            dp[i][1][1] += dp[i - 6][1][0];
            dp[i][1][2] += dp[i - 6][1][1];

            dp[i][2][1] += dp[i - 6][2][0];
            dp[i][2][2] += dp[i - 6][2][1];
        }

        // ----------------------
        // Transitions using 4 — add 4 only if total 4s used ≤ 2
        // ----------------------
        if (i >= 4) {
            // From 0 fours → to 1 four
            dp[i][1][0] += dp[i - 4][0][0];
            dp[i][1][1] += dp[i - 4][0][1];
            dp[i][1][2] += dp[i - 4][0][2];

            // From 1 four → to 2 fours
            dp[i][2][0] += dp[i - 4][1][0];
            dp[i][2][1] += dp[i - 4][1][1];
            dp[i][2][2] += dp[i - 4][1][2];
        }
    }

    // ----------------------
    // Final answer: Sum all dp[n][j][k] where j, k ∈ {0,1,2}
    // ----------------------
    int ans = 0;
    for (int j = 0; j <= 2; j++) {
        for (int k = 0; k <= 2; k++) {
            ans += dp[n][j][k];
        }
    }

    // Output the result
    cout << ans;

    return 0;
}

```

## CODE 2
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; cin >> n;

    // dp[i][j][k] → number of ways to make sum i using j 4's and k 6's (j, k = 0, 1, 2)
    vector<vector<vector<int>>> dp(n + 1, vector<vector<int>>(3, vector<int>(3, 0)));

    // Base case: 1 way to make sum 0 with 0 4s and 0 6s
    dp[0][0][0] = 1;

    for (int i = 1; i <= n; ++i) {
        for (int j = 0; j <= 2; ++j) {      // 4s used
            for (int k = 0; k <= 2; ++k) {  // 6s used

                // 1 and 2 don't affect 4 or 6 count
                if (i >= 1) dp[i][j][k] += dp[i - 1][j][k];
                if (i >= 2) dp[i][j][k] += dp[i - 2][j][k];

                // Use 4 if not exceeding 2
                if (i >= 4 && j > 0)
                    dp[i][j][k] += dp[i - 4][j - 1][k];

                // Use 6 if not exceeding 2
                if (i >= 6 && k > 0)
                    dp[i][j][k] += dp[i - 6][j][k - 1];
            }
        }
    }

    // Sum all valid combinations with 0 to 2 fours and 0 to 2 sixes
    int ans = 0;
    for (int j = 0; j <= 2; ++j) {
        for (int k = 0; k <= 2; ++k) {
            ans += dp[n][j][k];
        }
    }

    cout << ans << endl;
    return 0;
}

```
