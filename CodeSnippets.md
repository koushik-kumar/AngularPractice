 1. ```
    Queue<TreeNode> queue = new LinkedList(){{ offer(root); offer(null); }};
    - queue.offer(element)
    - queue.poll()
    ```
 2. ```
    - ArrayDeque<TreeNode> nextLevel = new ArrayDeque() {{ offer(root); }};
    ArrayDeque<TreeNode> currLevel = new ArrayDeque();
    - currLevel = nextLevel.clone();
    - nextLevel.clear();
    ```
 3. 
 
 




```
Deque<String> stack = new ArrayDeque<>(); 
stack.push("first"); 
stack.push("second");


Deque<String> queue = new ArrayDeque<>(); 
queue.offer("first"); 
queue.offer("second");

```