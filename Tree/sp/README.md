# 🌳 Tree Data Structure in DSA

---

## 📘 What is a Tree?

A **tree** is a hierarchical data structure made of **nodes**, starting from a special node called the **root**.

- Each node holds a **value/data**.
- It may have **children** (sub-nodes).
- Trees do not contain **cycles** (unlike graphs).
---

```
Example:
         A        <-- root
        /  \
       B    C     <-- children of A
      /  \
     D    E        <-- children of B

```  
----
## 🌿 Tree Terminology

| Term                         | Description                                                                                                              |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| **Node**                     | Basic unit that holds data and may have links to other nodes.                                                            |
| **Root**                     | The topmost node in the tree (only one root in a tree).                                                                  |
| **Leaf / External Node**     | A node with **no children**.                                                                                             |
| **Internal Node**            | A node that **has at least one child** (non-leaf).                                                                       |
| **Parent**                   | A node that has children.                                                                                                |
| **Child**                    | A node directly connected to another node moving away from the root.                                                     |
| **Sibling**                  | Nodes that share the same parent.                                                                                        |
| **Ancestor**                 | Any node above a given node on the path to the root.                                                                     |
| **Descendant**               | Any node below a given node on the path to a leaf.                                                                       |
| **Subtree**                  | A tree formed by a node and all its descendants.                                                                         |
| **Edge**                     | A connection between one node and another.                                                                               |
| **Path**                     | A sequence of nodes and edges connecting a node with a descendant.                                                       |
| **Depth**                    | The number of edges from the root to that node. Root has depth 0.                                                        |
| **Height of Node**           | Number of edges on the longest path from the node to a leaf.                                                             |
| **Height of Tree**           | Height of the root node (max depth of any node).                                                                         |
| **Level**                    | Level of a node = depth + 1 (root at level 1).                                                                           |
| **Degree of Node**           | Number of children a node has.                                                                                           |
| **Degree of Tree**           | Maximum degree of any node in the tree.                                                                                  |
| **Binary Tree**              | A tree where every node has **at most 2 children** (left and right).                                                     |
| **Full Binary Tree**         | Every node has 0 or 2 children (no node has only one child).                                                             |
| **Complete Binary Tree**     | All levels are completely filled except possibly the last, and the last level has all nodes **as far left as possible**. |
| **Perfect Binary Tree**      | All internal nodes have 2 children and all leaves are at the same level.                                                 |
| **Balanced Binary Tree**     | A binary tree where the height difference between left and right subtree for any node is at most 1.                      |
| **Skewed Tree**              | A tree where each node has only one child (Left-skewed or Right-skewed).                                                 |
| **Binary Search Tree (BST)** | Left child < root < right child.                                                                                         |
| **AVL Tree**                 | A self-balancing BST where balance factor of each node is -1, 0, or 1.                                                   |
| **Heap**                     | A complete binary tree with heap property (Min-Heap or Max-Heap).                                                        |
| **Threaded Binary Tree**     | A binary tree where null pointers are replaced by references to inorder predecessor/successor to make traversal faster.  |
| **Trie** (Prefix Tree)       | A special tree used to store strings efficiently, commonly used for autocomplete and dictionary lookup.                  |


---

## 🌲 Types of Trees

### ✅ General Tree
- A node can have any number of children.

### ✅ Binary Tree
- Each node has at most **two children**: `left` and `right`.

### ✅ Binary Search Tree (BST)
- Left subtree has values **less than** the node.
- Right subtree has values **greater than** the node.

### ✅ Balanced Tree (e.g., AVL, Red-Black)
- Keeps height minimal to ensure efficient operations.

### ✅ Heap
- A complete binary tree that satisfies heap property.
  - **Min-Heap**: parent < children
  - **Max-Heap**: parent > children

---

## 🔄 Tree Traversals

Traversal = Visiting all nodes in some order.

### 🌐 Depth-First Search (DFS)
1. **Inorder (LNR)**: Left → Node → Right  
2. **Preorder (NLR)**: Node → Left → Right  
3. **Postorder (LRN)**: Left → Right → Node  

### 📶 Breadth-First Search (BFS)
- Level-order traversal: Visit nodes level by level (uses queue).

---

## 💻 Sample Code (C++ - Binary Tree Traversal)

```
// Binary Tree Node
struct Node {
    int data;
    Node* left;
    Node* right;
    
    Node(int val) {
        data = val;
        left = right = nullptr;
    }
};

// Inorder Traversal (LNR)
void inorder(Node* root) {
    if (root == nullptr) return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

// Preorder Traversal (NLR)
void preorder(Node* root) {
    if (root == nullptr) return;
    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

// Postorder Traversal (LRN)
void postorder(Node* root) {
    if (root == nullptr) return;
    postorder(root->left);
    postorder(root->right);
    cout << root->data << " ";
}

// Level-order Traversal (BFS)
void levelOrder(Node* root) {
    if (root == nullptr) return;
    queue<Node*> q;
    q.push(root);
    
    while (!q.empty()) {
        Node* curr = q.front(); q.pop();
        cout << curr->data << " ";
        
        if (curr->left) q.push(curr->left);
        if (curr->right) q.push(curr->right);
    }
}

// Driver Code
int main() {
    /*
           1
         /   \
        2     3
       / \   / 
      4   5 6  
    */
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);

    cout << "Inorder: ";
    inorder(root);
    cout << "\nPreorder: ";
    preorder(root);
    cout << "\nPostorder: ";
    postorder(root);
    cout << "\nLevel Order: ";
    levelOrder(root);

    return 0;
}



```
---
# Diff bwn TREE and GRAPH
## 🌳 Tree (Connected Acyclic Graph)
**Definition**: A tree is a connected graph with no cycles.

**Properties**:
- If there are 'n' nodes in a tree, it will always have 'n - 1' edges.
- All nodes are connected.
- No loops or cycles.
- There is only one unique path between any two nodes.

# ✅ Example (Tree with 5 nodes):

Nodes = 5  
Edges = 4 (5 - 1)

      1
     / \
    2   3
       / \
      4   5
---

## 🔁 Graph (General Case)
**Definition**: A graph can be directed/undirected, may or may not be connected, and can have cycles.
- Nodes = n, Edges can be ≤ n(n-1)/2 for undirected graphs.
For a graph with n nodes and n edges, you may have:
- A cycle, or
- A disconnected component, depending on the structure.

# ✅ Example: A graph with 5 nodes and 5 edges
```
This can have a cycle:
    1
   / \
  2 - 3
      |
      4
      |
      5
```
🔍 Summary
| Structure | Nodes (`n`) | Edges     | Cycle       | Connected  |
| --------- | ----------- | --------- | ----------- | ---------- |
| Tree      | `n`         | `n - 1`   | ❌ No cycles | ✅ Yes      |
| Graph     | `n`         | ≥ `n - 1` | ✅ Possible  | ❌ Optional |
