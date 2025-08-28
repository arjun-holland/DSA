# PROBLEM
<img width="1214" height="844" alt="image" src="https://github.com/user-attachments/assets/c15cff0b-e01e-470c-b731-4cef9bf62a12" />
<img width="1179" height="552" alt="image" src="https://github.com/user-attachments/assets/28ce4c57-09c8-4594-928c-2ecde58b6cd9" />
<img width="1234" height="577" alt="image" src="https://github.com/user-attachments/assets/ebddd703-ed38-428d-b54b-fe15f3054cd7" />
<img width="1193" height="540" alt="image" src="https://github.com/user-attachments/assets/a4029ef5-07cf-4c7c-9785-a3ed412c3900" />
<img width="991" height="543" alt="image" src="https://github.com/user-attachments/assets/6e0743ef-9139-41ea-8537-a458adc4b43e" />


# INTUITION
![WhatsApp Image 2025-08-28 at 14 37 46_834faf3c](https://github.com/user-attachments/assets/2e96ee18-6404-417f-97c8-a27164ec5292)

# CODE
```
//T.C : O(m*n)
//S.C : O(m*n)
class Solution {
public:

    vector<vector<int>> directions = {{1, 1}, {1, -1}, {-1, -1}, {-1, 1}};
                          // diagonal :  0       1         2         3          
    int m, n;
    int t[501][501][4][2];

    int solve(int i, int j, int d, bool canTurn, int val, vector<vector<int>>& grid) {
        int i_ = i + directions[d][0];
        int j_ = j + directions[d][1];

        if(i_ < 0 || i_ >= m || j_ < 0 || j_ >= n || grid[i_][j_] != val) {
            return 0;
        }

        if(t[i_][j_][d][canTurn] != -1) {
            return t[i_][j_][d][canTurn];
        }

        int result = 0;
        int keepMoving = 1 + solve(i_, j_, d, canTurn, val == 2 ? 0 : 2, grid); // for turn = 2  
        result = max(result, keepMoving);  // 1st r = 2;

        if(canTurn == true) {
            int turnAndMove = max(keepMoving, 1 + solve(i_, j_, (d+1)%4, false, val == 2 ? 0 : 2, grid)); //
            result = max(result, turnAndMove);
        }

        return t[i_][j_][d][canTurn] = result;
    }

    int lenOfVDiagonal(vector<vector<int>>& grid) {
        m = grid.size();
        n = grid[0].size();
        memset(t, -1, sizeof(t));

        int result = 0;

        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(grid[i][j] == 1) {
                    for(int d = 0; d <= 3; d++) {
                        result = max(result, 1 + solve(i, j, d, true, 2, grid));
                    }
                }
            }
        }

        return result;

    }
};
```
