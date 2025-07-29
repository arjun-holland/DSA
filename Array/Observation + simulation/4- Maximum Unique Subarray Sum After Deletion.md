# Problem
<img width="764" height="280" alt="{047BB74F-7C69-45A0-936C-8F5A0A77722A}" src="https://github.com/user-attachments/assets/e81ba60e-dd67-4800-8fe3-e4f8f6b04c20" />
<img width="757" height="602" alt="{226C6E0A-7633-4605-A9D4-E26A7E14BD5B}" src="https://github.com/user-attachments/assets/cc3e368b-9bdb-48fc-a0cc-3c29e895662d" />
<img width="535" height="112" alt="{D2E71738-FBA9-4F32-B4BD-15E443B075BE}" src="https://github.com/user-attachments/assets/d7059310-3538-4ed4-b2cd-d2ef04112c7e" />


# Intuition
<img width="533" height="168" alt="{3CFAD1FF-820C-45C3-BE35-C72F76E9AED9}" src="https://github.com/user-attachments/assets/15024a1f-2a1c-415a-b2a0-50700c840eb1" />


# Code
```
class Solution {
public:
    bool check(vector<int>& nums){    //checking that array contains all negative numbers
        for(int e : nums){
            if(e >= 0)return false;
        }
        return true;
    }

    int helper(vector<int>& ans){
        int res = 0;
        int sum = 0;
        set<int> seen;
        for(int e = 0; e < ans.size() ; e++){
            if(!seen.empty() && seen.count(ans[e])){    
                sum -= ans[e];    //remove the first occurrance of e 
                sum += ans[e];     //add the second occurrance of e 
                res = max(res,sum);   //find the max
            }else{
                seen.insert(ans[e]);   //insert ele in seen set
                sum += ans[e];    //add cur ele to sum 
                res = max(res,sum);    //find the max
            }
        }
        return res;
    }
    int maxSum(vector<int>& nums) {
        if(nums.size() == 1)return nums[0];
        bool isn = check(nums);
        if(isn == true){          //if array contains all negative nbumbers then res is max negative numebr only
            if(nums.size() == 2)return max(nums[0],nums[1]);
            int res = INT_MIN;    
            for(int e : nums){   
                if(res < e){      
                    res = e; 
                }
            }
            return res;
        }
        vector<int> ans;          //array contains -ves and +ves then remove -ves (consider only +ves) as we need to maximize the subarry sum
        for(int e : nums){
            if(e > 0)ans.push_back(e);
        }
        return helper(ans);      //call helper to find the max sum on ans array
    }
};
```
