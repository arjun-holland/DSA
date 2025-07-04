# Problem Statement:
Given an unweighted, undirected graph with N nodes and M edges, compute the number of distinct shortest paths from node 1 to every other node. 

# 💡 Intuition
```
The goal is to find the number of shortest paths from a source node (node 1) to every other node in an unweighted, undirected graph.
Because the graph is unweighted, every edge has the same "cost" or "distance"—so we can use Breadth-First Search (BFS) to:
- Explore the graph level by level, starting from the source.
- Record the level (or distance) of each node from the source.
- Track how many distinct ways we can reach a node with the minimum level.

             root
               |   \
               |     \
             parent   parent-brother
               |     /     |
               |   /       |
            child -------own-child
From the above diagram we are getting that there are three paths are present from `root` to `child` but the shortest paths are only two.
```
# 🔁 How It Works:
Initially, we set the number of ways to reach the source node as 1.
- As we explore the graph using BFS:
- The `first time` we reach a node, we record its `level` and set its `number of paths` to the `number of paths from the parent`.
- If we encounter that node `again through another path of the same level`, we simply add to its path count.
- This ensures that we only count shortest paths, and only once per valid path.

# solution
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

int main() {
    ll n, m;
    cin >> n >> m; // n = number of nodes, m = number of edges

    // Adjacency list to represent the graph
    vector<ll> G[n + 1];

    // Read the edges (1-based indexing)
    for (ll i = 0; i < m; i++) {
        ll u, v;
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u); // Undirected graph
    }

    // Initialize arrays
    vector<ll> level(n + 1, -1);         // level[i] = shortest distance from node 1 to i
    vector<ll> ways(n + 1, 0);           // ways[i] = number of shortest paths from node 1 to i
    vector<bool> visited(n + 1, false);    // visited[i] = whether node i has been visited

    // BFS initialization
    queue<ll> q;
    ll source = 1;       //start with the 1 node
    q.push(source);

    level[source] = 0;        
    ways[source] = 1;         //1 way to reach from the 1 to itself
    visited[source] = true;

    // Perform BFS
    while (!q.empty()) {
        ll current = q.front();
        q.pop();

        for (ll neighbor : G[current]) {
            if (visited[neighbor] == false) {     // First-time visit: enqueue and set level
                visited[neighbor] = true;
                level[neighbor] = level[current] + 1;
                ways[neighbor] = ways[current];     // First path found
                q.push(neighbor);
            }
            else if (visited[neighbor] == true && level[neighbor] == level[current] + 1) {    // Already visited, and another shortest path found
                ways[neighbor] += ways[current];
            }else {
                // we find the path but it is longest path so do not include it to answer
            }
        }
    }

    // Output the number of shortest paths to each node
    for (ll i = 1; i <= n; i++) {
        cout << "Node " << i << ": " << ways[i] << " shortest path(s)" << endl;
    }
    return 0;
}

```
