# Problem
<img width="937" height="540" alt="image" src="https://github.com/user-attachments/assets/b24ffe3b-14c5-4f46-a2b6-7234e3b51573" />
<img width="862" height="653" alt="image" src="https://github.com/user-attachments/assets/2749dc8a-684a-4744-87e6-54e65541395e" />


# Intuition
<img width="1155" height="621" alt="image" src="https://github.com/user-attachments/assets/b7e33ebb-68ff-4919-85e3-e2c79fadcee1" />
<img width="1161" height="626" alt="image" src="https://github.com/user-attachments/assets/33847644-2ace-42ab-ad2c-c6abe4b7f9e4" />
<img width="1161" height="256" alt="image" src="https://github.com/user-attachments/assets/bbefddb7-e78d-4443-8a3b-7446ee355841" />
<img width="998" height="562" alt="image" src="https://github.com/user-attachments/assets/a26df192-6c13-4f41-a384-1fb3b746cf54" />
<img width="670" height="393" alt="image" src="https://github.com/user-attachments/assets/0e51d78f-8846-437c-aa08-204aa0414a7f" />


# Code
```
class Solution {
public:
    int longestSubarray(vector<int>& nums) {
        int m = *max_element(nums.begin(),nums.end());
        int a = 0,len = 0;
        for(int i=0;i<nums.size();i++){
            if(nums[i]==m){
                len += 1;
                a = max(a,len);
            }
            else{
                len = 0;
            }
        }
        return a;
    }
};
```
