
## Finding Height of a tree:

- Recursively obtain the height of a tree. 

  - What is height for a null node ==> can be treated as 0 or -1.
    - If putting -1 doesn't affect the solution like case where we return just boolean 
    - Else we treat height for null node as 0
  - `return 1 + max(height(root->left), height(root->right));`
    
    (or)

    `return Math.max(findHeight(root.left, height+1), findHeight(root.right, height+1));`

<br></br>

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

problem: https://leetcode.com/problems/balanced-binary-tree/

----------
## Level-order traversal

We can do this in 4 ways

  1. BFS - Using 2 queues (1 queue and a List)   --> O(N), O(D)
  2. BFS - Using 1 queue and sentinel       --> O(N), O(D)
  3. BFS - Using Queue and level number     --> O(N), O(D)
  4. DFS - Recursion using level number     --> O(N), O(H), worst case H can become N for skewed tree


<br></br>
- ### BFS: Two Queues
  - **Can be done using Queue and subList(or another queue)** 
  
    ```
    ArrayDeque<TreeNode> nextLevel = new ArrayDeque() {{ offer(root); }};
    ArrayDeque<TreeNode> currLevel = new ArrayDeque();        
    List<Integer> rightside = new ArrayList();
    
    TreeNode node = null;
    while (!nextLevel.isEmpty()) {
        // prepare for the next level
        currLevel = nextLevel.clone();
        nextLevel.clear();

        while (! currLevel.isEmpty()) {
            node = currLevel.poll();

            // add child nodes of the current level
            // in the queue for the next level
            if (node.left != null) 
                nextLevel.offer(node.left);    
            if (node.right != null) 
                nextLevel.offer(node.right);
        }
        
        // The current level is finished.
        // Its last element is the rightmost one.
        if (currLevel.isEmpty()) 
            rightside.add(node.val);    
    }
    ```


    ```
    {
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        
        while(!q.isEmpty()){
            int size = q.size();
            List<Integer> subList = new ArrayList<>();
            for(int i = 0; i < size; i++){
                TreeNode x = q.poll();
                subList.add(x.val);
                if(x.left != null)
                    q.add(x.left);
                if(x.right != null)
                    q.add(x.right);
            }
            result.add(subList.get(subList.size() - 1));
        }
    }
    ```
- ### BFS: One Queue + Sentinel
    **Can be done inserting null**
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

- ###  BFS: One Queue + Level Size Measurements
    ```
    int size = -1;
    while(!queue.isEmpty()){
        size = queue.size();            
        for(int i = 0; i < size; i++){
            TreeNode front = queue.poll();
            if(i == size -1)
                output.add(front.val);
            
            if(front.left != null)
                queue.add(front.left);
            if(front.right != null)
                queue.add(front.right);
        }
    }
    ```
- ### Recursive DFS
    ```
    class Solution {
        List<Integer> rightside = new ArrayList();
        
        public void helper(TreeNode node, int level) {
            if (level == rightside.size()) 
                rightside.add(node.val);
            
            if (node.right != null) 
                helper(node.right, level + 1);  
            if (node.left != null) 
                helper(node.left, level + 1);
        }    
        
        public List<Integer> rightSideView(TreeNode root) {
            if (root == null) return rightside;
            
            helper(root, 0);
            return rightside;
        }
    }

    ```

----------
### Rotten Oranges
  - BFS Approach: 
      - Need to count number of fresh oranges to check if all freshones are rotten or not
      - Need to subtract 1 minute in the result
        - ```
          if(fresh > 0)
              return -1;
          return count - 1;
          ```
        - Or can also be done as check in the while loop itself
        ```
        while(!q.isEmpty() && fresh > 0){
            int size = q.size();
            for( int i = 0; i < size; i++){
                int[] rott = q.poll();
                for(int[] dir : dirs){
                    int x = rott[0] + dir[0];
                    int y = rott[1] + dir[1];
                    if(x >= 0 && x < grid.length && y >= 0 && y < grid[0].length && grid[x][y] == 1){
                        grid[x][y] = 2;
                        q.add(new int[]{x, y});
                        fresh -= 1;
                    }
                }
            }
            count++;
        }
        
        if(fresh > 0)
            return -1;
        return count;
              ^^^^^^
        ```