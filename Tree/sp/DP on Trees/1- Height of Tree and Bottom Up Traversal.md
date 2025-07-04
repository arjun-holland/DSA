```
-> In DFS ; you come outside the first for loop only when you reach a leaf node for the first time;
hence printing the node after the first loop guarantees that all the leaves will be printed first
```
---
# problem
```
P1 : -  Given a Tree of N Nodes, rooted at node 1 find the sum of each subtree “i” in the given tree. 
Sum[i] = value of node “i” + sum(sum[c1] + sum[c2] + sum[c3] +...sum[cg]) = sum of subtree rooted at node ‘i’ 

—-> c1,c2,..............cg:-> children of node “i” 

```
---

```
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

const int MAXN = 100005;

vector<int> G[MAXN];      // Adjacency list for the tree
int height[MAXN];         // Stores height of each node
int used[MAXN];           // Marks visited nodes
int parent[MAXN];         // Stores parent of each node

void DFS(int node) {
    used[node] = 1;
    for (int u : G[node]) {
        if (!used[u]) {
            parent[u] = node;
            DFS(u);           // Recursive DFS on child
        }
    }

    // ----> Bottom-up traversal (Anwesha's Law)
    cout << "Visited (Bottom-up): Node " << node << endl;

    int h = 0;
    for (int child : G[node]) {
        if (child == parent[node]) continue; // Ignore parent

        h = max(h, height[child]);  // Track max height from children
    }
    height[node] = 1 + h;  // Tanvir/Tiju Law formula
}

int main() {
    int n;
    cin >> n;
    // Read tree edges (n-1 edges for a tree with n nodes)
    for (int i = 1; i <= n - 1; i++) {
        int u, v;
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u); // Undirected graph asyclic with single conneceted : tree
    }

    // Initialize visited and parent arrays
    fill(used, used + n + 1, 0);
    fill(parent, parent + n + 1, 0);

    // Start DFS from root (Node 1)
    DFS(1);

    // Output the height of each node
    cout << "\nHeights of Nodes:\n";
    for (int i = 1; i <= n; i++) {
        cout << "Height[" << i << "] = " << height[i] << endl;
    }
    return 0;
}
```
