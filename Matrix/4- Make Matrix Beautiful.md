# Problem
<img width="954" height="717" alt="image" src="https://github.com/user-attachments/assets/104a4535-5def-4af1-9a8e-07e83ea0b332" />
<img width="896" height="671" alt="image" src="https://github.com/user-attachments/assets/fecdfa11-4aa5-4950-8dd7-408316d80808" />

# Intuition
<img width="1174" height="605" alt="image" src="https://github.com/user-attachments/assets/68eaadfd-4c18-4065-98f5-6b1cfffb8355" />
<img width="1139" height="352" alt="image" src="https://github.com/user-attachments/assets/6acffb39-04cb-4ea5-ab44-c879c1c800d0" />


# Code
```
class Solution {
  public:
    int balanceSums(vector<vector<int>>& mat) {
        int ans = 0;
        vector<int> rs;

        // Step 1: Calculate row sums and find the maximum row sum
        for(auto r : mat){
            int cs = 0;
            for(int e : r){
                cs += e;  // Sum up elements in the row
            }
            ans = max(ans, cs);  // Track the max row sum
            rs.push_back(cs);    // Store row sum
        }

        int res = 0;
        // Step 2: Calculate operations to make all row sums equal to the max row sum
        for(int i = 0; i < rs.size(); i++){
            if(rs[i] == ans) continue;           // If already equal, skip
            res += (ans - rs[i]);                // Add how much this row is short
        }

        vector<int> cs;
        int ans1 = 0;

        // Step 3: Calculate column sums and find the maximum column sum
        for(int i = 0; i < mat.size(); i++){
            int c = 0;
            for(int j = 0; j < mat.size(); j++){
                c += mat[j][i];  // Sum up column i
            }
            ans1 = max(ans1, c);  // Track the max column sum
            cs.push_back(c);      // Store column sum
        }

        int res1 = 0;
        // Step 4: Calculate operations to make all column sums equal to the max column sum
        for(int i = 0; i < cs.size(); i++){
            if(cs[i] == ans1) continue;          // ❗ Bug: should be `cs[i] == ans1`, but left unchanged as per your request
            res1 += (ans1 - cs[i]);              // Add how much this column is short
        }

        // Step 5: Return the maximum of row-based or column-based operations
        return max(res, res1);
    }
};

```
