# Problem 
<img width="713" height="274" alt="image" src="https://github.com/user-attachments/assets/7f63c12b-f9bd-418d-887a-29dd2cd74ad7" />

# Intuition
<img width="1033" height="343" alt="image" src="https://github.com/user-attachments/assets/913c2285-c5ab-437a-accc-b3b6630f1823" />


# Code
```
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

int countLongestSubarraysWithSumK(vector<int>& a, int k) {
    unordered_map<int, int> mp;  // sum -> first index
    int n = a.size();
    int sum = 0;
    int maxLen = 0;
    int count = 0;

    mp[0] = -1;  // for subarrays starting from index 0

    for (int i = 0; i < n; i++) {
        sum += a[i];

        if (mp.find(sum - k) != mp.end()) {
            int len = i - mp[sum - k];
            if (len > maxLen) {
                maxLen = len;
                count = 1;
            } else if (len == maxLen) {
                count++;
            }
        }

        // store only the first occurrence of sum
        if (mp.find(sum) == mp.end()) {
            mp[sum] = i;
        }
    }

    return count;
}

int main() {
    vector<int> a = {10, 5, 2, 7, 1, 9, 8, 7};
    int k = 15;
    cout << countLongestSubarraysWithSumK(a, k) << endl;  // Output: 1
    return 0;
}

```
