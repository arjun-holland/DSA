# PROBLEM
<img width="725" height="656" alt="image" src="https://github.com/user-attachments/assets/39545331-56db-4900-8434-df0deb3174ba" />
<img width="713" height="410" alt="image" src="https://github.com/user-attachments/assets/7112c2f8-8f1b-45c5-9bb7-6df932c843e2" />


# INTUITION
<img width="983" height="606" alt="image" src="https://github.com/user-attachments/assets/ef0992ef-7d01-4d25-adf9-d6ad5b8d4da0" />
<img width="777" height="224" alt="image" src="https://github.com/user-attachments/assets/97f75ce2-a27b-4b11-b58f-e020f4801d89" />

![WhatsApp Image 2025-08-25 at 23 05 03_af4aef2d](https://github.com/user-attachments/assets/bd9cc954-7dd7-4de2-8e57-4e84bc66a281)


# CODE
```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

class Solution {
  public:
    // Function to check if it's possible to make the median 'm' by using at most 'k' operations (increments).
    bool possible(ll m, vector<int>& a, int k) {
        ll used = 0;            // total increments used
        int n = a.size();
        int mid = n / 2;        // index of median (after sorting)
        
        if (n % 2 != 0) {
            // Case 1: Odd size array
            // Median is a[mid], we want to raise it to at least 'm'
            used += max(0LL, m - a[mid]);
        } else {
            // Case 2: Even size array
            // Median is (a[mid-1] + a[mid]) / 2
            // To make median >= m, we need: (a[mid-1] + a[mid]) / 2 >= m
            // Equivalent to: a[mid-1] + a[mid] >= 2*m
            // So, extra needed = max(0, 2*m - (a[mid-1] + a[mid]))
            used += max(0LL, 2*m - a[mid] - a[mid-1]);
        }

        // For values to the right of median, if they are smaller than 'm',
        // we may need to raise them as well so median stays >= m.
        for (int i = mid + 1; i < n; i++) {
            used += max(0LL, m - a[i]);
        }

        // If total increments needed <= allowed k, it's possible
        return used <= k;
    }
  
    int maximizeMedian(vector<int>& arr, int k) {
        int n = arr.size();
        sort(arr.begin(), arr.end());  // Always sort first to find median
        
        ll ans = INT_MIN;  
        ll l = 0;                // Lower bound for possible median
        ll r = arr[n-1] + k;     // Upper bound (max element + all increments)
        
        // Binary search for the maximum possible median
        while (l <= r) {
            ll mid = l + (r - l) / 2;   // we  assume that mid is our median answer
            
            if (possible(mid, arr, k)) {
                ans = mid;       // This median is possible
                l = mid + 1;     // Try for a higher median , try for higher median answer
            } else {
                r = mid - 1;     // Too high, reduce search space
            }
        }
        return ans;
    }
};

```
