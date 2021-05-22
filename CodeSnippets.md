 1. first
 2. second
 3. third
 
 ```
 Queue<TreeNode> queue = new LinkedList(){{ offer(root); offer(null); }};
 - queue.offer(element)
 - queue.poll()
```

```
- ArrayDeque<TreeNode> nextLevel = new ArrayDeque() {{ offer(root); }};
  ArrayDeque<TreeNode> currLevel = new ArrayDeque();
- currLevel = nextLevel.clone();
- nextLevel.clear();
```


```
Deque<String> stack = new ArrayDeque<>(); 
stack.push("first"); 
stack.push("second");


Deque<String> queue = new ArrayDeque<>(); 
queue.offer("first"); 
queue.offer("second");

```