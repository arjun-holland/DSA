# 🔄 Breadth-First Search (BFS) – Graph Traversal

Breadth-First Search is a fundamental graph traversal algorithm that explores vertices **level by level** starting from a source node. 
It uses a **queue** to keep track of nodes to visit.

---

## code
# With Adjacency List
```
#include <bits/stdc++.h>
using namespace std;

// Type alias for long long integers
typedef long long int ll;

int main() {
    int n, m;
    cin >> n >> m; // n = number of nodes, m = number of edges

    // Adjacency list for graph representation
    vector<int> G[n + 1];

    // Reading edges (undirected)
    for (int i = 0; i < m; i++) {
        int x, y;
        cin >> x >> y;
        G[x].push_back(y);
        G[y].push_back(x);
    }

    // BFS from source node (you can change the source)
    int source = 1;

    // Arrays to track visited status and level (distance from source)
    vector<int> visited(n + 1, 0);
    vector<int> level(n + 1, 0);

    // Queue for BFS
    queue<int> q;

    // Initialization
    visited[source] = 1;
    level[source] = 0;
    q.push(source);

    // Perform BFS
    while (!q.empty()) {
        int current = q.front();
        q.pop();

        // Print node and its level
        cout << "Node: " << current << ", Level: " << level[current] << "\n";

        // Visit all unvisited neighbors
        for (int neighbor : G[current]) {
            if (!visited[neighbor]) {
                visited[neighbor] = 1;
                level[neighbor] = level[current] + 1;
                q.push(neighbor);
            }
        }
    }

    return 0;
}
```
# With Adjacency Matrix
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, m;
    cin >> n >> m;  // n = number of nodes, m = number of edges

    // Adjacency matrix (initialize with 0s)
    int G[1001][1001] = {0}; // Adjust size as needed (max 1000 nodes)

    // Read edges (undirected)
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        G[u][v] = 1;
        G[v][u] = 1;
    }

    // BFS initialization
    int source = 1;  // Starting node (change as needed)
    vector<int> visited(n + 1, 0);
    vector<int> level(n + 1, 0);
    queue<int> q;

    visited[source] = 1;
    level[source] = 0;
    q.push(source);

    // Perform BFS
    while (!q.empty()) {
        int current = q.front();
        q.pop();

        // Output current node and its level
        cout << "Node: " << current << ", Level: " << level[current] << "\n";

        // Visit all neighbors
        for (int neighbor = 1; neighbor <= n; neighbor++) {
            if (G[current][neighbor] == 1 && visited[neighbor] == 0) {
                visited[neighbor] = 1;
                level[neighbor] = level[current] + 1;
                q.push(neighbor);
            }
        }
    }

    return 0;
}

```


## 📘 Code Summary

This C++ code:
- Takes input of `n` nodes and `m` edges.
- Builds an **adjacency list** to represent the graph.
- Performs BFS starting from `source = 1`.
- Outputs the order of nodes visited and their levels (distance from the source).

---


## 📦 Data Structures Used

| Structure | Purpose |
|----------|---------|
| `vector<int> G[]` | Adjacency list |
| `queue<int> q` | BFS queue |
| `used[]` | Marks visited nodes |
| `level[]` | Stores depth from source |

---

## 🔄 BFS Algorithm Steps

1. Enqueue the **source** node and mark as visited.
2. While the queue is not empty:
   - Dequeue a node.
   - For each unvisited neighbor:
     - Mark as visited.
     - Set its level to current node's level + 1.
     - Enqueue it.

---

## 📌 BFS Properties

| Feature | Value |
|--------|-------|
| Time Complexity | `O(V + E)` |
| Space Complexity | `O(V)` |
| Type | Level-order traversal |
| Good For | Shortest path in unweighted graphs, Layer-wise exploration |

---

## 🛠️ Applications of BFS

- Finding shortest path in **unweighted** graphs
- Peer-to-peer networking (like BitTorrent)
- Crawling the web (like Googlebot)
- Social networking (finding degrees of separation)
- GPS navigation (simplified models)

---

## 💡 Bonus Tip:
Use BFS when you need the **shortest path** or want to explore **closest neighbors first**. For trees, it's ideal for **level-order traversal**.

---



