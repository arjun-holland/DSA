# Problem
<img width="876" height="926" alt="image" src="https://github.com/user-attachments/assets/9c4ea528-1848-4c5c-bfcf-4c8707e4eb09" />

# Code
```
class Solution {
  public:
    void setMatrixZeroes(vector<vector<int>> &mat) {
        int n = mat.size();       // Get number of rows
        int m = mat[0].size();    // Get number of columns

        set<int> ri, ci;          // Set to store row indices (ri) and column indices (ci) that contain 0

        // Step 1: Identify all rows and columns that need to be set to 0
        for (int r = 0; r < n; r++) {
            for (int c = 0; c < m; c++) {
                if (mat[r][c] == 0) {
                    ri.insert(r);  // Mark row r to be zeroed
                    ci.insert(c);  // Mark column c to be zeroed
                }
            }
        }

        // Step 2: Traverse the matrix again and set elements to 0
        // if their row or column was marked in step 1
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                // If current row or column is marked, set to 0
                if (ri.count(i) > 0 || ci.count(j) > 0) {
                    mat[i][j] = 0;
                }
            }
        }
    }
};

```
