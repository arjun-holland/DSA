# 🌲 Depth-First Search (DFS) in Graphs

DFS (Depth-First Search) is a classic graph traversal algorithm used to explore nodes and edges of a graph systematically. It's widely used in problems like **cycle detection**, **connected components**, and **pathfinding**.

---

## 📌 What is DFS?

- **DFS** starts from a given node and explores **as far as possible** along each branch before **backtracking**. 
- It uses **recursion** or an explicit **stack**.

---
## 🧠 DFS Intuition

DFS explores a graph **as deep as possible**, then **backtracks**. It works well for:
- Finding paths
- Checking connectivity
- Cycle detection
- Graph traversals

---


## 🔁 DFS Use Cases

- Detecting cycles in graphs
- Checking graph connectivity
- Finding connected components
- Topological sorting (DAGs)
- Maze solving
- Tree traversals (Inorder, Preorder, Postorder)
- Path existence queries

---

## 🛠️ DFS Implementation (C++ - Adjacency List)

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> graph;
vector<bool> visited;

void dfs(int node) {
    visited[node] = true;
    cout << "Visited node: " << node << endl;

    for (int neighbor : graph[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor);
        }
    }
}

int main() {
    int n, m;
    cin >> n >> m; // number of nodes and edges
    graph.resize(n + 1);
    visited.resize(n + 1, false);

    // Input edges
    for (int i = 0; i < m; ++i) {
        int u, v;
        cin >> u >> v;
        graph[u].push_back(v);
        graph[v].push_back(u); // Undirected graph
    }

    // Run DFS from node 1
    dfs(1);

    return 0;
}
```
## 🛠️ DFS in C++ using Adjacency Matrix

```cpp
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100; // Adjust based on expected node count
int adj[MAX][MAX];   // Adjacency matrix
bool visited[MAX];   // Visited nodes

void dfs(int node, int n) {
    visited[node] = true;
    cout << "Visited node: " << node << endl;

    for (int i = 1; i <= n; ++i) {
        if (adj[node][i] == 1 && !visited[i]) {
            dfs(i, n);
        }
    }
}

int main() {
    int n, m;
    cin >> n >> m; // Number of nodes and edges

    // Initialize adjacency matrix
    memset(adj, 0, sizeof(adj));
    memset(visited, false, sizeof(visited));

    // Read edges
    for (int i = 0; i < m; ++i) {
        int u, v;
        cin >> u >> v;
        adj[u][v] = 1;
        adj[v][u] = 1; // Undirected
    }

    // Run DFS from node 1
    dfs(1, n);

    return 0;
}
🧪 Sampl
