# 🧠 Two Pointers Approach in DSA

The **Two Pointers** technique is a powerful and efficient method used to solve array or string problems by using two indices (or "pointers") that iterate through the data simultaneously.

---

## ✅ When to Use Two Pointers

Use this approach when:

- ✅ The data structure is **sorted** (most effective!)
- ✅ You want to reduce time complexity from **O(n²)** to **O(n)**
- ✅ You're solving problems like:
  - 🔍 Finding pairs with a given sum
  - 🧹 Removing duplicates from a sorted array
  - 🔁 Checking for palindromes
  - 🔄 Merging sorted arrays
  - 📦 Partitioning arrays

---

## 🧰 How It Works

There are **two main pointer strategies**:

### 🔁 Opposite Direction (Start & End)
Useful in **sorted arrays** to find matching pairs.
```c++
vector<int> twoSumSorted(const vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    while (left < right) {
        int curr_sum = arr[left] + arr[right];

        if (curr_sum == target) {
            return {left, right}; // or {arr[left], arr[right]} if you want the values
        } else if (curr_sum < target) {
            left++;
        } else {
            right--;
        }
    }

    return {}; // Return empty vector if no pair found
}
```
### 🚶 Same Direction (Slow & Fast)
Useful for in-place modifications like removing duplicates.
```
#include <vector>
using namespace std;

int removeDuplicates(vector<int>& nums) {
    if (nums.empty()) return 0;

    int i = 0; // Slow pointer
    for (int j = 1; j < nums.size(); ++j) { // Fast pointer
        if (nums[j] != nums[i]) {
            ++i;
            nums[i] = nums[j];  //put the j th  index value in i th index
        }
    }

    return i + 1; // New length of array with unique elements
}
```

📊 Time & Space Complexity
| Problem                    | Time Complexity | Space Complexity |
| -------------------------- | --------------- | ---------------- |
| Two Sum (sorted)           | O(n)            | O(1)             |
| Remove Duplicates (sorted) | O(n)            | O(1)             |
| Palindrome Check           | O(n)            | O(1)             |




