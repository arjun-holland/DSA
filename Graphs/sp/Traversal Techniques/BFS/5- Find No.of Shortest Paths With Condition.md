# problem
```
Given a graph of n nodes and m edges ; undirected, unweighted ; each node value is also given as 0 or 5 ; 
Source node is 1 number node . 
Your task is to find for each node ‘i’ ; find the number of the shortest path  from node-1  + having maximum maximum number of 5 possible in the path.  
```

# Intuition
```
- You are asked to find for each node i:
- The shortest path length from node 1 to node i
- Among all shortest paths, count only the ones with maximum number of 5s collected along the path

    (1)[5]   {5 is the value of 1 - node}
      |
    (2)[0]
     / \
(3)[0] (4)[5]
     \   /
     (5)[5]
For (5)-node even two shortest paths exist , the ans is only one because only one path with max valusof 5 present
```

# solution
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

int main() {
    ll n, m;
    cin >> n >> m;   // Input: n = number of nodes, m = number of edges

    // Adjacency list to represent the undirected, unweighted graph
    vector<ll> G[n + 1];

    // Read all edges
    for (ll i = 0; i < m; i++) {
        ll u, v;
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u); // Undirected edge
    }
        
    // Input: node values — each node has a value 0 or 5
    vector<int> ct(n + 1);              // ct[i] stores the value (0 or 5) of node i
    vector<int> dupct(n + 1, 0);       // dupct[i] stores the max total "5s" collected along any shortest path to node i

    for (int i = 1; i <= n; i++) {
        cin >> ct[i];
    }

    // Initialize BFS data structures
    vector<ll> level(n + 1, -1);         // level[i] = shortest distance (in edges) from source to node i
    vector<ll> ways(n + 1, 0);           // ways[i] = number of shortest paths from node 1 to node i
    vector<bool> visited(n + 1, false);  // visited[i] = whether node i has been visited in BFS

    queue<ll> q;
    ll source = 1;       // Starting BFS from node 1
    q.push(source);

    // Initialization for source node
    level[source] = 0;
    ways[source] = 1;                  // Only one way to reach the source — itself
    visited[source] = true;
    dupct[source] = ct[source];        // The "5s" collected at source is just its own value (0 or 5)

    // Start BFS
    while (!q.empty()) {
        ll current = q.front();
        q.pop();

        for (ll neighbor : G[current]) {
            if (!visited[neighbor]) {         // First time visiting this neighbor — a new shortest path found
                visited[neighbor] = true;
                level[neighbor] = level[current] + 1;
                ways[neighbor] = ways[current];                      // Inherit number of paths from current
                dupct[neighbor] = dupct[current] + ct[neighbor];     // Add neighbor's value
                q.push(neighbor);
            }
            else if (level[neighbor] == level[current] + 1) {          // If already visited through another shortest path
                ll ct2 = dupct[current] + ct[neighbor];           // Alternate path 5-count

                if (ct2 > dupct[neighbor]) {                 // If this new path gives more 5s, prefer it and update path count
                    dupct[neighbor] = ct2;
                    ways[neighbor] = ways[current];          // Replace with better path count
                }
                else if (ct2 == dupct[neighbor]) {          // If 5-count is the same, just add number of ways
                    ways[neighbor] += ways[current];
                }
                // If ct2 < dupct[neighbor], ignore — it’s a weaker path
            }
            // Else: this is a longer path — ignore it completely
        }
    }

    // Output: for each node, print number of shortest paths (with max 5s along the path)
    for (ll i = 1; i <= n; i++) {
        cout << "Node " << i << ": " << ways[i] << " shortest path(s)" << endl;
    }

    return 0;
}

```
 
