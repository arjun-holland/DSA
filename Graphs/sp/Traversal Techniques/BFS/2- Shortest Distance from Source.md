# Problem
Given n, i.e. total number of nodes in an undirected graph numbered from 1 to n and an integer e, i.e. total number of edges in the graph. 
Find the shortest distance of all the node from the source node s.

# Input Format:
First line of input line contains two integers n and e. Next e line will contain two integers u and v meaning 
that node u and node v are connected to each other in undirected fashion. Last line will contain an integer s denoting the source node.

# Output Format:
For each input graph print the shortest distance of each node from the source node.
Sample Input
5 4
1 2
2 3
2 4
3 5
2
Sample Output
1 0 1 1 2 

# solution
```
When to Use Dijkstra's Algorithm and BFS
- Graph is weighted and non-negative weights.
- Need the shortest path from a source to all nodes.
- BFS is only correct for unweighted graphs (all edges have same cost).
HERE all edges have same cost so use BFS

Conclusion :
Because in the BFS algorithm we travel things in level wise form so each node which we visit for the first time is always at the shortest distance from the source node = 1(root) ; so the level array gives us the answer of the distance of each node from node 1 automatically. 

BFS can always be used to find the shortest path related stuff if your graph is un-weighted. 
```
---
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, e;
    cin >> n >> e;

    // Adjacency list initialized for n nodes (1-based indexing)
    vector<int> g[n + 1];

    // Read undirected edges
    for (int i = 0; i < e; i++) {
        int u, v;
        cin >> u >> v;
        g[u].push_back(v);
        g[v].push_back(u);
    }

    int src;
    cin >> src;

    queue<int> q;
    vector<bool> vis(n + 1, false);
    vector<int> level(n + 1, -1);  // -1 means unreachable initially

    vis[src] = true;
    level[src] = 0;
    q.push(src);

    while (!q.empty()) {
        int f = q.front();
        q.pop();

        for (int ng : g[f]) {
            if (!vis[ng]) {
                vis[ng] = true;
                level[ng] = level[f] + 1;
                q.push(ng);
            }
        }
    }

    // Output level (distance from source) for each node
    for (int i = 1; i <= n; i++) {
        cout << level[i] << " ";
    }

    return 0;
}

```

