# PROBLEM
```
Given a graph of n nodes and m edges ; undirected unweighted ; each node value is also given as 0 or 5 ; The source node is the “1” number node . 
Your task is to find for each node ‘i’ ; the shortest path length from node - 1  + the maximum number of 5 possible in the shortest path 
```

# INTUITION
<img width="746" height="326" alt="image" src="https://github.com/user-attachments/assets/3905e2c1-53d8-4915-8ae6-a41d798c54dc" />
<img width="933" height="228" alt="image" src="https://github.com/user-attachments/assets/2a1ce01b-9ae7-43a9-9813-5a7cb3e13039" />

# CODE
```
int main() {
    ll n; cin >> n;  // number of nodes
    ll m; cin >> m;  // number of edges

    vector<ll> val(n+5);  // stores the value (0 or 5) for each node

    // Read values for each node
    for (ll i = 1; i <= n; i++) {
        cin >> val[i];
    }

    vector<ll> G[n+5];  // Adjacency list for the graph

    // Read m edges and build the undirected graph
    for (ll i = 1; i <= m; i++) {
        ll u, v; 
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u);
    }

    // BFS data structures
    vector<ll> dist(n+5, 0);     // dist[i] = shortest distance from node 1 to node i
    vector<ll> fives(n+5, 0);    // fives[i] = max number of 5s on shortest path to node i
    vector<ll> used(n+5, 0);     // used[i] = whether node i has been visited in BFS

    queue<ll> q;
    q.push(1);       // Start BFS from node 1
    used[1] = 1;
    dist[1] = 0;
    
    // Initialize number of 5s on the path to node 1
    fives[1] = (val[1] == 5) ? 1 : 0;

    // Standard BFS loop
    while (!q.empty()) {
        ll v = q.front();  q.pop();

        // Visit all neighbors of node v
        for (auto u : G[v]) {
            if (used[u] == 0) {  // First time visiting node u
                used[u] = 1;
                dist[u] = dist[v] + 1;  // Update distance from source
                fives[u] = fives[v] + (val[u] == 5 ? 1 : 0);   // Update number of 5s along this path
                q.push(u);
            } else {
                if (dist[u] == dist[v] + 1) {    // Check if this path gives more 5s :  // If already visited and this path gives the same shortest distance
                    ll temp = fives[v] + (val[u] == 5 ? 1 : 0);   // Update number of 5s along this path
                    if (temp > fives[u]) {
                        fives[u] = temp;  // Update max 5s count
                    }
                }
            }
        }
    }

    // Output results
    for (ll i = 1; i <= n; i++) {
        if (used[i] == 0) { // Node is unreachable
            cout << -1 << " " << -1 << "\n";
        } else { // Print shortest distance and max 5s
            cout << dist[i] << " " << fives[i] << "\n";
        }
    }
    return 0;
}

```
