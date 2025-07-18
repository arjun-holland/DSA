# Problem
<img width="903" height="268" alt="image" src="https://github.com/user-attachments/assets/c78fe6bc-46a6-4d6a-ad45-bf7cb5580e5e" />
<img width="839" height="471" alt="image" src="https://github.com/user-attachments/assets/24e8d622-e22f-4178-ac5a-fd742e557d6f" />
<img width="801" height="189" alt="image" src="https://github.com/user-attachments/assets/cff81584-0504-4205-b4c7-07fba80f9231" />

---
<img width="950" height="560" alt="image" src="https://github.com/user-attachments/assets/511ef429-fc82-47a3-88ae-2e8e526f79e6" />
<img width="966" height="226" alt="image" src="https://github.com/user-attachments/assets/dd7aca46-d5c8-4955-bd5a-f2b9c68d6a4e" />

---
# Intuition
<img width="850" height="810" alt="image" src="https://github.com/user-attachments/assets/3c00d0da-961a-47a3-900f-106a60110136" />

---

# Code
```
class Solution {
public:
    vector<int> findThePrefixCommonArray(vector<int>& A, vector<int>& B) {
        // Maps to track whether a number has appeared in A and B respectively
        unordered_map<int,bool> mp1, mp2;
        
        // Mark the first elements of A and B as seen
        mp1[A[0]] = true;
        mp2[B[0]] = true;

        int ans = 0; // Counter for prefix common elements
        vector<int> res; // Result vector to store prefix common counts

        // If A[0] and B[0] are the same, increment ans
        if(mp2[A[0]] == true) ans++;
        res.push_back(ans); // First prefix result

        // Loop through the rest of the arrays
        for(int i = 1; i < A.size(); i++) {
            // If both elements at current index are the same
            if(A[i] == B[i]) {
                // Increment count from previous because both are equal (definitely common)
                res.push_back(res.back() + 1);            
            } else {
                ans = 0; // Reset temporary count

                // If current A[i] has already appeared in B, it's a common element
                if(mp2[A[i]] == true) {
                    ans++;
                } else {
                    // Otherwise, mark it as seen in A
                    mp1[A[i]] = true;
                }

                // If current B[i] has already appeared in A, it's a common element
                if(mp1[B[i]] == true) {
                    ans++;
                } else {
                    // Otherwise, mark it as seen in B
                    mp2[B[i]] = true;
                }

                // Add the newly found common elements to the previous count
                res.push_back(res.back() + ans);
            }
        }
        return res;
    }
};

```
