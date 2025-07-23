# Problem
<img width="927" height="345" alt="image" src="https://github.com/user-attachments/assets/26ee075f-a830-48f5-9a2c-e325b5d15910" />

<img width="832" height="328" alt="image" src="https://github.com/user-attachments/assets/3404354e-4798-433e-ab64-486ac647bbcc" />

<img width="503" height="159" alt="image" src="https://github.com/user-attachments/assets/4d661e6d-8324-4187-af4a-809bea026af7" />


# Code
```
class Solution {
public:
    int maximumUniqueSubarray(vector<int>& nums) {
        unordered_set<int> seen;
        int i = 0, j = 0;
        int currSum = 0, maxSum = 0;
        int n = nums.size();

        while (j < n) {
            while (seen.find(nums[j]) != seen.end()) {  // Shrink window from the left
                seen.erase(nums[i]);
                currSum -= nums[i];
                i++;
            }

            seen.insert(nums[j]);
            currSum += nums[j];
            maxSum = max(maxSum, currSum);
            j++;
        }

        return maxSum;
    }
};

```
