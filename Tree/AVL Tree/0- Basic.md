<img width="1042" height="264" alt="image" src="https://github.com/user-attachments/assets/79847d37-8385-4916-ba8d-439886467573" />

<img width="1048" height="245" alt="image" src="https://github.com/user-attachments/assets/4d737541-4b0c-49d7-a2c0-754916458e1d" />

<img width="1035" height="379" alt="image" src="https://github.com/user-attachments/assets/5c1bc152-abd5-4975-8529-b2579b3d6ce9" />

🔁 Rotations

| Case             | Description                               | Rotation(s) Needed    |
| ---------------- | ----------------------------------------- | --------------------- |
| LL (Left-Left)   | Inserting in left subtree of left child   | Right Rotation        |
| RR (Right-Right) | Inserting in right subtree of right child | Left Rotation         |
| LR (Left-Right)  | Inserting in right subtree of left child  | Left → Right Rotation |
| RL (Right-Left)  | Inserting in left subtree of right child  | Right → Left Rotation |

<img width="634" height="577" alt="image" src="https://github.com/user-attachments/assets/04342fa5-2318-431b-95aa-ac095d1ba80e" />
<img width="863" height="289" alt="image" src="https://github.com/user-attachments/assets/99a584bb-8a9b-4c45-a3a4-df513d85c3cb" />

<img width="1061" height="484" alt="image" src="https://github.com/user-attachments/assets/ac94e14a-4b7e-4281-a30a-e974b0152f20" />
<img width="1058" height="293" alt="image" src="https://github.com/user-attachments/assets/36812c60-4673-4cf0-ad2c-f3c20ee49179" />

<img width="591" height="297" alt="image" src="https://github.com/user-attachments/assets/356ed2e8-e432-4946-814f-dac50258eac5" />

# How LR rotation works
<img width="906" height="412" alt="image" src="https://github.com/user-attachments/assets/40083e70-6e72-40c9-8e93-59bd8660b219" />
<img width="599" height="259" alt="image" src="https://github.com/user-attachments/assets/17325f2c-2ab4-4070-96e6-1046f0ea42f5" />
<img width="862" height="592" alt="image" src="https://github.com/user-attachments/assets/081a9aec-9345-49d8-9de6-0180240a1884" />
<img width="822" height="292" alt="image" src="https://github.com/user-attachments/assets/e5d660a8-3f1c-46dc-b6a9-bf9ea3960148" />
<img width="875" height="649" alt="image" src="https://github.com/user-attachments/assets/29df162c-b33a-4562-9bed-434bc19952ef" />
<img width="830" height="298" alt="image" src="https://github.com/user-attachments/assets/5491e7b2-3446-403d-8da6-36392eed88cf" />


<img width="1599" height="732" alt="image" src="https://github.com/user-attachments/assets/13c8ce10-f709-48f9-8304-b3150b5f50f2" />

# Code 
```
#include <iostream>
#include <algorithm>
using namespace std;

// Node structure (was TreeNode)
class Node {
public:
    int val;
    Node* left;
    Node* right;

    Node(int x) : val(x), left(nullptr), right(nullptr) {}
};

// AVL Tree class
class AVLTree {
public:
    // Public interface: insert with external root
    Node* insert(Node* root, int key) {
        return insertNode(root, key);
    }

    // In-order traversal
    void inorder(Node* root) {
        if (!root) return;
        inorder(root->left);
        cout << root->val << " ";
        inorder(root->right);
    }

private:
    // Height of node
    int height(Node* node) {
        if (!node) return 0;
        return 1 + max(height(node->left), height(node->right));
    }

    // Balance factor
    int getBalance(Node* node) {
        if (!node) return 0;
        return height(node->left) - height(node->right);
    }

    // Right rotation
    Node* rightRotate(Node* y) {
        Node* x = y->left;
        Node* T2 = x->right;

        x->right = y;
        y->left = T2;

        return x;
    }

    // Left rotation
    Node* leftRotate(Node* x) {
        Node* y = x->right;
        Node* T2 = y->left;

        y->left = x;
        x->right = T2;

        return y;
    }

    // Internal recursive insert
    Node* insertNode(Node* node, int key) {
        if (!node)
            return new Node(key);

        if (key < node->val)
            node->left = insertNode(node->left, key);
        else if (key > node->val)
            node->right = insertNode(node->right, key);
        else
            return node; // No duplicates

        int balance = getBalance(node);

        // Left Left
        if (balance > 1 && key < node->left->val)
            return rightRotate(node);

        // Right Right
        if (balance < -1 && key > node->right->val)
            return leftRotate(node);

        // Left Right
        if (balance > 1 && key > node->left->val) {
            node->left = leftRotate(node->left);
            return rightRotate(node);
        }

        // Right Left
        if (balance < -1 && key < node->right->val) {
            node->right = rightRotate(node->right);
            return leftRotate(node);
        }

        return node;
    }
};

int main() {
    AVLTree obj;
    Node* root = nullptr;

    root = obj.insert(root, 10);
    root = obj.insert(root, 20);
    root = obj.insert(root, 30);
    root = obj.insert(root, 40);
    root = obj.insert(root, 50);
    root = obj.insert(root, 25);

    cout << "In-order traversal: ";
    obj.inorder(root); // Output: 10 20 25 30 40 50
    cout << endl;

    return 0;
}
```
