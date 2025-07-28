# Problem
<img width="905" height="605" alt="image" src="https://github.com/user-attachments/assets/934bd9eb-5ff4-46e8-8346-88da9c5b286f" />
<img width="814" height="214" alt="image" src="https://github.com/user-attachments/assets/65ab69a6-f33f-4d75-a5bd-312a69042d1b" />

# Intuition
```
We can solve this with 2 line but its tiem comp is O(nlog n)
       sort(nums.begin(),nums.end());   //O(n logn)
       return nums[(0+nums.size())/2];
```
<img width="1026" height="666" alt="image" src="https://github.com/user-attachments/assets/4d5d947f-cb03-4d4c-ac9d-c82d2eb093db" />
<img width="1158" height="249" alt="image" src="https://github.com/user-attachments/assets/7cff499f-f6de-4297-8531-48f193de2df6" />

# Example
```
✅ Example:
Let’s walk through:  nums = [2, 2, 1, 1, 1, 2, 2]
```
| i | nums\[i] | c | e | Explanation                        |
| - | -------- | - | - | ---------------------------------- |
| 0 | 2        | 1 | 2 | c was 0, so e = 2, c = 1           |
| 1 | 2        | 2 | 2 | Same as e → increment              |
| 2 | 1        | 1 | 2 | Different → decrement              |
| 3 | 1        | 0 | 2 | Different → decrement              |
| 4 | 1        | 1 | 1 | c = 0 → new candidate e = 1, c = 1 |
| 5 | 2        | 0 | 1 | Different → decrement              |
| 6 | 2        | 1 | 2 | c = 0 → new candidate e = 2, c = 1 |

✅ Final candidate = 2 → correct majority element.
✅ Why It's Efficient:
Time Complexity: O(n)
Space Complexity: O(1)
(No extra arrays, maps — just two variables)

# Code
```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int e;              // using moore's voting algorithm
        int c = 0;
        for(int i=0;i<nums.size();i++){
            if(c==0){
                e = nums[i];
                c=1;
            }
            else if(e==nums[i])c++;
            else c--;
        }
        return e;
    }
};
```
