# Lower bound : Number in array such that greater then or equal to the given number with has less index number.
```
📌 Functionality:
- Finds the first index where arr[index] ≥ target.
- Works only on sorted arrays (non-decreasing order).
- Time Complexity: O(log n)
```

# solution 
```
#include <iostream>
#include <vector>
using namespace std;

int lower_bound(const vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;
    int ans = arr.size();  // default to arr.size() in case all elements < target

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] >= target) {
            ans = mid;         // record candidate
            right = mid - 1;   // continue searching left
        } else {
            left = mid + 1;
        }
    }
    return ans;       // First index where arr[index] >= target
}

int main() {
    vector<int> nums = {1, 3, 3, 5, 8, 8, 10};
    int target = 8;
    int lb = lower_bound(nums, target);
    cout << "Lower bound index of " << target << " is: " << lb << endl;
    if (lb < nums.size() && nums[lb] == target)
        cout << "Target found at index " << lb << endl;
    else
        cout << "Target not found.\n";
    return 0;
}

```
