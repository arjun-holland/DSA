# PROBLEM
<img width="782" height="634" alt="image" src="https://github.com/user-attachments/assets/9034b0d3-3bb7-4a6a-bdf7-b3c1de0664c7" />
<img width="674" height="340" alt="image" src="https://github.com/user-attachments/assets/d1cef28e-6cdd-4c72-83c4-4fe202fc875b" />


# INTUITION
## Finding the shortest distance from a source node to all other nodes in an unweighted undirected graph.


<img width="918" height="218" alt="image" src="https://github.com/user-attachments/assets/ddc339c2-18e3-47f1-a162-bbda670ad251" />
<img width="954" height="453" alt="image" src="https://github.com/user-attachments/assets/17639ba6-d89d-4a6d-a161-280485944435" />
<img width="945" height="170" alt="image" src="https://github.com/user-attachments/assets/5016d415-f3c5-40d6-aa98-daecf6257bea" />

<img width="681" height="443" alt="image" src="https://github.com/user-attachments/assets/35ad306d-1ca5-4195-b7af-8e2d1297fc15" />

# CODE
```
#include <bits/stdc++.h>
using namespace std;

// Function to perform BFS and return shortest distances from source
vector<int> BFS(int n, vector<pair<int,int>> edges, int src){
    unordered_map<int, vector<int>> adjL;  // create the adjacency list : Graph Representation

    // Build adjacency list
    for (auto e : edges) {
        int u = e.first;
        int v = e.second;
        adjL[u].push_back(v);
        adjL[v].push_back(u);   // Undirected graph
    }

    vector<int> res(n + 1, -1);       // Distance array initialized with -1 (unreachable)
    vector<bool> used(n + 1, false);  // Visited array

    queue<int> q;
    q.push(src);
    used[src] = true;    // mark src visited 
    res[src] = 0;        // update the res for src

    // Standard BFS
    while (!q.empty()) {
        int u = q.front();
        q.pop();

        for (auto v : adjL[u]) {   // for all the neighbours of 'u'
            if (!used[v]) {        // if the neighbour is not visited
                used[v] = true;    
                q.push(v);
                res[v] = res[u] + 1;  // Distance to neighbor = current distance + 1 ,  // Each neighbor is 1 level deeper
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

    int src;
    cin >> src;

    vector<int> distances = BFS(n, edges, src);

    for (int i = 1; i <= n; i++) {
        cout << distances[i] << " ";
    }
    return 0;
}

```

# Conclusion :
```
Conclusion : Because in the BFS algorithm we travel things in level wise form so each node which we visit for the first time is always at the shortest distance from the source node = 1 ; so the level array gives us the answer of the distance of each node from node 1 automatically. 
```
