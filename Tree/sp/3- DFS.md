# 🌳 Tree DFS 

---

## 📌 Prerequisites : understand 
```
void DFS(int node,vector <int> G[],vector <int> & used,vector <int> &parent){
    
    cout << node << "\n";
    used[node] = 1; 
    
    for(auto u: G[node]){       //iterating all children "u" of "node"
        
        if(used[u]==0){
            //if this node/branch has never been visited before 
            //just go into it and search it using dfs in recursion
            parent[u] = node ; 
            DFS(u,G,used,parent);
            
        }  
    } 
}

int main() {
    int n ; 
    cin>>n ; 
    int m ; 
    cin>>m ; 
    vector <int> G[n+5] ; 
    int i = 1 ; 
    while(i<=m){
        int u,v ; 
        cin>>u>>v ; 
        G[u].push_back(v);
        G[v].push_back(u); 
        i++;
    }
    vector <int> used(n+5,0);
    vector <int> parent(n+5,0);
    DFS(1,G,used,parent); //starts from node 1  

    return 0 ; 
}
```

---


## 🏔️ Problem: Find Height of Each Node

**Definition:**  
- Height of node `x` = Longest downward path from node `x` to any leaf node.
- **📏 What Does Height of a Tree Represent?**
Height = Number of edges on the longest downward path from a root to a leaf.

### 🔁 Formula:
```text
Height[i] = 1 + max(height[c1], height[c2], ..., height[ck])
```
---
### Height of Tree (in Edges)
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

const int MAXN = 500005;
ll height[MAXN];             // Stores height of each node
int visited[MAXN];           // Marks visited nodes
int parent[MAXN];            // Stores parent of each node

// DFS function to compute height of tree nodes (bottom-up)
void DFS(int node, vector<int> G[]) {
    visited[node] = 1;

    for (int child : G[node]) {
        if (!visited[child]) {
            parent[child] = node;
            DFS(child, G);
        }
    }

    // Compute height using the formula:
    // height[node] = 1 + max(height[child1], height[child2], ...)

    ll max_child_height = 0;
    for (int child : G[node]) {           //leaf node does not go inside these
        if (child != parent[node]) {
            max_child_height = max(max_child_height, height[child]);
        }
    }
    height[node] = 1 + max_child_height;
}

//We can write the above function DFS with these
//void dfs(int node, int parent) {
//    height[node] = 0; // leaf Node itself counts as height = 0 (node-based)

//    for (int child : tree[node]) {
//        if (child == parent) continue; // Don't go back up
//        dfs(child, node); // Recursive DFS
//        height[node] = max(height[node], 1 + height[child]); // Height formula
//    }
//}

//void dfs(int node, int parent) {
//    height[node] = 1; // leaf Node itself counts as height = 1 (node-based)

//    for (int child : tree[node]) {
//        if (child == parent) continue;
//        dfs(child, node);
//        height[node] = max(height[node], 1 + height[child]);
//    }
//}


int main() {
    int n;
    cin >> n;
    vector<int> G[n + 1];
    // Reading the edges
    for (int i = 0; i < n - 1; ++i) {
        int u, v;
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u);
    }

    // Start DFS from root node (node 1)
    DFS(1, G);

    // Output heights of all nodes
    for (int i = 1; i <= n; ++i) {
        cout << height[i] << '\n';
    }
    return 0;
}
```
---
# Height of TREE (Nodes)
```
int height(TreeNode* root) {
    if (root == nullptr) return 0;

    int left_height = height(root->left);
    int right_height = height(root->right);

    return 1 + max(left_height, right_height);
}
or
int height_in_edges(TreeNode* root) {
    if (root == nullptr) return 0;               
    return 1 + max(height_in_edges(root->left), height_in_edges(root->right));
}
```
# Height of TREE (edges)
```
int height(TreeNode* root) {
    if (root == nullptr) return -1;

    int left_height = height(root->left);
    int right_height = height(root->right);

    return 1 + max(left_height, right_height);
}
or
int height_in_edges(TreeNode* root) {
    if (root == nullptr) return -1;               
    return 1 + max(height_in_edges(root->left), height_in_edges(root->right));
}

or
Simple subtract 1 from the height(nodes)
```




