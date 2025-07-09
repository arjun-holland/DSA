# problem
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.
According to the definition of LCA on Wikipedia:
“The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants
(where we allow a node to be a descendant of itself).”

# Image
![image](https://github.com/user-attachments/assets/796e0413-e84a-4500-9b84-d7ba5a842df2)
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```
![image](https://github.com/user-attachments/assets/a3880182-e9d7-4d90-8446-bd1ae19e686d)

---
# code
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        // Base case
        if (!root) return nullptr;
        if (root == p || root == q) return root;

        // Recur for left and right subtree
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);

        // If both calls return non-null, current node is LCA
        if (left && right) return root;

        // Otherwise, return non-null side
        return left ? left : right;
    }
};

```
