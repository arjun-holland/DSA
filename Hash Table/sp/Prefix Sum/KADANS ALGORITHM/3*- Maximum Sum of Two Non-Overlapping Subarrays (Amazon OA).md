# 🔍 Problem Statement
Given an integer array nums, find two non-overlapping subarrays such that their total sum is maximum.
Each subarray can be empty (i.e., sum = 0), and the subarrays must not overlap.

# 💡 Intuition
1.We need to find two disjoint segments such that:
      Total = max(left subarray) + max(right subarray)
2.The challenge is ensuring non-overlap. So, we:
      Iterate a partition point i from 0 to n:
          Left side: max subarray in nums[0..i]
          Right side: max subarray in nums[i+1..n]
3.At each i, we calculate:
      G[i] = max subarray on left (prefix) + max subarray on right (suffix)
Keep track of the maximum G[i] for all valid i.

We precompute:
      prefixMaxSum[i] = best subarray ending at or before i
      suffixMaxSum[i] = best subarray starting at or after i

# 🛠️ Approach
Use a variation of Kadane's Algorithm to compute max subarray sums from left and right.
At each point i, store the best sum so far from prefix and suffix.
Combine the best left and right subarrays that do not overlap.

Return the maximum of all such combinations.

# ✅ Code in cpp
#include <bits/stdc++.h>
using namespace std;

int maxTwoNonOverlappingSubarrays(const vector<int>& a) {
    int n = a.size();
    if (n == 0) return 0;

    vector<int> leftMax(n), rightMax(n);

    // Kadane left-to-right (no forced 0)
    int curr = a[0], best = a[0];
    leftMax[0] = best;
    for (int i = 1; i < n; ++i) {
        curr = max(a[i], curr + a[i]);
        best = max(best, curr);
        leftMax[i] = best;
    }

    // Kadane right-to-left (no forced 0)
    curr = a[n - 1], best = a[n - 1];
    rightMax[n - 1] = best;
    for (int i = n - 2; i >= 0; --i) {
        curr = max(a[i], curr + a[i]);
        best = max(best, curr);
        rightMax[i] = best;
    }

    // Combine: try every non-overlapping pair
    int maxTotal = INT_MIN;
    for (int i = 0; i < n - 1; ++i) {
        maxTotal = max(maxTotal, leftMax[i] + rightMax[i + 1]);
    }
    return maxTotal;
}

int main() {
    int n;
    cin >> n;
    vector<int> nums(n + 1);
    for (int i = 1; i <= n; i++) {
        cin >> nums[i];
    }
    cout << "Maximum sum of two non-overlapping subarrays: "
         << maxTwoNonOverlappingSubarraysSum(nums) << endl;
    return 0;
}

# ✅ Time & Space Complexity
Time: O(n)
Space: O(n) for prefix and suffix arrays


# dry run
a = [1, -2, 3, 4, -1, 2]

leftMax = [1, 1, 3, 7, 7, 8]
rightMax = [8, 7, 7, 6, 5, 2]

Try all splits:
- leftMax[0] + rightMax[1] = 1 + 7 = 8
- leftMax[2] + rightMax[3] = 3 + 6 = 9 ✅
- leftMax[3] + rightMax[4] = 7 + 5 = 12 ✅ (best)
