# Problem
<img width="1028" height="554" alt="image" src="https://github.com/user-attachments/assets/99b0e31c-751d-486c-be47-f090bb1db2a3" />

<img width="775" height="585" alt="image" src="https://github.com/user-attachments/assets/02a5cd73-b69d-40d8-b129-89aac68c63f2" />

# Intuition
## 🔍 Problem Intuition
```
You're given a 2D matrix (n x m) where:
    - Each cell contains an integer.
    - Positive integers represent "active" or "open" cells.
    - Negative integers represent "blocked" or "unreachable" cells.
    - You are to compute a value for each active cell based on:
    - Sum of all elements outside its connected component that are multiples of its value.
    - Finally, you compute the total sum of these values and subtract the number of blocked cells from the result.
```
## 🧠 Step-by-Step Intuition
### 1. Input and Initial Setup
```
You read an n x m grid of integers.
    - Count how many cells are blocked (< 0) — this count is stored in blockedCount.
    - Track connected components of unblocked (positive) cells using DFS.
```
### 2. Connected Components via DFS
```
You use Depth-First Search (dfs) to group all adjacent positive cells into the same component.
    - A cell can connect to its 4 neighbors (up, down, left, right).
    - This is stored in:
    - components: List of all such components.
    - compId[x][y]: Marks which component each cell belongs to.
```
### 3. Frequency Table (Global Count)
```
You build a global frequency table:
    freq[val] = number of times val appears in the grid    (for val > 0)
Later, for each active cell value x, we want to find how many times its multiples (like 2x, 3x, 4x, etc.) appear outside its component.
```
### 4. Process Each Component Separately
```
For each component:
a. Temporarily Remove Its Values from Global Frequency
    This is important:
    You want to count only the multiples that are outside the current component, because all values in the same component are reachable and hence should be excluded.

b. Compute Each Cell's Answer
    For each cell (x, y) in the component:
    Let val = matrix[x][y]
    Now loop over all multiples of val, and sum:
        sum += freq[mul] * mul
    Why?
    You're computing the total value of all cells outside the component that are multiples of this cell's value.

c. Restore the Frequencies
    You add back the values from this component to the global frequency table — ready to process the next component.
```
### 5. Total Answer and Blocked Penalty
```
Once you've computed the "external multiple sum" for each cell, you:
Sum all the ans[x][y] values.
Subtract blockedCount.
Why subtract?
It seems the problem is designed to penalize each blocked cell by -1, so they're discounted from the final total.
```
## NOTE
```
In order to find the multiplies of x in outside of the current component ,
    We don't need to iterate over all the outside components and find the multiplies of x (Brute Force Way)
    We can use the BLACKBOX method of MULTIPLE PAIRS as {x,y1},{x,y2}
```

<img width="1470" height="631" alt="image" src="https://github.com/user-attachments/assets/c1372b2c-8764-4704-a6b1-e2b9e0d0b630" />


# Code
```
#include <bits/stdc++.h>
using namespace std;

const int MAXV = 1e6 + 1;
vector<pair<int, int>> directions = {{-1, 0}, {1, 0}, {0, 1}, {0, -1}};

// DFS to group connected components of unblocked cells
void dfs(int x, int y, vector<pair<int, int>>& cur_comp, int comp_id,
         vector<vector<int>>& mat, vector<vector<int>>& compId) {
    compId[x][y] = comp_id;
    cur_comp.push_back({x, y});

    for (auto d : directions) {
        int nx = x + d.first;
        int ny = y + d.second;

        if (nx >= 0 && nx < mat.size() && ny >= 0 && ny < mat[0].size() &&
            mat[nx][ny] > 0 && compId[nx][ny] == -1) {
            dfs(nx, ny, cur_comp, comp_id, mat, compId);
        }
    }
}

int main() {
    int n, m;
    cin >> n >> m;

    vector<vector<int>> matrix(n, vector<int>(m));
    vector<vector<int>> compId(n, vector<int>(m, -1));
    vector<vector<pair<int, int>>> components;
    int blockedCount = 0;

    // Input matrix and count blocked cells
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++) {
            cin >> matrix[i][j];
            if (matrix[i][j] < 0) blockedCount++;
        }

    // Identify connected components of unblocked cells
    int cur_comp_id = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            if (matrix[i][j] > 0 && compId[i][j] == -1) {
                vector<pair<int, int>> cur_comp;
                dfs(i, j, cur_comp, cur_comp_id, matrix, compId);
                components.push_back(cur_comp);
                cur_comp_id++; 
            }

    // Global frequency of each positive number
    vector<int> freq(MAXV, 0);
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            if (matrix[i][j] > 0)
                freq[matrix[i][j]]++;

    vector<vector<long long>> ans(n, vector<long long>(m, 0));  

    for (int comp = 0; comp < components.size(); comp++) {
        // Temporarily exclude current component from global freq because they are reachable 
        for (auto& e : components[comp]) {
            int v = matrix[e.first][e.second];
            freq[v]--;
        }

        // Compute sed-values for current component
        for (auto& e : components[comp]) {
            int x = e.first, y = e.second;
            int val = matrix[x][y];
            long long sum = 0;

            // Sum multiples of val that are outside the component
            for (int mul = val; mul < MAXV; mul += val) {
                sum += 1LL * freq[mul] * mul;
            }

            ans[x][y] = sum;
        }

        // Restore frequencies
        for (auto& e : components[comp]) {
            int v = matrix[e.first][e.second];
            freq[v]++;
        }
    }

    // Total sed-value sum, adding 1 per blocked cell
    long long totalSum = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            totalSum += ans[i][j];

    cout << "\n" << totalSum - blockedCount << "\n";

    return 0;
}
```
## Online Code Execution

You can view or run the code online using JDoodle:

👉 [Run on JDoodle](https://www.jdoodle.com/ga/25zz5jfKqLbKoEduRGBN9w%3D%3D)
