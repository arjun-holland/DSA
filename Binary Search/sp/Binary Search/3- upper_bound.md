# Upper bound : Number in array such that greater then the given number with has less index number.
```
📌 Functionality:
- Finds the first index where arr[index] > target.
- Works only on sorted arrays (non-decreasing order).
- Time Complexity: O(log n)
```

# solution 
```
#include <iostream>
#include <vector>
using namespace std;

int upper_bound(const vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;
    int ans = arr.size();    // Default in case all elements ≤ target , default to "no upper bound"

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] > target) {
            ans = mid;         // potential upper bound
            right = mid - 1;   // try smaller index
        } else {
            left = mid + 1;    // search right side
        }
    }

    return ans;    // First index where arr[index] > target
}


int main() {
    vector<int> nums = {1, 3, 3, 5, 8, 8, 10};
    int target = 8;
    int lb =  upper_bound(nums, target);
    cout << "Upper bound index of " << target << " is: " << lb << endl;
    if (lb < nums.size() && nums[lb] == target)
        cout << "Target found at index " << lb << endl;
    else
        cout << "Target not found.\n";
    return 0;
}

```
