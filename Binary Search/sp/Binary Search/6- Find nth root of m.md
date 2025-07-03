# Problem
You are given 2 numbers n and m, the task is to find n√m (nth root of m). If the root is not integer then returns -1.

# Examples :
Input: n = 2, m = 9
Output: 3
Explanation: 3^2 = 9
# Constraints:
- 1 <= n <= 30
- 1 <= m <= 10^9
---
# solution :
```
- Intuition
- Find  m^(1/n) = ? like find the nth root of m
- let m^(1/n) = a
- m = a^n [By applying the ^m on both sides]
- HERE, We know 'n','m' values so we want to find the 'a' value
- And the range of 'a' value must be less than or equal to the range of 'm' value because when the 'n' is equal to 1,
- it directly indicates that 'a' is equal to the 'm' , so the ranges are equal
```
```
class Solution {
  public:
    int nthRoot(int n, int m) {
        int l = 1, r = 1e9;    // Define search range of a
        int ans = -1;
        while(l <= r){
            int md = (l+r)/2;
            if(pow(md,n) == m){
                return md;
            }
            else if(pow(md,n) < m){
                l = md + 1;
            }else{
                r = md - 1;
            }
        }
        return ans;
    }
};
```
