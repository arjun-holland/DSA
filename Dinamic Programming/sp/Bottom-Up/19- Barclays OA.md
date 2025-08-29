# PROBLEM
<img width="667" height="708" alt="image" src="https://github.com/user-attachments/assets/652f4165-0c21-4ed4-9b67-e696364f159f" />
<img width="656" height="239" alt="image" src="https://github.com/user-attachments/assets/28b9977b-ded9-4521-a365-f38828edea7c" />
<img width="714" height="386" alt="image" src="https://github.com/user-attachments/assets/d74ea059-6891-4f39-98f7-72a09a24c474" />


# INTUITION
```
// Problem:
// Stephen works for N days. Each day he can do:
//   - Easy task (anytime)
//   - Difficult task (only if he rested the previous day)
//   - No task (rest)
//
// Goal: Maximize the salary he earns.
```
<img width="826" height="304" alt="image" src="https://github.com/user-attachments/assets/24beca32-726a-449d-8174-5ae19bb73313" />
<img width="849" height="260" alt="image" src="https://github.com/user-attachments/assets/266ebb68-2977-4250-9851-d13adb1fe51c" />
<img width="911" height="228" alt="image" src="https://github.com/user-attachments/assets/f78c3ae4-8a31-41cd-98e5-55d008e25e37" />
<img width="909" height="469" alt="image" src="https://github.com/user-attachments/assets/2bb7ead9-1ad5-43ee-afce-790a19ba7fc7" />
<img width="900" height="350" alt="image" src="https://github.com/user-attachments/assets/fa89b1b8-0b11-42eb-8b36-5ae1c882d2df" />
<img width="892" height="509" alt="image" src="https://github.com/user-attachments/assets/01932e57-06af-4ced-adef-a718ae101d71" />


<img width="863" height="160" alt="image" src="https://github.com/user-attachments/assets/8eceeada-9ea5-4157-97a3-f2252a22d9f4" />


# CODE
```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;


ll dp[200005][4];  
// dp[i][state]:
//   i = current day
//   state = 1 → did Easy task on day i
//   state = 2 → did Hard task on day i
//   state = 3 → did No task on day i

int main() {
    ll n, type;  
    cin >> n >> type;   // type is always 2 (easy + hard)

    vector<ll> easy(n + 1), hard(n + 1);

    // Input arrays
    for (int i = 1; i <= n; i++) {
        cin >> easy[i] >> hard[i];
    }

    // Base cases for day 1
    dp[1][1] = easy[1];   // do easy task on day 1
    dp[1][2] = hard[1];   // do hard task on day 1
    dp[1][3] = 0;         // do nothing on day 1

    // Fill DP table
    for (int i = 2; i <= n; i++) {
        // Case 1: Do Easy task today
        // Can come from any of yesterday's states (easy, hard, or rest)
        dp[i][1] = easy[i] + max({dp[i-1][1], dp[i-1][2], dp[i-1][3]});

        // Case 2: Do Hard task today
        // Allowed only if yesterday was "rest"
        dp[i][2] = hard[i] + dp[i-1][3];

        // Case 3: Do Nothing today so salary is 0
        // Salary = best of yesterday, carry forward
        dp[i][3] = 0 + max({dp[i-1][1], dp[i-1][2], dp[i-1][3]});
    }

    // Answer = maximum possible salary on last day
    cout << max({dp[n][1], dp[n][2], dp[n][3]}) << "\n";

    return 0;
}

```
