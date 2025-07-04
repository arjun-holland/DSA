# 🧾 Problem Statement (Rewritten Clearly):
```
Given an undirected acyclic graph (i.e., a tree), where each node has at most 3 neighbors,
Find a vertex such that if you root the tree at this vertex, the resulting tree will be a valid binary tree.
```

# process :
```
Ask the interviewer :
-> How many nodes can be in the graph? -> 100000
-> Sir is this is a single connected component graph given in input -> Yes (means we hasve to decide its a tree);
-> Sir, are there multiple edges in the graph?-> No (means we hasve to decide its a tree).
come to final Observation -
- Given graph is a tree -> such that each node has maximum 3 edges. 
- We are given a tree; where each node <= 3 edges. 
- We have to decide which node should be selected as the root so that the tree becomes a binary tree. 
Each node of a binary tree has 2 children. 
The input tree will have this property - each node will have at max 2 children except the root node.
(-> root node can have 3 children which distorts the validity of being a binary tree.) 
                       1
                    /  |  \
                   2   3    4
                 / \   / \   / \
                5   6  7  8  9  0
        
Strategy - Select a node which has 2 edges or 1 edge(best option) - then it can always be converted to a binary tree. 
-> Proof :- The only problem is that the root of the input tree might have 3 children or else the problem is already solved.
 The root is assumed for input tree is the answer if it is already attached to two nodes only 
-> In case; the root has 3 child; then selecting the leaf of the tree always works. 
```
 # Solution 1:
```
#include <iostream>
#include <vector>
using namespace std;

const int MAXN = 1e5 + 5;
vector<int> G[MAXN];
int n;

int main() {
    cin >> n;

    for (int i = 0; i < n - 1; ++i) {
        int u, v;
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u);
    }

    // Step 1: Early exit if any node has degree > 3
    for (int i = 1; i <= n; ++i) {
        if (G[i].size() > 3) {
            cout << "No valid root: node " << i << " has degree > 3\n";
            return 0;
        }
    }

    // Step 2: Pick any node with degree ≤ 2 as root
    for (int i = 1; i <= n; ++i) {
        if (G[i].size() <= 2) {    //if node has 1 child or 2 child it can be root node
            cout << "Valid root (no DFS needed): " << i << endl;
            return 0;
        }
    }
    cout << "No valid root found.\n";
    return 0;
}
```
---
 # Solution 2:
```
#include <iostream>
#include <vector>
using namespace std;

const int MAXN = 1e5 + 5;
vector<int> G[MAXN];
int n;

// DFS to validate binary tree from a given root
bool isValidBinaryTree(int node, int parent) {
    int children = 0;

    for (int child : G[node]) {
        if (child == parent) continue;
        children++;
        if (children > 2) return false; // violates binary tree rule
        if (!isValidBinaryTree(child, node)) return false;
    }

    return true;
}

int main() {
    cin >> n;

    for (int i = 0; i < n - 1; ++i) {
        int u, v;
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u);
    }

    // ✅ Degree Check Once (not inside root loop)
    for (int i = 1; i <= n; ++i) {
        if (G[i].size() > 3) {
            cout << "No valid root: node " << i << " has degree > 3\n";
            return 0;
        }
    }

    // ✅ Try each node as root only if degree constraint is okay
    for (int root = 1; root <= n; ++root) {
        if (isValidBinaryTree(root, -1)) {
            cout << "Valid root found: " << root << endl;
            return 0;
        }
    }

    cout << "No valid root found to form a binary tree.\n";
    return 0;
}

```


