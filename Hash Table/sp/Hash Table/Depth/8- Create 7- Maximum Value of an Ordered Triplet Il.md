# Problem 
<img width="1305" height="268" alt="image" src="https://github.com/user-attachments/assets/bc09d916-10fc-4597-a6ff-8121ca225112" />
<img width="1399" height="521" alt="image" src="https://github.com/user-attachments/assets/41615c03-3ac8-4596-9c3c-f8069a978fea" />
<img width="771" height="170" alt="image" src="https://github.com/user-attachments/assets/a7c24830-e2b3-417a-9c59-6d20dfa0f6bf" />

# Intuition
## Brute Force : O(n^3)
```
class Solution {
public:
    long long maximumTripletValue(vector<int>& nums) {
        int n = nums.size();
        long long d = 0;

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = j + 1; k < n; k++) {
                    long long vl = (long long)(nums[i] - nums[j]) * nums[k];
                    d = max(d, vl);
                }
            }
        }

        return d;
    }
};
```
## Good Observation : O(n^2) : As constraints are high its not accepted gives TLE
<img width="932" height="383" alt="image" src="https://github.com/user-attachments/assets/7dd602eb-b81a-49dc-b19a-102e2506a1be" />

`so we need then max i and min j and max k`

<img width="752" height="211" alt="image" src="https://github.com/user-attachments/assets/4f3ade5d-5a3a-4b73-a7ab-0e910e3d91ec" />
<img width="902" height="235" alt="image" src="https://github.com/user-attachments/assets/1d3238bd-7f7a-4f59-8312-2444d9cf7b3f" />
<img width="914" height="238" alt="image" src="https://github.com/user-attachments/assets/63947312-b2a0-4fcd-9bdb-f13f269679be" />
<img width="869" height="91" alt="image" src="https://github.com/user-attachments/assets/a1da3f59-f439-4539-833b-a3d35e62f9b7" />

```
class Solution {
public:
    long long maximumTripletValue(vector<int>& nums) {
        int n = nums.size();
        long long maxValue = 0;

        for (int j = 1; j < n - 1; ++j) {
            int max_i = nums[0];           // Find max nums[i] for i < j
            for (int i = 0; i < j; ++i) {
                max_i = max(max_i, nums[i]);
            }

            // For every k > j, compute expression
            for (int k = j + 1; k < n; ++k) {
                long long value = (long long)(max_i - nums[j]) * nums[k];
                maxValue = max(maxValue, value);
            }
        }
        return maxValue;
    }
};

```

# Optimal : O(n)
<img width="930" height="222" alt="image" src="https://github.com/user-attachments/assets/2341a172-0277-4ac3-ad55-cfeb5c67b19c" />

```
typedef long long ll;

class Solution {
public:
    long long maximumTripletValue(vector<int>& nums) {
        int n = nums.size();
        vector<ll> maxDiffPrefix(n, 0);  // max (nums[i] - nums[j]) up to index i

        maxDiffPrefix[1] = nums[0] - nums[1];
        ll maxLeft = max((ll)nums[0], (ll)nums[1]);      // max(nums[0...i-1])
        ll maxValue = 0;

        for (int k = 2; k < n; ++k) {
            maxDiffPrefix[k] = max(maxDiffPrefix[k - 1], maxLeft - nums[k]);    // Update the best (nums[i] - nums[j]) seen so far

            ll tripletValue = maxDiffPrefix[k - 1] * nums[k];    // Calculate value for current k
            maxValue = max(maxValue, tripletValue);

            maxLeft = max(maxLeft, (ll)nums[k]);     // Update the maximum value on the left for future iterations
        }

        return maxValue;
    }
};

```
