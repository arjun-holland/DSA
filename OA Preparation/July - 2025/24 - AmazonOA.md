# Problem
<img width="1373" height="552" alt="image" src="https://github.com/user-attachments/assets/c955586a-6fdf-49a8-a5e4-4c7e08eb8ced" />
<img width="1029" height="624" alt="image" src="https://github.com/user-attachments/assets/d6bd6150-fe01-4a39-b4a7-e2e4e6a46796" />
<img width="932" height="142" alt="image" src="https://github.com/user-attachments/assets/eb29fb96-022d-418e-8918-54c6182b4fa0" />

# Intuition

# Code
```
#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;
#define fo(i, start, end) for (ll i = start; i <= end; i++)
#define pfo(i, end, start) for (ll i = end; i >= start; i--)
#define all(x) x.begin(), x.end()

const ll INF = 1e18;

// 8-directional moves
ll dx[8] = {1, -1, 0, 0, 1, -1, -1, 1};
ll dy[8] = {0, 0, 1, -1, 1, -1, 1, -1};

// BFS : (Traverse several nodes simultaniously)Function to compute distance from each cell to nearest delivery center (1) 
vector<vector<ll>> computeDistanceMatrix(const vector<vector<int>>& grid, ll n, ll m) {
    vector<vector<ll>> lvl(n + 1, vector<ll>(m + 1, INF));
    vector<vector<ll>> used(n + 1, vector<ll>(m + 1, 0));
    queue<pair<ll, ll>> q;

    fo(i, 1, n) {
        fo(j, 1, m) {
            if (grid[i][j] == 1) {//put all 1's in queue q whose lvl is 0 as there are starting
                lvl[i][j] = 0;
                used[i][j] = 1;
                q.push({i, j});
            }
        }
    }

    while (!q.empty()) {
        auto [x, y] = q.front(); q.pop();
        for (ll d = 0; d < 8; d++) {
            ll nx = x + dx[d];
            ll ny = y + dy[d];
            if (nx >= 1 && nx <= n && ny >= 1 && ny <= m && grid[nx][ny] == 0 && used[nx][ny] == 0) {
                used[nx][ny] = 1;
                lvl[nx][ny] = lvl[x][y] + 1;
                q.push({nx, ny});
            }
        }
    }

    return lvl;
}

int main() {
    ll n, m;
    cin >> n >> m;

    vector<vector<int>> grid(n + 1, vector<int>(m + 1));
    fo(i, 1, n) {
        fo(j, 1, m) {
            cin >> grid[i][j];
        }
    }

    vector<vector<ll>> lvl = computeDistanceMatrix(grid, n, m);

    ll u = 0;    //Find the Maximum valuse in the updated matrix (lvl)
    fo(i, 1, n) {
        fo(j, 1, m) {
            u = max(u, lvl[i][j]);
        }
    }

    ll ans = u;

    // Looping from max level (u + 1) down to 1 to check if we can reduce inconvenience by placing one more delivery center
    pfo(val, u , 1) {
    // Define the bounds of intersection square for all cells whose lvl[i][j] >= val
        ll xmin = 1, ymin = 1, xmax = n, ymax = m;
        ll count = 0; // To count how many cells have inconvenience >= val

        // Traverse the entire grid to find all such cells
        fo(i, 1, n) {
            fo(j, 1, m) {
                if (lvl[i][j] >= val) {
                    count++; // This cell has inconvenience >= val
                    // r = maximum allowed Manhattan distance from new center to this cell
                    ll r = val - 1;
    
                    // Construct square region [x1,y1] to [x2,y2] centered at (i,j) with radius r
                    ll x1 = i - r, y1 = j - r, x2 = i + r, y2 = j + r;
    
                    // Update the intersection region over all such squares
                    xmin = max(xmin, x1); // Intersection left boundary
                    ymin = max(ymin, y1); // Intersection top boundary
                    xmax = min(xmax, x2); // Intersection right boundary
                    ymax = min(ymax, y2); // Intersection bottom boundary
                }
            }
        }

        // If there are no such cells (count == 0), or intersection region is valid (non-empty):
        // Then placing a delivery center at any point in this region reduces max inconvenience to val - 1
        if (count == 0 || (xmin <= xmax && ymin <= ymax)) {
            ans = val - 1; // Update answer to smaller inconvenience
        }
    }

    cout << ans << "\n";
    return 0;
}

```

# Submission Link
https://www.jdoodle.com/ga/zOdam5IYiOV2zDUS0q5Zfg%3D%3D
