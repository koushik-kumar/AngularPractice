 `Queue<TreeNode> queue = new LinkedList(){{ offer(root); offer(null); `

 `queue.offer(element)`
 `queue.poll()`


```
ArrayDeque<TreeNode> nextLevel = new ArrayDeque() {{ offer(root); }};
    ArrayDeque<TreeNode> currLevel = new ArrayDeque();
currLevel = nextLevel.clone();
nextLevel.clear();

