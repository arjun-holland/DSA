# Problem 
<img width="675" height="161" alt="image" src="https://github.com/user-attachments/assets/4cda5814-7ac9-4abe-97ff-c5ea5eec2a29" />


# Intuition  
## Brute Force
```
Write 4 for loops to satisy the condition A[i] > A[j] < A[k] >A[l] such that i < j < k < l ;
      TC : O(n^2)
```
## Optimal 
```
First :  A[i] > A[j] : use prefix array to know how many elements are present which are greater than the A[j] are present in range 0 to j-1.
Second :  A[k] > A[l] : use suffix array to know how many elements are present which are lesser than the A[k] are present in range  k+1 to n-1.
Third : A[j] < A[k] : k range is {j+1, n} in this range when we got the A[j] < A[k] then `ans += pref[j] * suf[k]` 
```


# Code
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    int b[n + 1];
    int pref[n + 1] = {0};
    int suf[n + 1] = {0};

    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    pref[1] = 0;   //there is no greater element present at starting index
    int j = 2;
    while (j <= n) {
        int c = 0;
        int i = 1;
        while (i <= j - 1) {
            if (b[i] > b[j]) {
                c++;
            }
            i++;
        }
        pref[j] = c;
        j++;
    }

    suf[n] = 0;   //there is no lesser element present at the ending index
    int k = n - 1;
    while (k >= 1) {
        int c = 0;
        int l = k + 1;
        while (l <= n) {
            if (b[k] > b[l]) {
                c++;
            }
            l++;
        }
        suf[k] = c;
        k--;
    }

    int c = 0;
    j = 1;

    while (j <= n) {
        int k = j + 1;
        while (k <= n) {
            if (b[j] < b[k]) {
                c += pref[j] * suf[k];
            }
            k++;
        }
        j++;
    }
    cout << c;
    return 0;
}

```
