# PROBLEM
<img width="563" height="709" alt="image" src="https://github.com/user-attachments/assets/90c5b4d0-51a9-4d12-b3a8-6b3235070d7c" />
<img width="535" height="461" alt="image" src="https://github.com/user-attachments/assets/a575c42b-55f4-4338-b47d-46adf2c6d28f" />


# INTUITION
<img width="1060" height="488" alt="image" src="https://github.com/user-attachments/assets/3a71cd64-611c-4012-b3e5-a39284682a29" />

# CODE
```

class Solution {
public:
    vector<int> findDiagonalOrder(vector<vector<int>>& mat) {
        
        int row = mat.size();       // number of rows
        int col = mat[0].size();    // number of columns
        vector<int> ans;            // result array

        int i = 0, j = 0;           // starting position (top-left corner)
        bool upward = true;         // initial direction: going "up-right"

        // Continue until we've visited all elements
        while(ans.size() < row * col){
            ans.push_back(mat[i][j]);   // record the current element

            if(upward){
                // Currently moving "up-right" (↗)

                if(j == col - 1){  
                    // If we are at the last column → must go down
                    i++;
                    upward = false;    // change direction to "down-left"
                } 
                else if(i == 0){       
                    // If we are at the top row → must go right
                    j++;
                    upward = false;    // change direction to "down-left"
                } 
                else {
                    // Otherwise, keep moving "up-right"
                    i--; 
                    j++;
                }
            }
            else {
                // Currently moving "down-left" (↙)

                if(i == row - 1){ 
                    // If we are at the last row → must go right
                    j++;
                    upward = true;     // change direction to "up-right"
                } 
                else if(j == 0){       
                    // If we are at the first column → must go down
                    i++;
                    upward = true;     // change direction to "up-right"
                } 
                else {
                    // Otherwise, keep moving "down-left"
                    i++;
                    j--;
                }
            }
        }

        return ans;   // final traversal order
    }
};

```

---

# INTUITION 2
<img width="892" height="705" alt="image" src="https://github.com/user-attachments/assets/67fea3b0-7ddb-4f98-a941-8454f4e6b628" />
<img width="876" height="531" alt="image" src="https://github.com/user-attachments/assets/087e3950-705d-402c-a41b-596edbe31831" />
<img width="1018" height="165" alt="image" src="https://github.com/user-attachments/assets/9e87d6a6-4433-4612-93a8-3c258f1c71fc" />

<img width="1046" height="295" alt="image" src="https://github.com/user-attachments/assets/80e3a18a-2ca2-477a-938c-0d91419e0c08" />

![WhatsApp Image 2025-08-25 at 23 05 03_c4fbd481](https://github.com/user-attachments/assets/85c24af6-3da1-47dc-9047-39cc9bf71c11)

# CODE
```
class Solution {
public:
    vector<int> findDiagonalOrder(vector<vector<int>>& mat) {
        int m = mat.size(), n = mat[0].size();
        vector<int> ans;
        //ans.reserve(m * n); // optimization: avoid resizing
        
        for (int d = 0; d < m + n - 1; d++) {   //no.of diagonals for m rows and n columns is (m + n - 1)
            // temporary container for current diagonal
            vector<int> temp;
            
            // starting row index
            int r = (d < n) ? 0 : d - n + 1;
            // starting col index
            int c = (d < n) ? d : n - 1;
            
            // collect elements in this diagonal
            while (r < m && c >= 0) {
                temp.push_back(mat[r][c]); 
                r++;
                c--;
            }
            
            // if diagonal index is even → reverse before appending
            if (d % 2 == 0) {
                reverse(temp.begin(), temp.end());
            }
            
            ans.insert(ans.end(), temp.begin(), temp.end());
        }
        
        return ans;
    }
};
```

<img width="1017" height="555" alt="image" src="https://github.com/user-attachments/assets/fd42904c-5c75-4389-9969-7b275d6e18f3" />
