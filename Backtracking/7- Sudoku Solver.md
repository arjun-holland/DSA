# PROBLEM
<img width="926" height="404" alt="image" src="https://github.com/user-attachments/assets/2ee4e1e7-0f5c-4cee-a919-66233c2876dd" />
<img width="1112" height="719" alt="image" src="https://github.com/user-attachments/assets/e30dd90c-fb98-4564-951d-bc9b7569f95d" />
<img width="997" height="368" alt="image" src="https://github.com/user-attachments/assets/fe779015-319f-4191-a686-db11cdf2499b" />
<img width="989" height="229" alt="image" src="https://github.com/user-attachments/assets/ab52d008-2c70-41d0-a5a5-a9e9139af761" />


# INTUITION

```
As we need to iterate all the ways to complete the Sudoku, we need to use the backtracking,
Cus we need to go back when the way is not working.

we are implementing the code as we do in our realife  
```

## For checking that the submatrix of (i,j) point has char 'c' or not?
<img width="694" height="343" alt="image" src="https://github.com/user-attachments/assets/13ac9ad8-40af-4c77-b2d3-bba23969ec4e" />


# CODE
```
class Solution {
public:

    // Entry function that starts solving the Sudoku
    void solveSudoku(vector<vector<char>>& board) {
        solve(board);      // Start backtracking from here
    }

    // Recursive function that uses backtracking to fill the board
    bool solve(vector<vector<char>>& board) {

        // Loop through each cell in the board
        for (int i = 0; i < board.size(); i++) {
            for (int j = 0; j < board[0].size(); j++) {

                // If the current cell is empty (denoted by '.')
                if (board[i][j] == '.') {

                    // Try placing digits '1' to '9' in the empty cell
                    for (char c = '1'; c <= '9'; c++) {

                        // Check if placing c at (i, j) is valid
                        if (isvalid(board, i, j, c)) {
                            board[i][j] = c;             // Place the digit

                            // Recursively try to solve the rest of the board
                            if (solve(board) == true)
                                return true;          // If successful, stop and return true
                            else
                                board[i][j] = '.'; // Backtrack if it didn't work
                        }
                    }
                    // If no digit from '1' to '9' is valid, return false to backtrack
                    return false;
                }
            }
        }
        //We checked all the cells, If no empty cell is left, the board is completely solved
        return true;
    }

    // Helper function to check whether placing 'c' at (row, col) is valid
    bool isvalid(vector<vector<char>>& board, int row, int col, char c) {

        for (int i = 0; i < 9; i++) {
            // Check the entire column for the same digit
            if (board[i][col] == c) return false;

            // Check the entire row for the same digit
            if (board[row][i] == c) return false;

            // Check the 3x3 subgrid of the c 
            // (3*(row/3), 3*(col/3)) gives starting(top-left) of the 3x3 subgrid box
            int boxRow = 3 * (row / 3) + i / 3;
            int boxCol = 3 * (col / 3) + i % 3;  //when i completely divisible by 3 them increment row , row = 0, 3%3 => 0 => row++ => row = 1

            if (board[boxRow][boxCol] == c) return false;
        }

        // If no conflicts found, placement is valid
        return true;
    }
};

```
