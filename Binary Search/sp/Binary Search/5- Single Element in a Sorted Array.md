# Problem
You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.
Return the single element that appears only once.
Your solution must run in O(log n) time and O(1) space.

---

# Example :
- Input: nums = [1,1,2,3,3,4,4,8,8]
- Output: 2

# Constraints:
- 1 <= nums.length <= 10^5
- 0 <= nums[i] <= 10^5

---

# solution 1: T.C : O(n) , S.C : O(1)
```
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int a = 0;
    
        for (int e : nums) {      // 🚀 XOR all elements in the array
            a = a ^ e;           // XOR current element with accumulator
        }
        return a;        // 🎯 Only the single unique element remains
    }
};
```
---
🧠 Why Does XOR ( ^ ) Work?
Here are the core XOR properties that make this possible:
| Operation   | Result                              |
| ----------- | ----------------------------------- |
| `a ^ a`     | `0` (any number XOR itself is zero) |
| `a ^ 0`     | `a` (any number XOR 0 is itself)    |
| Commutative | `a ^ b = b ^ a`                     |
| Associative | `(a ^ b) ^ c = a ^ (b ^ c)`         |

--- 

# solution 2: T.C  : O(log n), S.C : O(1)
## The first element of pair is present at the even index and second element of the pair is present at the odd index
## But it will change after a single element, That means the first element is present at the odd index and the second element is present at the even index after a single element occurs 
```
EX: 1 1 2 2 3 4 4 
    0 1 2 3 4 5 6 
            |
```
```
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int l = 0, r = nums.size() - 1;

        while (l < r) {
            int m = (l + r) / 2;

            // 🔁 Pair index trick:
            // if m is even: m^1 = m+1 gives next odd index
            // if m is odd : m^1 = m-1 gives previous even index

            if (nums[m] == nums[m ^ 1]) {
                l = m + 1;     // ✅ Pair is matched correctly, go right
            } else {
                r = m;     // ❌ Mismatch in pair, go left , r = m so we cant exclude the single elemnt : dry run on 1 1 2 3 3 
            }
        }
        return nums[l];   // l == r: this is the single element
    }
};

```
