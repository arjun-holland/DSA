# Problem
<img width="567" height="381" alt="image" src="https://github.com/user-attachments/assets/8508657c-ebf0-4823-8a28-d186379e0ba3" />

# Code
```
class Solution {
public:
    int uniquePaths(int m, int n) {
        // Create a 2D DP table with dimensions m x n
        // Initialize all values to 1 because there's only 1 way
        // to reach any cell in the first row or first column
        vector<vector<int>> dp(m, vector<int>(n, 1));
        
        // Fill the DP table starting from cell (1,1)
        for(int i = 1; i < m; ++i) {
            for(int j = 1; j < n; ++j) {
                // The number of unique paths to reach (i,j) is the sum of:
                // paths from the cell above (i-1,j) and from the left (i,j-1)
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        
        // The bottom-right cell contains the total unique paths
        return dp[m-1][n-1];
    }
};
```
