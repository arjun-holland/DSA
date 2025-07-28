# Problem
<img width="1258" height="356" alt="image" src="https://github.com/user-attachments/assets/d5b0ba89-3002-4747-9305-415694563ef0" />
<img width="1225" height="774" alt="image" src="https://github.com/user-attachments/assets/39f2abf4-290c-41c8-a735-4e9a15e8ca82" />
<img width="1063" height="314" alt="image" src="https://github.com/user-attachments/assets/e5a856d2-6ec0-4326-9ff2-6ae74b8ea48c" />


# Intuition
<img width="1011" height="293" alt="image" src="https://github.com/user-attachments/assets/62ff9f7a-f781-4d9a-8027-2246d2c5cc62" />
<img width="1052" height="714" alt="image" src="https://github.com/user-attachments/assets/6ddd60c8-0e88-4ddc-b267-1915b427520b" />
<img width="1365" height="717" alt="image" src="https://github.com/user-attachments/assets/7ae5ea87-ffda-4832-ab12-ee486401fe4f" />
<img width="1090" height="288" alt="image" src="https://github.com/user-attachments/assets/c40661b2-0bfa-4058-a865-7a1c5efb43b3" />


# Code
```
class Solution {
public:
    long long maxSubarrays(int n, vector<vector<int>>& conflictingPairs) {
        // Map to store for each end index `e`, the list of start indices `s` such that (s,e) is a conflict pair
        unordered_map<int, vector<int>> conflictEndValues;

        // Step 1: Normalize and populate conflict pairs
        for (auto& p : conflictingPairs) {
            int s = p[0];
            int e = p[1];

            if (s > e) swap(s, e);  // Ensure s <= e to simplify later checks

            conflictEndValues[e].push_back(s);  // Group conflict pairs by their end index
        }

        int maxConflict = 0;                  // Track the furthest left conflict start seen so far
        int secondMaxConflict = 0;            // Track second maximum for optimization
        vector<long long> extra(n + 1, 0);    // Store potential "bonus subarrays" when a conflict pair is removed
        long long ans = 0;

        // Step 2: Iterate from 1 to n (array values in nums)
        for (int e = 1; e <= n; e++) {
            // Check if current index `e` has any conflict pairs ending here
            for (int& u : conflictEndValues[e]) {
                if (u >= maxConflict) {              // Update maxConflict and secondMaxConflict if u is bigger
                    secondMaxConflict = maxConflict;
                    maxConflict = u;
                } else if (u > secondMaxConflict) {
                    secondMaxConflict = u;
                }
            }

            // All subarrays ending at 'e' and starting after maxConflict are valid
            ans += (e - maxConflict);

            // Calculate bonus if the max conflict edge is removed
            extra[maxConflict] += maxConflict - secondMaxConflict;   //blocked pairs 
        }

        // Step 3: Return base answer + the best possible gain from removing one conflict
        return ans + *max_element(extra.begin(), extra.end());
    }
};

```
