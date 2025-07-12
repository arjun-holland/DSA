# Problem
Select maximum sum subset from the two arrays such that no two elements are consecutive.

# Intuition
🧠 Recurrence Relation Recap
  `dp[i] = max(dp[i-1], max(a1[i], a2[i]) + dp[i-2])`
```
Where:
dp[i] is the maximum sum you can get considering up to the ith column.
- dp[i-1] means the max previous value
- max(a1[i], a2[i]) ensures you're picking the better element at index i ans add the non adjacent element value.

```
<img width="1599" height="718" alt="image" src="https://github.com/user-attachments/assets/87827d4b-fd28-4aed-b7ee-03a363bb9e16" />


# Code
```
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int maxSubsetSumNoConsecutive(const vector<int>& a1, const vector<int>& a2) {
    int n = a1.size();
    if (n == 0) return 0;

    vector<int> dp(n, 0);

    // Base case for first element
    dp[0] = max(a1[0], a2[0]);

    if (n == 1) return dp[0];

    // Base case for second element
    dp[1] = max(dp[0], max(a1[1], a2[1]));

    // Fill dp array using recurrence
    for (int i = 2; i < n; ++i) {
        int pick = max(a1[i], a2[i]) + dp[i - 2]; // Include current
        int skip = dp[i - 1];                     // Exclude current
        dp[i] = max(pick, skip);
    }

    return dp[n - 1];
}

int main() {
    vector<int> a1 = {1, 5, 3, 21234};
    vector<int> a2 = {-4509, 200, 3, 40};

    int result = maxSubsetSumNoConsecutive(a1, a2);
    cout << "Maximum sum of subset with no consecutive picks: " << result << endl;

    return 0;
}

```
