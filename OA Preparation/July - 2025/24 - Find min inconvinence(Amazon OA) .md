# Problem
<img width="1373" height="552" alt="image" src="https://github.com/user-attachments/assets/c955586a-6fdf-49a8-a5e4-4c7e08eb8ced" />
<img width="1029" height="624" alt="image" src="https://github.com/user-attachments/assets/d6bd6150-fe01-4a39-b4a7-e2e4e6a46796" />
<img width="932" height="142" alt="image" src="https://github.com/user-attachments/assets/eb29fb96-022d-418e-8918-54c6182b4fa0" />

# Intuition
<img width="867" height="375" alt="image" src="https://github.com/user-attachments/assets/b9addb53-0f7d-43df-b6d5-afa0f8bb2a21" />
<img width="886" height="524" alt="image" src="https://github.com/user-attachments/assets/84cd2857-1e59-4143-a998-33b3225a31bb" />
<img width="878" height="385" alt="image" src="https://github.com/user-attachments/assets/91cf06bf-277b-49bc-a932-c189d13bf4a7" />
<img width="893" height="443" alt="image" src="https://github.com/user-attachments/assets/ad6de943-ed60-49b9-9316-1f57517d804c" />
<img width="904" height="549" alt="image" src="https://github.com/user-attachments/assets/a5f2805a-2d3e-4467-9de6-8557d834ab2c" />
<img width="877" height="300" alt="image" src="https://github.com/user-attachments/assets/3528056d-dda7-4cdb-a4ad-5567321adfb4" />

---
<img width="861" height="331" alt="image" src="https://github.com/user-attachments/assets/56eae093-f206-4e94-a108-b035e406a4b6" />
<img width="853" height="244" alt="image" src="https://github.com/user-attachments/assets/3024f275-fbf5-45d6-af2b-06d7f0c1c6d1" />
<img width="877" height="649" alt="image" src="https://github.com/user-attachments/assets/417f2b11-1f2e-4026-ad04-cbbbea83210f" />
<img width="882" height="589" alt="image" src="https://github.com/user-attachments/assets/c695cddb-d10c-4037-b0b1-aeafc0985d0c" />
<img width="843" height="691" alt="image" src="https://github.com/user-attachments/assets/5e0fd323-8123-43c3-b35a-15a430fbcdf5" />
<img width="885" height="454" alt="image" src="https://github.com/user-attachments/assets/efa86cee-4928-4bdb-80de-752b8d63b757" />
<img width="863" height="220" alt="image" src="https://github.com/user-attachments/assets/bba9d871-84ed-4061-abc3-d0c2dcbaa6c5" />
<img width="878" height="273" alt="image" src="https://github.com/user-attachments/assets/7ec3e0c9-96ee-4ebd-9ecf-e375071ccd53" />

<img width="822" height="464" alt="image" src="https://github.com/user-attachments/assets/ca58964e-8686-4bc1-aa5a-ae09d8cbfe14" />


<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/ae59990f-18c9-4d74-a3fd-e5bf3b9b20ff" />

---
 
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
        ll count = 0;        // To count how many cells have inconvenience >= val

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
