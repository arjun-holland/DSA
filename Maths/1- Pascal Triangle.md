/*
Given an integer numRows, return the first numRows of Pascal's triangle.
In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:

Example 1:
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
*/

//Intuition : Use the Combinatorics formula nCr


//Case  1:complete triangle
class Solution {
public:
    vector<int> genRow(int n){
        vector<int> r;
        r.push_back(1);
        int ans = 1;
        for(int i=1;i<n;i++){
            ans = ans * (n-i);
            ans = ans / i;
            r.push_back(ans);
        }
        return r;
    }
    vector<vector<int>> generate(int n) {
        vector<vector<int>> ans;
        for(int i=0;i<n;i++){
            ans.push_back(genRow(i+1));
        }
        return ans;
    }
};

//Case 2: particular row
class Solution {
  public:
    int solve(int r,int c){  // Case 3 : particular element
        int res = 1;
        for(int i=0;i<c;i++){
            res = res*(r-i);
            res = res/(i+1);
        }
        return res;
    }
    vector<int> nthRowOfPascalTriangle(int n) {
        vector<int> ans;
        for(int i=1;i<=n;i++){ //colums
            ans.push_back(solve(n-1,i-1));  // Case 3 : particular element
        }
        return ans;
    }
};


/* simualation approach
        // Create a 2D vector to store the Pascal's triangle
        vector<vector<int>> ans(n);

        // Loop through each row from 0 to n-1
        for(int i = 0; i < n; i++) {
            // Resize the current row to have (i + 1) elements
            ans[i].resize(i + 1);

            // The first and last elements of each row are always 1
            ans[i][0] = ans[i][i] = 1;

            // Compute the values for the inner elements of the row
            for(int j = 1; j < i; j++) {
                // Each inner element is the sum of the two elements directly above it
                ans[i][j] = ans[i-1][j-1] + ans[i-1][j];
            }
        }

        // Return the generated Pascal's triangle
        return ans;*/

# Code
```
class Solution {
public:
    int value(int r,int c){
        int n = 1;
        for(int i=0;i<c;i++){
            n = n * (r-i);
            n = n / (i+1);
        }
        return n;
    }
    vector<int> row(int n){
        vector<int> r;
        for(int i = 1; i <= n; i++){
            int e = value(n-1,i-1);
            r.push_back(e);
        }
        return r;
    }
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> ans;
        for(int i = 1; i <= numRows; i++){
            vector<int> r = row(i);
            ans.push_back(r);
        }
        return ans;
    }
};
```
