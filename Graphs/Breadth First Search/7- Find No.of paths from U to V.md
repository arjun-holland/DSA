# PROBLEM
```
Given a graph of N nodes ; m edges ; undirected ; unweighted ;
for each node ‘i’ ; find the number of shortest paths from node ‘1’ to node ‘i’. 
```

# INTUITION

```
In the BFS : ways[i] represent the number of ways to reach the node i from node 1 in the shortest path length…..

if(visited[u] == 0){
    //it means that there is a guarantee that this node is being visited for the first time and it is on the shortest path hence ways[u] = ways[v] 
    q.push(u)
    Visited[u] = 1 
    Ways[u] = ways[v] 
}
Else if(lvl(v)+1 == lvl(u)){
    // either the node u is on the shortest path from node v, then u may add the number of shortest paths of ways[v] 
    Ways[u] = ways[u] + ways[v] 
}
Else {
    // or the node u is not on the shortest path from nodes
    //Do nothing don't add anything as this path from {v—>u} doesn't lis on the shortest path so counting this way is wrong okjiii
}
```

<img width="1078" height="577" alt="image" src="https://github.com/user-attachments/assets/1cf6b930-a5e7-44b4-a3d3-91b580ee1490" />


# CODE 1
```
#include <bits/stdc++.h>
using namespace std;

// Function to return number of shortest paths from node 1 to every node
pair<vector<int>, vector<int>>  BFS(int n, vector<pair<int, int>> &edges, int src) {
    unordered_map<int, vector<int>> adj;

    // Build adjacency list
    for (auto &e : edges) {
        adj[e.first].push_back(e.second);
        adj[e.second].push_back(e.first);
    }

    vector<int> dist(n + 1, -1);     // Distance from source // or we cxan say it as level of node,, 0 1 2 ....
    vector<int> count(n + 1, 0);     // Number of shortest paths

    queue<int> q;
    q.push(src);
    dist[src] = 0;   //level of source is 0
    count[src] = 1;  //we can reach the src from src in 1 way

    while (!q.empty()) {
        int u = q.front();
        q.pop();

        for (auto v : adj[u]) {
            if (dist[v] == -1) {  // First time reaching v
                dist[v] = dist[u] + 1;
                count[v] = count[u];
                q.push(v);
            } else if (dist[v] == dist[u] + 1) {  // Another shortest path to v
                count[v] += count[u];
            }
        }
    }

    return {dist, count};
}

int main() {
    int n, m;
    cin >> n >> m;

    vector<pair<int, int>> edges;

    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        edges.push_back({u, v});
    }

    int src = 1;
    auto [dist, count] = BFS(n, edges, src);

    // Output number of shortest paths from node 1 to every node
    for (int i = 1; i <= n; i++) {
        cout << count[i] << endl;
    }

    return 0;
}

```


# CODE 2
```
int main() {
    ll n, m;
    cin >> n >> m;  // n = number of nodes // m = number of edges

    vector<vector<ll>> G(n + 1); // adjacency list; nodes assumed 1..n

    // Read edges
    for (ll i = 0; i < m; i++) {
        ll u, v;
        cin >> u >> v;
        // since the graph is undirected:
        G[u].push_back(v);
        G[v].push_back(u);
    }

    // BFS initialization
    queue<ll> q;

    vector<ll> used(n + 1, 0);   // used[i] = 0 means not visited yet; 1 means visited

    vector<ll> lvl(n + 1, -1);
    // lvl[i] = shortest distance (in edges) from source (node 1) to i
    // initialize with -1 meaning "not reached yet"

    vector<ll> ways(n + 1, 0);
    // ways[i] = number of different shortest paths from source to i

    // Start from source = 1
    ll src = 1;
    used[src] = 1;
    lvl[src] = 0;
    ways[src] = 1;  // There's exactly one path from source to itself

    q.push(src);

    // BFS loop
    while (!q.empty()) {
        ll v = q.front();
        q.pop();

        // For each neighbor u of v
        for (ll u : G[v]) {
            if (used[u] == 0) {
                // First time we encounter u
                used[u] = 1;
                lvl[u] = lvl[v] + 1;
                ways[u] = ways[v];
                q.push(u);
            }
            else {
                // u has already been visited
                // Check if the current way through v gives another shortest path to u

                if (lvl[v] + 1 == lvl[u]) {
                    // The path from source → … → v → u is also of shortest-length to u
                    ways[u] += ways[v];
                }
            }
        }
    }

    // Output: number of shortest paths to each node from source 1
    for (ll i = 1; i <= n; i++) {
        cout << "Node " << i << ": " << ways[i] << " shortest paths, ";
        if (lvl[i] == -1) {
            cout << "unreachable";
        } else {
            cout << "distance = " << lvl[i];
        }
        cout << "\n";
    }
    return 0;
}
```
