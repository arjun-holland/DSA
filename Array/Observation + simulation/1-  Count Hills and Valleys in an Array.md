# Problem 
<img width="1008" height="301" alt="image" src="https://github.com/user-attachments/assets/485dee12-3f6a-45c7-a899-dfc97fa8fbc7" />

---
<img width="1021" height="526" alt="image" src="https://github.com/user-attachments/assets/58f7e545-cce9-47f6-8432-973e33c47cd8" />

---
# Code
```
class Solution {
public:
    int countHillValley(vector<int>& nums) {
        int n = nums.size();
        int ct = 0;
        
        for(int i = 1; i < n - 1; ++i) {
            // Skip duplicates to the left
            if(nums[i] == nums[i-1]) continue;

            // Find previous different value
            int l = i - 1;
            while(l >= 0 && nums[l] == nums[i]) l--;

            // Find next different value
            int r = i + 1;
            while(r < n && nums[r] == nums[i]) r++;

            if(l >= 0 && r < n) {
                if((nums[i] > nums[l] && nums[i] > nums[r]) ||
                   (nums[i] < nums[l] && nums[i] < nums[r])) {
                    ct++;
                }
            }
        }
        return ct;
    }
};

```
---

# Time Complexity
<img width="1090" height="246" alt="image" src="https://github.com/user-attachments/assets/78e69a34-6822-4a7b-b985-bea8fceabe2a" />
<img width="973" height="158" alt="image" src="https://github.com/user-attachments/assets/a9ee03ce-9940-474f-9d0f-9ddf2caf8638" />
<img width="1011" height="619" alt="image" src="https://github.com/user-attachments/assets/d935613a-984f-4b1d-af11-6d9513aa9b33" />
<img width="1027" height="427" alt="image" src="https://github.com/user-attachments/assets/ba06784a-0ca1-4968-9b30-583f3c9f25dd" />



