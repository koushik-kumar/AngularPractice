

**Finding Height of a tree:**

- Recursively obtain the height of a tree. 
  1. first
  2. second
  3. third
  - 
  - An empty tree has 0 height
    ```
    public int findHeight(TreeNode root, int height){
        if(root == null)
            return height;
        
        return Math.max(findHeight(root.left, height+1), findHeight(root.right, height+1));
        
    }
    ```