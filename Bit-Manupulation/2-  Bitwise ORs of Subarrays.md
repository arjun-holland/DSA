# Problem 
<img width="991" height="353" alt="image" src="https://github.com/user-attachments/assets/fd6f5468-88a4-4c65-a594-8be3c2fba559" />
<img width="950" height="578" alt="image" src="https://github.com/user-attachments/assets/9cd2aeaf-eb43-4b38-b468-e3d8b06c1043" />
<img width="818" height="152" alt="image" src="https://github.com/user-attachments/assets/7c036a64-f705-4907-8682-949008877ee5" />

# Intuition
<img width="1149" height="438" alt="image" src="https://github.com/user-attachments/assets/4f284888-1d87-4744-bf03-b6b41b70be16" />

<img width="971" height="456" alt="image" src="https://github.com/user-attachments/assets/748cfd7c-69a6-4e87-8718-9b36da0feb56" />

# Code
```
class Solution {
public:
    int subarrayBitwiseORs(vector<int>& arr) {
        unordered_set<int> result;   // all distinct OR values
        unordered_set<int> curr;     // OR values ending at current index

        for (int num : arr) {
            unordered_set<int> next;
            next.insert(num);  // start a new subarray from here

            for (int prev : curr) {
                next.insert(prev | num);  // extend previous subarrays
            }

            curr = move(next);  // update current ORs
            result.insert(curr.begin(), curr.end());  // merge into result set
        }

        return result.size();
    }
};

```
<img width="1161" height="465" alt="image" src="https://github.com/user-attachments/assets/6bf7b6f1-f3bf-47aa-b32e-5e517db9c355" />


---

<img width="1148" height="275" alt="image" src="https://github.com/user-attachments/assets/7350b772-93d4-492e-b81d-64194d1c16d9" />
<img width="1132" height="509" alt="image" src="https://github.com/user-attachments/assets/ef8c2414-feab-49ba-95eb-2255acc9b4ba" />
<img width="984" height="531" alt="image" src="https://github.com/user-attachments/assets/13b30dd7-0a53-4d59-9718-1522a3899c1a" />

