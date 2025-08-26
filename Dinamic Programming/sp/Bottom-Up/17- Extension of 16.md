# PROBLEM
<img width="854" height="467" alt="image" src="https://github.com/user-attachments/assets/20d2da63-04ba-4c1f-adcb-2339ab79d9dd" />

# INTUITION
<img width="765" height="603" alt="image" src="https://github.com/user-attachments/assets/c0d20a65-a5fe-4c68-887e-2c8919aac34f" />
<img width="866" height="146" alt="image" src="https://github.com/user-attachments/assets/1aa84bb4-96ae-4783-8de1-80e1eda09f7e" />


# CODE
```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int MAXN = 100005;
ll dp[MAXN][3];       // dp[i][0]=choose a, dp[i][1]=choose b, dp[i][2]=choose c
int parent[MAXN][3];  // to reconstruct path

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n; 
    cin >> n;
    vector<ll> a(n+1), b(n+1), c(n+1);

    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 1; i <= n; i++) cin >> b[i];
    for (int i = 1; i <= n; i++) cin >> c[i];

    // Base cases
    dp[1][0] = a[1]; parent[1][0] = -1;
    dp[1][1] = b[1]; parent[1][1] = -1;
    dp[1][2] = c[1]; parent[1][2] = -1;

    for (int i = 2; i <= n; i++) {
        // Case 1: pick a[i]
        ll bestA = dp[i-1][0];
        int parA = 0;
        if (i-2 >= 1 && dp[i-2][1] > bestA) { bestA = dp[i-2][1]; parA = 1; }
        if (i-2 >= 1 && dp[i-2][2] > bestA) { bestA = dp[i-2][2]; parA = 2; }
        dp[i][0] = bestA + a[i];
        parent[i][0] = parA;

        // Case 2: pick b[i]
        ll bestB = dp[i-1][1];
        int parB = 1;
        if (i-2 >= 1 && dp[i-2][0] > bestB) { bestB = dp[i-2][0]; parB = 0; }
        if (i-2 >= 1 && dp[i-2][2] > bestB) { bestB = dp[i-2][2]; parB = 2; }
        dp[i][1] = bestB + b[i];
        parent[i][1] = parB;

        // Case 3: pick c[i]
        ll bestC = dp[i-1][2];
        int parC = 2;
        if (i-2 >= 1 && dp[i-2][0] > bestC) { bestC = dp[i-2][0]; parC = 0; }
        if (i-2 >= 1 && dp[i-2][1] > bestC) { bestC = dp[i-2][1]; parC = 1; }
        dp[i][2] = bestC + c[i];
        parent[i][2] = parC;
    }

    // Final maximum
    ll ans = max({dp[n][0], dp[n][1], dp[n][2]});
    cout << "Maximum Earning = " << ans << "\n";

    // Reconstruct the schedule
    int lastChoice;
    if (ans == dp[n][0]) lastChoice = 0;
    else if (ans == dp[n][1]) lastChoice = 1;
    else lastChoice = 2;

    vector<char> schedule(n+1);
    int i = n;
    while (i >= 1) {
        if (lastChoice == 0) schedule[i] = 'A';
        else if (lastChoice == 1) schedule[i] = 'B';
        else schedule[i] = 'C';

        int prevChoice = parent[i][lastChoice];
        if (prevChoice == -1) break;

        // if transition was from i-1, step back 1
        if (prevChoice == lastChoice) i--;
        else i -= 2;

        lastChoice = prevChoice;
    }

    cout << "Schedule: ";
    for (int j = 1; j <= n; j++) cout << schedule[j] << " ";
    cout << "\n";

    return 0;
}

```

<img width="616" height="338" alt="image" src="https://github.com/user-attachments/assets/136b86cb-ac47-48e2-a88e-ea78757dad68" />


---

<img width="621" height="216" alt="image" src="https://github.com/user-attachments/assets/55412e66-c06a-4796-b727-e8649d7f64d7" />
<img width="1132" height="257" alt="image" src="https://github.com/user-attachments/assets/fde1ea2f-2002-4eea-a5ea-b789e072359e" />
<img width="594" height="345" alt="image" src="https://github.com/user-attachments/assets/43e72aac-6e37-4a80-9f81-699b051689ec" />
<img width="591" height="523" alt="image" src="https://github.com/user-attachments/assets/599467fb-5bb7-4829-b63f-ad99ac130793" />
<img width="587" height="175" alt="image" src="https://github.com/user-attachments/assets/a2b29d88-054f-4053-b241-403421b438ac" />

