# Problem
<img width="752" height="478" alt="image" src="https://github.com/user-attachments/assets/12c9ee00-40a3-49a7-b6df-0d51a4a46995" />


# Intuition

<img width="831" height="190" alt="image" src="https://github.com/user-attachments/assets/982a6fa7-a8f5-44b8-8932-154aee2fa87c" />

## Brute Force : <img width="927" height="144" alt="image" src="https://github.com/user-attachments/assets/d6bddbf4-d7c0-4873-b79a-111f9dcf2c24" />

```
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int countMountainSubarrays(vector<int>& nums) {
        int n = nums.size();
        int count = 0;

        // Try all subarrays of length >= 3
        for (int start = 0; start < n; ++start) {
            for (int end = start + 2; end < n; ++end) {
                // Subarray: nums[start..end]
                int peak = -1;

                // Find peak index (must not be at ends)
                for (int i = start + 1; i < end; ++i) {
                    if (nums[i - 1] < nums[i] && nums[i] > nums[i + 1]) {
                        peak = i;  //peak element index
                        break;
                    }
                }

                if (peak == -1) continue;  // No peak found

                // Check strictly increasing before peak
                bool valid = true;
                for (int i = start + 1; i <= peak; ++i) {
                    if (nums[i - 1] >= nums[i]) {
                        valid = false;
                        break;
                    }
                }

                // Check strictly decreasing after peak
                for (int i = peak + 1; i <= end && valid; ++i) {
                    if (nums[i - 1] <= nums[i]) {
                        valid = false;
                        break;
                    }
                }

                if (valid) {
                    count++;
                }
            }
        }

        return count;
    }
};

int main() {
    Solution sol;
    vector<int> nums = {1, 2, 4, 2, 1};
    int result = sol.countMountainSubarrays(nums);
    cout << result << endl;  // Output: 4
    return 0;
}
```

## Optimal
```
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

int main() {
    int n;
    cin >> n;

    // Input array 'b' (1-based indexing for convenience)
    vector<int> b(n + 2);       

    // Suffix array: suf[i] will store the length of strictly decreasing sequence starting from b[i]
    vector<int> suf(n + 2, 1);  

    // Read input values into array 'b'
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    // Step 1: Build suffix array : suf[i] = number of consecutive decreasing elements starting at index i
    suf[n] = 1;         // last element is always a decreasing sequence of length 1
    for (int i = n - 1; i >= 1; i--) {
        if (b[i] > b[i + 1]) {
            suf[i] = suf[i + 1] + 1;
        } else {
            suf[i] = 1;
        }
    }

    ll count = 0;  // Final count of mountain subarrays
    int c = 0;     // Length of current strictly increasing sequence ending at index i

    // Step 2: Traverse the array to count valid mountain subarrays
    for (int i = 1; i <= n; i++) {
          // If current element is greater than previous, increase the increasing streak
        if (b[i] > b[i - 1]) {
            c++;
        } else {
            // Otherwise, reset the increasing sequence
            c = 1;
        }

        // Valid mountain requires:
        // - Increasing part of at least length 2 (c >= 2)
        // - Decreasing part of at least length 2 (suf[i] >= 2)
        if (c >= 2 && suf[i] >= 2) {
            // Each combination of increasing and decreasing positions forms a unique mountain subarray
            count += (ll)(c - 1) * (suf[i] - 1);
        }
    }

    // Output the result
    cout << count << endl;

    return 0;
}
```
