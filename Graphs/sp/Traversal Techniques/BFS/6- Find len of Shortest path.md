# Problem
```
Given a graph of n nodes and m edges ; undirected unweighted ; each node value is also given as 0 or 5 ; 
Source node is 1 number node . 
Your task is to find for each node ‘i’ ; the shortest path length from node-1  + the maximum number of 5 possible in the path 
```
# Intuition
```
- Intuition is same as 5th problem (previous), To find the shortest path length we can use the level[]
- In BST the level[] gives the shortest path length for every node i from starting node
```

# Solution
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

int main() {
    ll n, m;
    cin >> n >> m;   // n = number of nodes, m = number of edges

    // Adjacency list to represent the graph
    vector<ll> G[n + 1];

    // Read the edges (1-based indexing)
    for (ll i = 0; i < m; i++) {
        ll u, v;
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u); // Undirected graph
    }
        
    vector<int> ct(n+1),dupct(n+1,0);
    for(int i=1;i<=n;i++){  //cost of node either 0 or 5
        cin >> ct[i];
    }

    // Initialize arrays
    vector<ll> level(n + 1, -1);         // level[i] = shortest distance from node 1 to i
    vector<ll> ways(n + 1, 0);           // ways[i] = number of shortest paths from node 1 to i
    vector<bool> visited(n + 1, false);    // visited[i] = whether node i has been visited

    // BFS initialization
    queue<ll> q;
    ll source = 1;       //start with the 1 node
    q.push(source);
    dupct[source] = ct[source];

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
                dupct[neighbor] = dupct[current] + ct[neighbor]; // ✅ fixed
            }
            else if (visited[neighbor] == true && level[neighbor] == level[current] + 1) {    // Already visited, and another shortest path found
            //     ways[neighbor] += ways[current];      //we update child's  ways when path is same from its parent level
                int ct2 = dupct[current] + ct[neighbor];
                if(ct2 > dupct[neighbor]){
                    dupct[neighbor] = ct2;            // ✅ update max-5 path
                    ways[neighbor] = ways[current];
                }else if(ct2 == dupct[neighbor]){
                    ways[neighbor] += ways[current];
                }
            }else {
                // we find the path but it is longest path so do not include it to answer
            }
        }
    }

    // Output the number of shortest paths to each node
    for (ll i = 1; i <= n; i++) {
        cout << "Node " << i << ": " << ways[i] << " shortest path(s)" << endl;
    }
    // Output the shortest path length to each node
     for (ll i = 1; i <= n; i++) {
          cout << "Node " << i << ": " << level[i] << " shortest path length" << endl;
     }

    return 0;
}

```
