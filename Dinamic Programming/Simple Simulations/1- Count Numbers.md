# Problem
<img width="1017" height="746" alt="image" src="https://github.com/user-attachments/assets/9d6c6000-e885-4f44-90f4-60b7f700e4f6" />
<img width="1019" height="430" alt="image" src="https://github.com/user-attachments/assets/2e9224fa-cdba-4198-b0a9-a241b5ef99cd" />
<img width="1013" height="473" alt="image" src="https://github.com/user-attachments/assets/8c639b22-39f0-4c74-b72f-a41542aebc8b" />

# Intuition


<img width="1100" height="769" alt="image" src="https://github.com/user-attachments/assets/1eb6f91d-b894-43d6-aabb-f363a231cc90" />
<img width="892" height="565" alt="image" src="https://github.com/user-attachments/assets/4a75b3fb-acb7-4e68-b4f0-112aac17df22" />

| Version        | Time Complexity | Space (Stack) | Acceptable for N = 10⁶? |
| -------------- | --------------- | ------------- | ----------------------- |
| Pure Recursion | `O(3^N)`        | `O(N)`        | ❌ No                    |
| Memoized (DP)  | `O(N × 9)`      | `O(N)`        | ✅ Yes                   |



<img width="638" height="207" alt="image" src="https://github.com/user-attachments/assets/771c8c16-995e-4a74-96e8-14256ddcc572" />




# Code
```
#include <iostream>
#include <vector>
using namespace std;

const int MOD = 998244353;
vector<vector<int>> dp; // memoization table
int N;

// Recursive function
int count(int pos, int digit) {
    if (digit < 1 || digit > 9) return 0;         // digits must be in [1, 9]
    if (pos == N) return 1;                       // reached N digits successfully

    if (dp[pos][digit] != -1) return dp[pos][digit];

    int ways = 0;
    ways = (ways + count(pos + 1, digit - 1)) % MOD;
    ways = (ways + count(pos + 1, digit)) % MOD;
    ways = (ways + count(pos + 1, digit + 1)) % MOD;

    return dp[pos][digit] = ways;
}

int user_logic(int n) {
    N = n;
    dp.assign(N, vector<int>(10, -1)); // initialize dp[pos][digit] = -1

    int total = 0;
    for (int d = 1; d <= 9; ++d) {
        total = (total + count(1, d)) % MOD;
    }

    return total;
}

int main() {
    int N;
    cin >> N;
    cout << user_logic(N) << endl;
    return 0;
}
```

---

# Optimal Resursion

<img width="906" height="254" alt="image" src="https://github.com/user-attachments/assets/c836931b-7850-4755-aa97-1752e1b32472" />

<img width="668" height="360" alt="image" src="https://github.com/user-attachments/assets/722d456d-f35e-4d44-bc22-3dea3d22099e" />

<img width="956" height="824" alt="image" src="https://github.com/user-attachments/assets/9fa9173b-6df5-4ad0-a3f6-c350ea3b3594" />
<img width="702" height="87" alt="image" src="https://github.com/user-attachments/assets/12944820-58c6-4234-8f80-d28cc1eac93c" />

<img width="578" height="260" alt="image" src="https://github.com/user-attachments/assets/d3f0bfec-71fd-4392-bbfa-0f81cdf4febc" />


 ---
 
# Optimal Code
```
#include <iostream>
#include <vector>
using namespace std;
const int MOD = 998244353;

int user_logic(int N) {
    vector<long long> prev(10, 0);        // prev[d] = # of ways to make length-(i-1) ending in d
    for (int d = 1; d <= 9; ++d) {
        prev[d] = 1;                     // base case: one way to make 1-digit number ending in d
    }
    for (int i = 2; i <= N; ++i) {
        vector<long long> curr(10, 0);
        for (int d = 1; d <= 9; ++d) {
            curr[d] = prev[d];                // same digit
            if (d - 1 >= 1) curr[d] = (curr[d] + prev[d - 1]) % MOD;
            if (d + 1 <= 9) curr[d] = (curr[d] + prev[d + 1]) % MOD;
        }
        prev = move(curr);
    }
    long long total = 0;
    for (int d = 1; d <= 9; ++d) {
        total = (total + prev[d]) % MOD;
    }
    return total;
}

int main() {
    int N;
    cin >> N;
    cout << user_logic(N) << endl;
    return 0;
}

```
