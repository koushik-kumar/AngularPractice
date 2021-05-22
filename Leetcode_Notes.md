

### Finding Height of a tree:

problem: https://leetcode.com/problems/balanced-binary-tree/

- Recursively obtain the height of a tree. 
  1. An empty tree has -1 height
        ```
        int height(TreeNode root) { 
            // An empty tree has height -1
            if (root == NULL) {
            return -1;
            }
            return 1 + max(height(root->left), height(root->right));
        }
        ```
  2. An empty tree has 0 height
        ```
        public int findHeight(TreeNode root, int height){
            if(root == null)
                return height;
            
            return Math.max(findHeight(root.left, height+1), findHeight(root.right, height+1));
            
        }
        ```

----------
### Level-order traversal

- Right side view
  - **Can be done using Queue and subList(or another queue)**
    ```
    public int findHeight(TreeNode root, int height){
        if(root == null)
            return height;
        
        return Math.max(findHeight(root.left, height+1), findHeight(root.right, height+1));
        
    }
    ```
  - **Can be done inserting null**
    ```
    public List<Integer> rightSideView(TreeNode root) {
        if (root == null) return new ArrayList<Integer>();
        
        Queue<TreeNode> queue = new LinkedList(){{ offer(root); offer(null); }};
        TreeNode prev, curr = root;
        List<Integer> rightside = new ArrayList();
        
        while (!queue.isEmpty()) {
            prev = curr;
            curr = queue.poll();

            while (curr != null) {
                // add child nodes in the queue
                if (curr.left != null) {
                    queue.offer(curr.left);    
                }
                if (curr.right != null) {
                    queue.offer(curr.right);
                }
                
                prev = curr;
                curr = queue.poll();
            }      

            // the current level is finished
            // and prev is its rightmost element
            rightside.add(prev.val);
            // add a sentinel to mark the end
            // of the next level
            if (!queue.isEmpty())
                queue.offer(null);
        }
        return rightside;
    }
    ```