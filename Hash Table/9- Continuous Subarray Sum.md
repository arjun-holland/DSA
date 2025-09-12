# PROBLEM
<img width="952" height="462" alt="image" src="https://github.com/user-attachments/assets/d43ba2cf-34fb-41af-aa6e-370b3024f9d7" />
<img width="963" height="560" alt="image" src="https://github.com/user-attachments/assets/b26dd62e-5d3b-46cb-b664-d637429861b5" />
<img width="799" height="261" alt="image" src="https://github.com/user-attachments/assets/46db4249-6f7e-456b-9c1c-a9e6f322a3f2" />


# INTUITION
```
  nums = [5, 0, 0, 0];
  k = 3;

Initialize:
  sum = 0;
  mpp = { 0: -1 };

✅ i = 0 → nums[0] = 5
  sum = 0 + 5 = 5
  remainder = 5 % 3 = 2
  mpp = { 0: -1 }
  → remainder 2 not in mpp → mpp[2] = 0
  → No return yet

State:
  sum = 5
  mpp = { 0: -1, 2: 0 }

✅ i = 1 → nums[1] = 0
  sum = 5 + 0 = 5
  remainder = 5 % 3 = 2
  → remainder 2 found in mpp at index 0
  → i - mpp[2] = 1 - 0 = 1 < 2 → not valid yet
  → don't return

State:
  sum = 5
  mpp = { 0: -1, 2: 0 }

✅ i = 2 → nums[2] = 0
  sum = 5 + 0 = 5
  remainder = 5 % 3 = 2
  → remainder 2 found in mpp at index 0
  → i - mpp[2] = 2 - 0 = 2 ✅ ≥ 2 → return true

✅ ✅ Final Result: true
Reason:
  Subarray [0, 0] at indices 1 and 2 (or even 2 and 3) has sum 0, which is a multiple of 3.
```
<img width="917" height="192" alt="image" src="https://github.com/user-attachments/assets/6ccc4436-eb2b-4554-ade9-4ff71d893373" />


# CODE
```
class Solution {
public:
    bool checkSubarraySum(vector<int>& nums, int k) {
        unordered_map<int, int> mpp;
        int sum = 0;
        mpp[0] = -1;

        for(int i = 0; i < nums.size(); i++) {
            sum += nums[i];
            int remainder = sum % k;
            if (mpp.find(remainder) != mpp.end()) {
                if (i - mpp[remainder] >= 2) {
                    return true;
                }
            } else {
                mpp[remainder] = i;
            }
        }
        return false;
    }
};

```
