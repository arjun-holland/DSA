# problem
There is an integer array nums sorted in ascending order (with distinct values).
Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) 
such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed).

For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].
Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.
You must write an algorithm with O(log n) runtime complexity.

# Example:
- Input: nums = [4,5,6,7,0,1,2],
- target = 0
- Output: 4

# Constraints:
- 1 <= nums.length <= 5000
- -10^4 <= nums[i] <= 10^4
- All values of nums are unique.
- nums is an ascending array that is possibly rotated.
- -10^4 <= target <= 10^4

---
# solution : 
- I can solve this with linear search which is going to take the O(n) time complexity
- **use the binary search**: As there are two sorted positions present in the array and the first element of the first sorted portion of array
   is actual greater than the last element of second sorted portion which is a relation and with these relation we can simply solve this with the help of  binary search  
```
// 🔍 LeetCode-style: Search in Rotated Sorted Array
// Time Complexity: O(log n)

class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;

        while (l <= r) {
            int m = l + (r - l) / 2;  // Safe mid calculation

            if (nums[m] == target)
                return m;  // ✅ Found the target

            // 🧭 Determine if we're in the left sorted portion
            if (nums[m] >= nums[0]) {
                // 🎯 Target is either in right half (larger than nums[m])
                // or outside the current sorted portion (less than nums[0])
                if (nums[m] < target || target < nums[0])
                    l = m + 1;
                else
                    r = m - 1;
            }
            // 🧭 Otherwise, we're in the right sorted portion
            else {
                // 🎯 Target is either in left half (less than nums[m])
                // or outside the current sorted portion (greater than nums[end])
                if (nums[m] > target || target > nums[nums.size() - 1])
                    r = m - 1;
                else
                    l = m + 1;
            }
        }

        return -1;  // ❌ Target not found
    }
};

```
