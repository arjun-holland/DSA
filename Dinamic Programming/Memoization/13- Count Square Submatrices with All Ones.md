# PROBLEM
<img width="910" height="603" alt="image" src="https://github.com/user-attachments/assets/0aa665e0-443e-489e-a4cd-fe69aa5dfa02" />
<img width="833" height="600" alt="image" src="https://github.com/user-attachments/assets/55881b96-c2a3-4cda-b97b-cfcece28f0cd" />

# BRUTE FORCE CODE
 
<img width="958" height="478" alt="image" src="https://github.com/user-attachments/assets/1b80946c-2606-4df2-b501-c81e68e4b696" />


```
We can form a square at (i,j) by going to right, down and diagonal when we have (i,j) = 1;

                (i,j)
                  __ __ __ 
                 |\ 
                 |  \
                 |   \

no.of squares at (i,j) = min(right, down, diagonal)        
```
```
class Solution {
public:
    int solve(vector<vector<int>>& mat,int i,int j){
        if(i >= mat.size() || j >= mat[0].size())return 0;
        if(mat[i][j] == 0)return 0;

        int down = 1+solve(mat,i+1,j);
        int right = 1+solve(mat,i,j+1);
        int diagonal = 1+solve(mat,i+1,j+1);

        return min(down,min(right,diagonal));

    }
    int countSquares(vector<vector<int>>& mat) {
        int res = 0;
        int n = mat.size();
        int m = mat[0].size();

        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                res += solve(mat,i,j);
            }
        }
        return res;
    }
};
```

# OPTIMAL CODE 1 : DP

```
class Solution {
public:

    int solve(vector<vector<int>>& mat,int i,int j,vector<vector<int>>& dp){
        if(i >= mat.size() || j >= mat[0].size())return 0;
        if(mat[i][j] == 0)return 0;
        if(dp[i][j] != -1)return dp[i][j];

        int down = 1+solve(mat,i+1,j,dp);
        int right = 1+solve(mat,i,j+1,dp);
        int diagonal = 1+solve(mat,i+1,j+1,dp);

        return dp[i][j] = min(down,min(right,diagonal));

    }
    int countSquares(vector<vector<int>>& mat) {
        int res = 0;
        int n = mat.size();
        int m = mat[0].size();
        vector<vector<int>> dp(n,vector<int>(m,-1));

        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                res += solve(mat,i,j,dp);
            }
        }
        return res;
    }
};
```

# OPTIMAL CODE 2
```
class Solution {
public:
    bool isSquare(vector<vector<int>>& mat,int i,int j,int sz){
        if(i + sz > mat.size() || j + sz >  mat[0].size())return false;   //check we can form a square of required size or not

        for(int r=i; r<(i+sz); r++){
            for(int c=j; c<(j+sz); c++){
                if(mat[r][c] == 0)return false;
            }
        }
        return true;
    }

    int countSquares(vector<vector<int>>& mat) {
        int n = mat.size();
        int m = mat[0].size();
        int res = 0;
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(mat[i][j] == 1){
                    int size = 1;
                    while(isSquare(mat,i,j,size)){
                        res++;
                        size++;
                    }
                }
            }
        }
        return res;
    }
};
```

# FINAL DP CODE
```
class Solution {
public:
    int countSquares(vector<vector<int>>& mat) {
        int n = mat.size(), m = mat[0].size(), res = 0;
        vector<vector<int>> dp(n, vector<int>(m, 0));

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (mat[i][j] == 1) {
                    if (i == 0 || j == 0)
                        dp[i][j] = 1;
                    else
                        dp[i][j] = 1 + min({dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]});
                        
                    res += dp[i][j];
                }
            }
        }
        return res;
    }
};
```
