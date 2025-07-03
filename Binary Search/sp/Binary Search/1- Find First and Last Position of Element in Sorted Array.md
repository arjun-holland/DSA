# Problem Statement
```
Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.
If target is not found in the array, return [-1, -1].
You must write an algorithm with O(log n) runtime complexity.
```
---
# Example :
```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

# Constraints:
```
0 <= nums.length <= 10^5
-10^9 <= nums[i] <= 10^9
nums is a non-decreasing array.
-10^9 <= target <= 10^9
```
---

# solution 1
```
class Solution {
public:

    vector<int> search(int mid,vector<int>&nums){
        vector<int> ans;
        int least = mid;
        int most = mid;
        while(least>=0 && nums[least]==nums[mid]  ){
            least-=1;
        }
        while(most<=nums.size()-1 && nums[most]==nums[mid] ){
            most+=1;
        }
        ans.push_back(least+1);
        ans.push_back(most-1);
        return ans;
    }

    vector<int> searchRange(vector<int>& nums, int target) {
        int p1=0;
        int p2=nums.size()-1;
        vector<int> ans={-1,-1};
        if(nums.size()==1){
            if(nums[0]==target){
                ans={0,0};
                return ans;
            }
            else{
                return ans;
            }
        }
        while(p1 <= p2){
            int mid=(p1+p2)/2;
            if(nums[mid]==target){
                ans=search(mid,nums);
                break;
            }
            else if(nums[mid]>target){
                p2=mid-1;
            }
            else{
                p1=mid+1;
            }
        }
        return ans;
    }
};
```

# solution 2 : using the upper_bound() , lower_bound()
```
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> a = {-1,-1};
        int si = lower_bound(nums.begin(),nums.end(),target)-nums.begin();
        if (si == nums.size() || nums[si] != target) 
            return a;
        int ei = upper_bound(nums.begin(),nums.end(),target)-nums.begin();

        a = {si,ei-1};
        return a;
    }
};
```

