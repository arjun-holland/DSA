# Problem
<img width="631" height="639" alt="image" src="https://github.com/user-attachments/assets/a4c73fb5-bff6-4ff5-b6f8-067ad64da140" />
<img width="621" height="644" alt="image" src="https://github.com/user-attachments/assets/2ae79bde-87db-46ba-944e-1ccc1b668bf9" />

# Code
```
class Solution {
public:
    long long zeroFilledSubarray(vector<int>& nums) {
        long long ans = 0;
        for(int i=0;i<nums.size();){
            if(nums[i] != 0){
                i++;
                continue;
            }
            long long ct = 0, j = i;
            while(j < nums.size() && nums[j] == 0){
                ct++;
                j++;
            }
            ans += (ct * (ct + 1))/2;
            i = j;
        }
        return ans;
    }
};
```
