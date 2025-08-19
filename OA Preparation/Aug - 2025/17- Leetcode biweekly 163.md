# PROBLEM
<img width="936" height="411" alt="image" src="https://github.com/user-attachments/assets/4dd0a705-91c8-4235-9b44-15cf7e767df8" />
<img width="781" height="423" alt="image" src="https://github.com/user-attachments/assets/97349b1b-3a19-469f-9c98-a7d23a770d0d" />
<img width="703" height="245" alt="image" src="https://github.com/user-attachments/assets/a8e2a672-6052-40b9-ac01-9dd8d99fe26a" />

# INTUITION
## Problem Overview
<img width="1040" height="304" alt="image" src="https://github.com/user-attachments/assets/a1f9c23c-67dc-406f-977d-d1c9f2f08a7f" />

## BRUTE FORCE
<img width="926" height="227" alt="image" src="https://github.com/user-attachments/assets/de898142-f56a-47a1-a3f2-05fc6a9e9ac8" />
<img width="921" height="351" alt="image" src="https://github.com/user-attachments/assets/9361bc67-b4b7-449b-81b6-a562c4ea2cc9" />
<img width="915" height="579" alt="image" src="https://github.com/user-attachments/assets/0639748b-b944-4ff2-9d03-06b10c4d326a" />
<img width="925" height="457" alt="image" src="https://github.com/user-attachments/assets/41e0ffac-2461-4a63-9cc0-587fbfe6872f" />
<img width="1056" height="521" alt="image" src="https://github.com/user-attachments/assets/c7223101-b29a-4367-9ce6-549a96ed9b5a" />
```
class Solution {
public:
    int minCost(vector<vector<int>>& grid, int k) {
        int m = grid.size(), n = grid[0].size();
        const int INF = 1e9;
        
        // dp[t][i][j] = min cost to reach (i,j) using at most t teleportations
        vector<vector<vector<int>>> dp(k+1, vector<vector<int>>(m, vector<int>(n, INF)));
        
        dp[0][0][0] = 0;  // starting cell, cost is 0 (do not include grid[0][0] as per problem)

        // Fill dp[0] (no teleportation) using standard DP
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (i > 0)  //make sure we are start from the 2nd row
                    dp[0][i][j] = min(dp[0][i][j], dp[0][i-1][j] + grid[i][j]);
                if (j > 0)  //make sure we are start from the 2nd column 
                    dp[0][i][j] = min(dp[0][i][j], dp[0][i][j-1] + grid[i][j]); // c(01) => c(00) + c(01)
            }
        }  
        //i > 0 : dp[i][j] = dp[i-1][j] + g[i][j]
        //j > 0 : dp[i][j] = dp[i][j-1] + g[i][j]

        // Now calculate dp[t][i][j] for t = 1 to k
        for (int t = 1; t <= k; ++t) {
            // First, allow teleportation from dp[t-1][x][y] to dp[t][i][j] if grid[x][y] >= grid[i][j]
            for (int i = 0; i < m; ++i) {   //for every value
                for (int j = 0; j < n; ++j) {
                    for (int x = 0; x < m; ++x) {  //search value
                        for (int y = 0; y < n; ++y) {
                            if (grid[x][y] >= grid[i][j]) {
                                dp[t][i][j] = min(dp[t][i][j], dp[t-1][x][y]);  // teleport, cost 0
                                
                            }
                        }
                    }
                }
            }

            // Then do regular right/down moves from t-th layer
            for (int i = 0; i < m; ++i) {
                for (int j = 0; j < n; ++j) {
                    if (i > 0)
                        dp[t][i][j] = min(dp[t][i][j], dp[t][i-1][j] + grid[i][j]);
                    if (j > 0)
                        dp[t][i][j] = min(dp[t][i][j], dp[t][i][j-1] + grid[i][j]);
                }
            }
        }

        // Final answer is dp[k][m-1][n-1]
        return dp[k][m-1][n-1];
    }
};
```

## OPTIMAL
<img width="1041" height="333" alt="image" src="https://github.com/user-attachments/assets/2152ead6-6015-4030-a960-3a459996449d" />
<img width="906" height="367" alt="image" src="https://github.com/user-attachments/assets/186681ea-e7f2-4f00-9c4c-456519c2b8ba" />
<img width="910" height="426" alt="image" src="https://github.com/user-attachments/assets/89ea16b8-361c-4462-8ef6-7ef3aeffb598" />
<img width="907" height="389" alt="image" src="https://github.com/user-attachments/assets/7f201105-e0f6-435c-b735-3812dacc658a" />
<img width="1024" height="273" alt="image" src="https://github.com/user-attachments/assets/99b7bd1a-46f1-4d21-9fd3-98ab41c7ec88" />
<img width="904" height="613" alt="image" src="https://github.com/user-attachments/assets/d50ab5cd-279b-422f-b6a7-bda761717c57" />
<img width="1028" height="342" alt="image" src="https://github.com/user-attachments/assets/cfaaf4ce-fc75-4757-9136-1b726a3d64c4" />
<img width="900" height="418" alt="image" src="https://github.com/user-attachments/assets/2b90b1f8-ef28-48e5-a4fb-669e0cb91d61" />
<img width="759" height="173" alt="image" src="https://github.com/user-attachments/assets/b7bdc1e1-5f03-4998-841b-d6149e033255" />

```
class Solution {
public:
    int minCost(vector<vector<int>>& grid, int k) {
        int m = grid.size(), n = grid[0].size();
        const int INF = 1e9;
        vector<vector<vector<int>>> dp(k+1, vector<vector<int>>(m, vector<int>(n, INF)));
        dp[0][0][0] = 0;

        // Regular DP pass for no teleportation
        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j) {
                if (i > 0)
                    dp[0][i][j] = min(dp[0][i][j], dp[0][i-1][j] + grid[i][j]);
                if (j > 0)
                    dp[0][i][j] = min(dp[0][i][j], dp[0][i][j-1] + grid[i][j]);
            }

        // Flatten cells
        vector<tuple<int, int, int>> cells;
        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j)
                cells.emplace_back(grid[i][j], i, j);

        sort(cells.rbegin(), cells.rend());

        for (int t = 1; t <= k; ++t) {
            // Sort cells by grid value descending

            int min_prev = INF;
            int idx = 0;

            for (auto &[val, i, j] : cells) {
                // While grid[x][y] >= val, update min from previous teleportable cells
                while (idx < cells.size() && get<0>(cells[idx]) >= val) {
                    auto &[v, x, y] = cells[idx];
                    min_prev = min(min_prev, dp[t-1][x][y]);
                    ++idx;
                }

                // Apply teleportation
                dp[t][i][j] = min(dp[t][i][j], min_prev);
            }

            // Regular DP movement: right and down
            for (int i = 0; i < m; ++i)
                for (int j = 0; j < n; ++j) {
                    if (i > 0)
                        dp[t][i][j] = min(dp[t][i][j], dp[t][i-1][j] + grid[i][j]);
                    if (j > 0)
                        dp[t][i][j] = min(dp[t][i][j], dp[t][i][j-1] + grid[i][j]);
                }
        }
        return dp[k][m-1][n-1];
    }
};
```
