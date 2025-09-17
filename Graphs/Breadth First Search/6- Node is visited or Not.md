# PROBLEM
```
Given a graph G of N nodes and M edges ; 1st node is the source node ; print n answers .
answer for ith line should be yes if you can visit the i node from node 1 else no 
```

# INTUITION
<img width="907" height="206" alt="image" src="https://github.com/user-attachments/assets/2988a6f7-4be0-4d96-a0d6-f168cb086b76" />

# CODE
```
#include <bits/stdc++.h>
using namespace std;

// BFS function to check reachability from source
vector<int> BFS(int n, vector<pair<int, int>> edges, int src) {
    unordered_map<int, vector<int>> adjL;

    // Build adjacency list
    for (auto e : edges) {
        int u = e.first;
        int v = e.second;
        adjL[u].push_back(v);
        adjL[v].push_back(u);  // Undirected graph
    }

    vector<int> res(n + 1, -1);       // -1 means unreachable
    vector<bool> used(n + 1, false);  // Visited array

    queue<int> q;
    q.push(src);
    used[src] = true;
    res[src] = 0;

    while (!q.empty()) {
        int u = q.front();
        q.pop();

        for (auto v : adjL[u]) {
            if (!used[v]) {
                used[v] = true;
                q.push(v);
                res[v] = res[u] + 1;
            }
        }
    }

    return res;
}

int main() {
    int n, e;
    cin >> n >> e;
    vector<pair<int, int>> edges;

    for (int i = 0; i < e; i++) {
        int u, v;
        cin >> u >> v;
        edges.push_back({u, v});
    }

    int src = 1;  // Node 1 is the source node

    vector<int> res = BFS(n, edges, src);

    // Output "yes" if reachable, otherwise "no"
    for (int i = 1; i <= n; i++) {
        if (res[i] != -1) {
            cout << "yes" << endl;
        } else {
            cout << "no" << endl;
        }
    }

    return 0;
}

```
