<img width="1036" height="182" alt="image" src="https://github.com/user-attachments/assets/82b9a1e4-8b4c-48f5-a9f0-b599e36599f6" />
<img width="1079" height="543" alt="image" src="https://github.com/user-attachments/assets/e5fb8682-c8fa-43bf-a9d9-6ae436463f03" />
<img width="1054" height="752" alt="image" src="https://github.com/user-attachments/assets/49a29f84-bcad-45f2-bd37-9da76c1c61d4" />

<img width="1053" height="407" alt="image" src="https://github.com/user-attachments/assets/243e0c43-bef6-40c4-8fc8-6bdfd02c5b5b" />
<img width="1047" height="224" alt="image" src="https://github.com/user-attachments/assets/67a1d89a-a18b-4a3e-89f6-d25ccfa7fcb2" />

## EXAMPLE FOR 2D - DP
<img width="1074" height="548" alt="image" src="https://github.com/user-attachments/assets/0c959b05-d926-4934-8d23-39959edf9e62" />
<img width="1070" height="739" alt="image" src="https://github.com/user-attachments/assets/34b89e51-df4d-4673-b3ef-304491e3eb82" />
<img width="893" height="734" alt="image" src="https://github.com/user-attachments/assets/9f1c9a15-c7c9-4428-bbde-1a4b214032ff" />


<img width="790" height="192" alt="image" src="https://github.com/user-attachments/assets/aec4ed1b-6fca-4986-b6f1-3828d1250e5b" />




### CODE
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> a(n+1), b(n+1);
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
    }
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    // dp[i][0] = max EVEN sum ending at index i
    // dp[i][1] = max ODD  sum ending at index i
    vector<vector<long long>> dp(n+1, vector<long long>(2, -1e15));

    // Base case: index 1 can start either from a[1] or b[1]
    dp[1][a[1] % 2] = max(dp[1][a[1] % 2], 1LL * a[1]);
    dp[1][b[1] % 2] = max(dp[1][b[1] % 2], 1LL * b[1]);

    // Transition
    for (int i = 2; i <= n; i++) {
        // Try picking from a[i]
        if (a[i] % 2 == 0) {
            // even value -> parity stays same
            dp[i][0] = max(dp[i][0], dp[i-1][0] + a[i]);  //whay compare dp[i][0] that is current statent as we have to use the a[], b[] and gety the max one only 
            dp[i][1] = max(dp[i][1], dp[i-1][1] + a[i]);
        } else {
            // odd value -> parity flips
            dp[i][0] = max(dp[i][0], dp[i-1][1] + a[i]);
            dp[i][1] = max(dp[i][1], dp[i-1][0] + a[i]);
        }

        // Try picking from b[i]
        if (b[i] % 2 == 0) {
            dp[i][0] = max(dp[i][0], dp[i-1][0] + b[i]);
            dp[i][1] = max(dp[i][1], dp[i-1][1] + b[i]);
        } else {
            dp[i][0] = max(dp[i][0], dp[i-1][1] + b[i]);
            dp[i][1] = max(dp[i][1], dp[i-1][0] + b[i]);
        }
    }

    cout << "Max EVEN sum = " << dp[n][0] << endl;
    cout << "Max ODD sum  = " << dp[n][1] << endl;
}
```

## Example For 3D - DP

