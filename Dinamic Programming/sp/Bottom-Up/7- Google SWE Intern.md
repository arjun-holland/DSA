<img width="986" height="223" alt="image" src="https://github.com/user-attachments/assets/ef989b92-cb5b-4c68-bca7-0ff195ba4222" /># PROBLEM
<img width="770" height="370" alt="image" src="https://github.com/user-attachments/assets/662bd73f-5889-48dc-965f-71486df09460" />


# INTUITION
<img width="960" height="305" alt="image" src="https://github.com/user-attachments/assets/b3da521e-850d-4730-af0b-7f6d99687691" />
<img width="799" height="296" alt="image" src="https://github.com/user-attachments/assets/d6476c6e-f4b9-4303-97de-afb8aff316bd" />
<img width="938" height="415" alt="image" src="https://github.com/user-attachments/assets/cd98f7dc-8f29-4241-b888-cb2a2459f2c3" />
<img width="809" height="296" alt="image" src="https://github.com/user-attachments/assets/d95b95a4-11e3-4cfa-b197-45ad7c3ce2e7" />
<img width="768" height="130" alt="image" src="https://github.com/user-attachments/assets/94f155fd-7374-4ae5-9d92-f8e96b144e99" />
<img width="957" height="227" alt="image" src="https://github.com/user-attachments/assets/21652c2c-4acf-49c4-aab2-117e0cc39ad7" />


# CODE

```
#include <bits/stdc++.h>
using namespace std;

int maxJourneySum(vector<int>& arr) {
    int n = arr.size(); // 1-based indexing
    vector<int> dp(n+1, INT_MIN);

    dp[1] = arr[1]; // starting point

    for (int i = 2; i <= n; i++) {
        if (i-1 >= 1) dp[i] = max(dp[i], arr[i] + dp[i-1]);
        if (i-3 >= 1) dp[i] = max(dp[i], arr[i] + dp[i-3]);
        if (i-5 >= 1) dp[i] = max(dp[i], arr[i] + dp[i-5]);
    }
    return dp[n];
}

int main() {
    vector<int> arr = {0, 5, 8, 3, 100, -5, -5, 5, 10}; // 1-based indexing
    cout << maxJourneySum(arr) << endl;
    return 0;
}

```
