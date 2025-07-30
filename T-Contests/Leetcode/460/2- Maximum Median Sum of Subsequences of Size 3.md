// ✅ LeetCode Problem 3627: Maximum Median Sum of Subsequences of Size 3

---
// 🔗 Submission: [https://leetcode.com/problems/maximum-number-of-subsequences-after-one-inserting/submissions/1716438576/](https://leetcode.com/problems/maximum-median-sum-of-subsequences-of-size-3/submissions/1716203290/)

# Problem
<img width="1030" height="467" alt="image" src="https://github.com/user-attachments/assets/5717d2d6-770a-4192-8a58-5e00ef2d8c62" />
<img width="1008" height="872" alt="image" src="https://github.com/user-attachments/assets/3a7f3f81-14b8-461c-8447-abb88bc02ba4" />
<img width="891" height="205" alt="image" src="https://github.com/user-attachments/assets/8defc4fd-754e-473d-ab3b-6f01525b2200" />

# Intuition
<img width="795" height="402" alt="image" src="https://github.com/user-attachments/assets/11b913af-f594-4167-a90d-4972b8cfbf0f" />
<img width="1110" height="315" alt="image" src="https://github.com/user-attachments/assets/ffa46416-150f-4e65-b7c4-341ef10fd0f2" />
<img width="1142" height="682" alt="image" src="https://github.com/user-attachments/assets/6d53050b-cf87-4cb7-aac6-64afca66c31d" />
<img width="1146" height="577" alt="image" src="https://github.com/user-attachments/assets/2fc39093-d8ac-40ac-ab34-f3d756f6cefd" />
<img width="1154" height="461" alt="image" src="https://github.com/user-attachments/assets/5043199c-7f4c-4bc3-ba9a-4b85423ed4ca" />
<img width="974" height="212" alt="image" src="https://github.com/user-attachments/assets/9b47b57c-8e54-406a-aafb-fc4f739d1c25" />
<img width="1122" height="272" alt="image" src="https://github.com/user-attachments/assets/7610162e-d88c-491d-8af1-211d293adb8a" />


# Code
```
class Solution {
public:
    long long maximumMedianSum(vector<int>& nums) {
        long long sum = 0;
        sort(nums.begin(),nums.end());
        int n = nums.size();
        for(int i = n/3; i < nums.size(); i += 2){
            sum += nums[i];
        }
        return sum;
    }
};
```
