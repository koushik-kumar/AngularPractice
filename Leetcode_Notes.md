

Finding Height of a tree:

- Recursively obtain the height of a tree. 
  - An empty tree has -1 height
    ```
        int height(TreeNode root) { 
            // An empty tree has height -1
            if (root == NULL) {
            return -1;
            }
            return 1 + max(height(root->left), height(root->right));
        }
    ```
  - An empty tree has 0 height
    