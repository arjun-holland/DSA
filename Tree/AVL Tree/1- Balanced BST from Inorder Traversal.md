# Problem
<img width="901" height="610" alt="image" src="https://github.com/user-attachments/assets/343e93bf-7633-495c-beb4-ef09aadccbf4" />
<img width="857" height="363" alt="image" src="https://github.com/user-attachments/assets/bc43d8f5-31ad-4820-8e2d-065a9040c1bb" />
<img width="870" height="286" alt="image" src="https://github.com/user-attachments/assets/5c877fbd-f041-4c38-acff-11111028e677" />
<img width="883" height="591" alt="image" src="https://github.com/user-attachments/assets/e6f66f7f-84cd-448f-9273-ab6cedad9995" />
<img width="905" height="280" alt="image" src="https://github.com/user-attachments/assets/a5ec88d0-92b7-447e-969b-4a4c7e3cc4bf" />
<img width="880" height="614" alt="image" src="https://github.com/user-attachments/assets/977f52b9-c28f-4b70-a8c1-16b40f150ef4" />

# Intuition

<img width="970" height="725" alt="image" src="https://github.com/user-attachments/assets/eb08b380-fd76-4376-94c1-6f34ac3f699c" />
<img width="1032" height="175" alt="image" src="https://github.com/user-attachments/assets/6aa18547-c9aa-4205-9013-6aed0e2f8ed3" />
<img width="1035" height="597" alt="image" src="https://github.com/user-attachments/assets/5f4daf71-8fcb-4f2f-9ef0-3bb27d983a16" />
<img width="1055" height="758" alt="image" src="https://github.com/user-attachments/assets/d122ca4f-6629-4a6e-be34-91350eba15bf" />


<img width="1049" height="703" alt="image" src="https://github.com/user-attachments/assets/c18f5708-6342-43f0-8f21-5d86ddebc91e" />


<img width="1042" height="468" alt="image" src="https://github.com/user-attachments/assets/d52a0a82-6ede-4253-a4de-0e3d46f8362a" />

<img width="1044" height="775" alt="image" src="https://github.com/user-attachments/assets/8d7d7621-79b9-4d99-92c5-864cd1991b25" />
<img width="1039" height="666" alt="image" src="https://github.com/user-attachments/assets/61487834-6cb3-4654-aaf5-43bf058671ad" />


✅ In Summary

| Concept                                                      | Meaning                                                            |
| ------------------------------------------------------------ | ------------------------------------------------------------------ |
| "Left-heavy" in this problem                                 | Pick the **left-middle** of a sorted array when array size is even |
| Are we counting nodes on left and right after tree is built? | ❌ No                                                               |
| Are we choosing left-middle root **during construction**?    | ✅ Yes                                                              |
| Does this ensure more left nodes in **every subtree**?       | Not always, but generally yes over many levels                     |

<img width="994" height="81" alt="image" src="https://github.com/user-attachments/assets/4b962f78-6029-45af-9c66-088ec31ed298" />

# Code
```
#include <iostream>
#include <vector>
#include <string>
#include <queue>  // ✅ Needed for level-order traversal
using namespace std;

// TreeNode definition
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

TreeNode* buildBalancedBST(const vector<int>& nums, int low, int high) {
    if (low > high) return nullptr;

    // Choose left middle for even-length to make tree left-heavy
    int mid = low + (high - low) / 2;      
    // When the size is even [0-----3] => (0+3)/2 => 1 index taken it as we prefer left heave most then right 
    // When the size is odd [0-----2] => (0+2)/2 => 1 index taken it as by default the middle ele is gives the BST when size is odd
     
  
    TreeNode* root = new TreeNode(nums[mid]);
    root->left = buildBalancedBST(nums, low, mid - 1);
    root->right = buildBalancedBST(nums, mid + 1, high);
    return root;
}

TreeNode* sortedArrayToBST(vector<int>& nums) {
    return buildBalancedBST(nums, 0, nums.size() - 1);
}


// Level-order (BFS) tree to string
string treeNodeToString(TreeNode* root) {
    if (!root) return "";
    string res = "";
    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        auto f = q.front();
        q.pop();
        res += to_string(f->val) + " ";  // ✅ Fix: convert int to string

        if (f->left != NULL)
            q.push(f->left);
        if (f->right != NULL)
            q.push(f->right);
    }
    return res;
}

int main() {
    int n;
    cin >> n;
    vector<int> arr(n);
    for (int i = 0; i < n; ++i) {
        cin >> arr[i];
    }

    TreeNode* root = sortedArrayToBST(arr);
    string result = treeNodeToString(root);
    cout << result << endl;
    return 0;
}

```
