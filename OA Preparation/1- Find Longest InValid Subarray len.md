# Problem 
![image](https://github.com/user-attachments/assets/ddbf4678-3147-4b90-872f-34145701a4c7)
![image](https://github.com/user-attachments/assets/f506a316-5986-4ac2-a3dc-dc6a1690934b)

# Intuition
![image](https://github.com/user-attachments/assets/a87ae116-0259-49c8-b9bc-64bb6b1eba63)

# code
```
#include <bits/stdc++.h>
using namespace std;

int maxLen(int x, vector<int> a) {
    int n = a.size();

    // Compute total sum using prefix
    vector<int> prf(n + 1, 0);
    for (int i = 1; i <= n; ++i) {
        prf[i] = prf[i - 1] + a[i - 1];
    }

    if (prf[n] % x != 0) {
        return n;     //total array is Invalid 
    }

    // Find smallest prefix with prf[i] % x != 0
    int left = -1;
    for (int i = 1; i <= n; ++i) {
        if (prf[i] % x != 0) {
            left = i;
            break;
        }
    }

    // Find largest prefix with prf[i] % x != 0
    int right = -1;
    for (int i = n; i >= 1; i--) {
        if (prf[i] % x != 0) {
            right = i;
            break;
        }
    }

    if (left == -1) {   // All prefix sums divisible by x → all a[i] % x == 0
        return -1;
    }

    // Remove from start or end to get max valid subarray
    return max(n - left, right - 1);
}

int main(){
    vector<int> a = {5, 5, 2, 3, 1};
    int n = 5,k=2;
    cout << maxLen(k,a);
}
```
