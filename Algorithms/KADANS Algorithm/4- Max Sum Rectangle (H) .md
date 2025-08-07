# Problem
<img width="894" height="863" alt="image" src="https://github.com/user-attachments/assets/7c18d274-2059-4cd1-baed-8f5f77f1c96e" />
<img width="852" height="393" alt="image" src="https://github.com/user-attachments/assets/a34fcc73-ab37-429f-b4fc-834a802e7cbd" />

# Brute Force : TC : O(n^2 * m^2)
```
class Solution {
public:
    int maxRectSum(vector<vector<int>>& mat) {
        int n = mat.size();       // Rows
        int m = mat[0].size();    // Columns
        int maxSum = INT_MIN;
      
        for (int top = 0; top < n; top++) {
            for (int bottom = top; bottom < n; bottom++) {
                for (int left = 0; left < m; left++) {
                    for (int right = left; right < m; right++) {
                        int sum = 0;
                        for (int i = top; i <= bottom; i++) {
                            for (int j = left; j <= right; j++) {
                                sum += mat[i][j];
                            }
                        }
                        maxSum = max(maxSum, sum);
                    }
                }
            }
        }

        return maxSum;
    }
};
```

# Optimal Code Intuition
```
The question is just the extension of the KADANS algo general question,
general que : Return the maxsum of sub-array in Array which contains both -ve and +ve
present que : Return the maxsum of sub-matrix in matrix  which contains both -ve and +ve

        mat = [[ -3, -5, 3, -1 ]
               [ -9, -6, 6, 3  ]]
then the max sum is 11
    at bottom = 0th index :  temp[] = [ -3, -5, 3, -1 ]
                                    => Apply KADANS Algo it gives max sum => 3
       botttom - 1st index : temp[] = [ (-3 + -9), (-5 + -6), (3 + 6), (-1 + 3) ]
                                    =>[ -12, -11, 9, 2 ]
                                    => Apply KADANS Algo it gives max sum => 11

 At first it considers only the [0th row - 2nd column] as maxsub-matrix as it gives the maxSum
 in the end it considers only the [0th row,1st row - 2nd column, 3rd column] as maxsub-matrix as it gives the maxSum
```

<img width="977" height="347" alt="image" src="https://github.com/user-attachments/assets/0fcc6c36-1035-4130-bb56-dc37e648ebde" />
<img width="1044" height="231" alt="image" src="https://github.com/user-attachments/assets/1c6acc91-4386-4e8f-8aa4-0c867efaef41" />
<img width="937" height="113" alt="image" src="https://github.com/user-attachments/assets/375bd686-72dd-4a1f-9428-80280ff5149a" />

<img width="1133" height="759" alt="image" src="https://github.com/user-attachments/assets/beacae8a-cce9-425e-b0fe-6733beeaaef5" />


# Optinal Code
```

class Solution {
public:
    int maxRectSum(vector<vector<int>> &mat) {
        int n = mat.size();       // Rows
        int m = mat[0].size();    // Columns
        int maxSum = INT_MIN;

        for (int top = 0; top < n; top++) {
            vector<int> temp(m, 0);  //temp[] = column-wise sum from top to bottom rows

            // Fix top row, and expand bottom row
            for (int bottom = top; bottom < n; bottom++) {
                // Compress rows into 1D array
                for (int col = 0; col < m; col++) {
                    temp[col] += mat[bottom][col];
                }

                // Apply Kadane’s Algorithm on the 1D temp array
                int curSum = temp[0], best = temp[0];
                for (int k = 1; k < m; k++) {
                    curSum = max(temp[k], curSum + temp[k]);
                    best = max(best, curSum);
                }

                maxSum = max(maxSum, best);
            }
        }

        return maxSum;
    }
};
```

# Optimla Code for getting the sub-matrix
```
class Solution {
public:
    int maxRectSum(vector<vector<int>>& mat) {
        int n = mat.size();
        int m = mat[0].size();

        int maxSum = INT_MIN;

        // Coordinates of final rectangle
        int finalTop = 0, finalBottom = 0, finalLeft = 0, finalRight = 0;

        for (int top = 0; top < n; top++) {
            vector<int> temp(m, 0);

            for (int bottom = top; bottom < n; bottom++) {
                // Build 1D column-wise sum
                for (int col = 0; col < m; col++) {
                    temp[col] += mat[bottom][col];
                }

                // Apply Kadane's with coordinate tracking
                int curSum = 0, maxHere = INT_MIN;
                int startCol = 0, left = 0, right = 0;

                for (int col = 0; col < m; col++) {
                    if (curSum <= 0) {
                        curSum = temp[col];
                        startCol = col;
                    } else {
                        curSum += temp[col];
                    }

                    if (curSum > maxHere) {
                        maxHere = curSum;
                        left = startCol;
                        right = col;
                    }
                }

                // Update global max and coordinates
                if (maxHere > maxSum) {
                    maxSum = maxHere;
                    finalTop = top;
                    finalBottom = bottom;
                    finalLeft = left;
                    finalRight = right;
                }
            }
        }

        // Optional: Print coordinates
        cout << "Max Sum: " << maxSum << endl;
        cout << "Top: " << finalTop << ", Bottom: " << finalBottom << endl;
        cout << "Left: " << finalLeft << ", Right: " << finalRight << endl;

        return maxSum;
    }
};

```
