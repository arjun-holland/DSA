# Problem
<img width="859" height="444" alt="image" src="https://github.com/user-attachments/assets/ca7124cd-0804-464b-a922-31774ba1f366" />
<img width="862" height="821" alt="image" src="https://github.com/user-attachments/assets/965d1b48-d70d-4863-a4bf-2705018914ef" />
<img width="849" height="167" alt="image" src="https://github.com/user-attachments/assets/8091a35c-578a-44f2-9d8a-0af3aa2071c0" />

# Intuition
<img width="1225" height="686" alt="image" src="https://github.com/user-attachments/assets/18a4a954-32c0-410d-af74-5491d4d272d4" />


# Code
```
class Solution {
public:
    int maxOr = 0;      // Stores the maximum OR value
    int count = 0;      // Number of subsets achieving max OR

    void dfs(vector<int>& nums, int index, int currOr) {
        if (index == nums.size()) {
            // Base case: we've built a subset
            if (currOr == maxOr) count++;  // Count it if OR equals max
            return;
        }

        // Option 1: include nums[index]
        dfs(nums, index + 1, currOr | nums[index]);

        // Option 2: exclude nums[index]
        dfs(nums, index + 1, currOr);
    }

    int countMaxOrSubsets(vector<int>& nums) {
        // Step 1: Find the maximum possible OR from all elements
        for (int num : nums) {
            maxOr |= num;
        }

        // Step 2: Start DFS to count all valid subsets
        dfs(nums, 0, 0);

        return count;
    }
};

```
