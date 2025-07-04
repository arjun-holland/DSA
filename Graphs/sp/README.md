# 📊 Graph in DSA (Data Structures & Algorithms)

Graphs are a fundamental data structure used to represent relationships or connections between entities. They are widely used in real-world scenarios like social networks, maps, recommendation engines, and more.

---

## 🔹 What is a Graph?

A **graph** is a collection of:
- **Vertices (nodes)**: The fundamental units.
- **Edges (links)**: Connections between pairs of vertices.

### Types of Graphs:
| Type | Description |
|------|-------------|
| **Directed Graph (Digraph)** | Edges have a direction (A ➡️ B). |
| **Undirected Graph** | Edges are bidirectional (A ↔️ B). |
| **Weighted Graph** | Edges have weights or costs. |
| **Unweighted Graph** | Edges are treated equally. |
| **Cyclic Graph** | Contains at least one cycle. |
| **Acyclic Graph** | No cycles present (e.g., DAG - Directed Acyclic Graph). |
| **Connected Graph** | There’s a path between every pair of vertices. |
| **Disconnected Graph** | Not all vertices are connected. |

---

## 🧠 Graph Representations

### 1. **Adjacency Matrix**
- 2D array where `matrix[i][j]` is `1` (or weight) if there’s an edge between vertex `i` and `j`.

```text
  A B C
A 0 1 0        where 1 - edge btw A and B 
B 1 0 1
C 0 1 0
✅ Quick edge lookup: O(1)
❌ Space-heavy: O(V²)
Space.-> O(N&N)
Use Matrix:-> If nodes are less and edges are way too many then use matrix; it called as dense graph. 
1<=N<=100
1<=M<=1000000
```
### 1. **Adjacency List**
- An array/list of lists or hash maps, where each vertex stores a list of connected vertices.
```
graph = {
  'A': ['B'],
  'B': ['A', 'C'],
  'C': ['B']
}
✅ Space-efficient: O(V + E)
✅ Faster traversal
Time.-> O(N).
Space.-> O(N+2*M) :-> O(N+M)
Adjacent List -> N and M are kind of equivalent to each other :->
1<=N,M<=100000

```

### 🛠️ Graph Traversal Algorithms
1. Breadth-First Search (BFS)
- Uses a queue
- Explores neighbors level-by-level
- Good for shortest path in unweighted graphs

2. Depth-First Search (DFS)
- Uses a stack (or recursion)
- Explores as far as possible before backtracking
- Good for path-finding, cycle detection

### ⚙️ Key Graph Algorithms
| Algorithm                | Use Case                            |
| ------------------------ | ----------------------------------- |
| **Dijkstra's Algorithm** | Shortest path in weighted graphs    |
| **Bellman-Ford**         | Shortest path with negative weights |
| **Floyd-Warshall**       | All-pairs shortest paths            |
| **Prim’s Algorithm**     | Minimum Spanning Tree               |
| **Kruskal’s Algorithm**  | Minimum Spanning Tree               |
| **Topological Sort**     | Scheduling tasks (DAGs)             |
| **Union-Find**           | Cycle detection, disjoint sets      |
| **A\***                  | Pathfinding (like GPS/navigation)   |
