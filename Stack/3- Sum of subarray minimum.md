# Problem
```
Given an array arr[] of positive integers, find the total sum of the minimum elements of every possible subarrays.
Note: It is guaranteed that the total sum will fit within a 32-bit unsigned integer.

Examples:
Input: arr[] = [3, 1, 2, 4]
Output: 17
Explanation: Subarrays are [3], [1], [2], [4], [3, 1], [1, 2], [2, 4], [3, 1, 2], [1, 2, 4], [3, 1, 2, 4].
Minimums are 3, 1, 2, 4, 1, 1, 2, 1, 1, 1. Sum of all these is 17.

Constraints:
1 ≤ arr.size() ≤ 3*104
1 ≤ arr[i] ≤ 10^3
```

# Intuition:
## 🎯 Goal:
You want to compute: sum of minimums of all subarrays of arr
Naively, you'd generate all subarrays and find their mins (O(n²) to O(n³)) → way too slow!

## 💡 Optimized Idea:
Each element arr[i] contributes to multiple subarrays as the minimum. So instead of checking all subarrays, ask:
- In how many subarrays is arr[i] the minimum?

Once you know that, you can directly compute its contribution.

## 📦 Key Insight:
If you can compute:
Number of subarrays where arr[i] is the minimum,
Then multiply that count by arr[i] to get its total contribution to the final sum.

## ✅ For each element arr[i], find:
NSL[i]: Nearest Smaller to Left → first index left of i with value < arr[i]

NSR[i]: Nearest Smaller to Right → first index right of i with value ≤ arr[i]

Now:
leftD = i - NSL[i] → number of choices for left boundary of subarray
rightD = NSR[i] - i → number of choices for right boundary
Thus, total subarrays where arr[i] is minimum = leftD * rightD
Total contribution = arr[i] * leftD * rightD

# Example
```
Index:     0   1   2   3
Value:     3   1   2   4

Bars:
      
  ┌─┐         ┌─┐
  │ │     ┌─┐ │ │
  │ │ ┌─┐ │ │ │ │
  3   1   2   4


Visualizing:
Index:   0   1   2   3
Array:   3   1   2   4
NSL:    -1  -1   1   2
NSR:     1   4   4   4

Contribution:
[3]   ← (1*1)    = 3
[1]   ← (2*3)    = 6
[2]   ← (1*2)    = 4
[4]   ← (1*1)    = 4
                 ------
                 Total = 17
```

# Code
```
class Solution {
public:

    vector<int> getNSL(vector<int>& arr, int n) {
        vector<int> result(n);
        stack<int>  st;

        for (int i = 0; i < n; i++) {
            // pop until you find a smaller element or stack becomes empty
            while (!st.empty() && arr[st.top()] >= arr[i]) {
                st.pop();
            }
            // if empty, no smaller to left; else top of stack is NSL
            result[i] = st.empty() ? -1 : st.top();
            st.push(i);
        }
        return result;
    }
    
    vector<int> getNSR(vector<int>& arr, int n) {
        vector<int> result(n);
        stack<int>  st;

        for (int i = n - 1; i >= 0; i--) {
            // pop until you find a strictly smaller element or stack becomes empty
            while (!st.empty() && arr[st.top()] > arr[i]) {
                st.pop();
            }
            // if empty, no smaller to right; else top of stack is NSR
            result[i] = st.empty() ? n : st.top();
            st.push(i);
        }
        return result;
    }

    int sumSubMins(vector<int>& arr) {
        int  n   = arr.size();
        vector<int> NSL = getNSL(arr, n);
        vector<int> NSR = getNSR(arr, n);

        int sum = 0;

        for (int i = 0; i < n; i++) {
            int leftD = i - NSL[i];     // distance to previous smaller on left
            int rightD = NSR[i] - i;    // distance to next smaller on right
    
            sum += arr[i] * leftD * rightD; // each element contributes arr[i] * leftD * rightD
        }
        return sum;
    }
};
```
