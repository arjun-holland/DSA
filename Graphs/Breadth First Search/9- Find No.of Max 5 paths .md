# PROBLEM
<img width="895" height="317" alt="image" src="https://github.com/user-attachments/assets/800e0ed0-857c-4397-85b5-6bd86ba9fa2a" />

# INTUITION
```
We're counting the number of shortest paths that have the maximum number of 5s among shortest paths.
```
<img width="739" height="455" alt="image" src="https://github.com/user-attachments/assets/343bcee9-36a1-49e0-b686-85229e8f6572" />
<img width="879" height="209" alt="image" src="https://github.com/user-attachments/assets/f43d8d61-8921-4d6c-b579-6bac578f1bb4" />

```
  - count[1] tracks number of shortest paths with max 5s to node 1.
  - There is only one path (length 0), so count[1] = 1.
  - Whether node 1 is 0 or 5, we still initialize it as a valid path.
```

<img width="924" height="464" alt="image" src="https://github.com/user-attachments/assets/c95a048e-69f0-4c7f-a223-19fbd68e1907" />



# CODE
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

int main() {
    ll n, m;
    cin >> n >> m;

    vector<ll> val(n + 1);
    for (ll i = 1; i <= n; i++) cin >> val[i];

    vector<ll> G[n + 1];
    for (ll i = 1; i <= m; i++) {
        ll u, v;
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u);
    }

    vector<ll> dist(n + 1, -1);         // Shortest distance to each node
    vector<ll> maxFives(n + 1, 0);      // Max number of 5s on any shortest path
    vector<ll> count(n + 1, 0);         // Number of shortest paths with maxFives

    queue<ll> q;
    q.push(1);

    dist[1] = 0;
    maxFives[1] = (val[1] == 5 ? 1 : 0);
    count[1] = 1;   //There is exactly one way to reach node 1 from node 1 (the trivial path) which has max 5 path.

    while (!q.empty()) {
        ll v = q.front(); q.pop();

        for (auto u : G[v]) {
            ll fivesThroughV = maxFives[v] + (val[u] == 5 ? 1 : 0);

            if (dist[u] == -1) {  // First time visiting node u
                dist[u] = dist[v] + 1;
                maxFives[u] = fivesThroughV;
                count[u] = count[v];
                q.push(u);
            }
            else if (dist[u] == dist[v] + 1) {  // Another shortest path found
                if (fivesThroughV > maxFives[u]) {
                    maxFives[u] = fivesThroughV;
                    count[u] = count[v]; // Start fresh with this better path
                } 
                else if (fivesThroughV == maxFives[u]) {
                    count[u] += count[v]; // Add more ways with same max 5s
                }
            }
        }
    }

    // Output result
    for (ll i = 1; i <= n; i++) {
        if (dist[i] == -1) {
            cout << -1 << " " << 0 << "\n";
        } else {
            cout << dist[i] << " " << count[i] << "\n";
        }
    }
    return 0;
}

```
