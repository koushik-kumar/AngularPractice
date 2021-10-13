## ArrayList

Points to note
1. ArrayList in Java is a Resizable-array implementation of the List interface.
2. Internally ArrayList class uses an array of Object class to store its elements.
3. When initializing an ArrayList you can provide initial capacity then the array would be of the size
provided as initial capacity.
4. If initial capacity is not specified then default capacity is used to create an array. Default capacity is 10.
5. When an element is added to an ArrayList it first verifies whether it can accommodate the new element or it needs to grow, in case capacity has to be increased then the new capacity is calculated which is 50% more than the old capacity and the array is increased by that much capacity.
6. When elements are removed from an ArrayList space created by the removal of an element has to be filled in the underlying array. That is done by Shifting any subsequent elements to the left.

```
public class ArrayList{
    transient Object[] elementData;
    private static final Object[] EMPTY_ELEMENTDATA = {};
    private static final int DEFAULT_CAPACITY = 10;

    /**
    * Shared empty array instance used for default sized empty instances. We
    * distinguish this from EMPTY_ELEMENTDATA to know how much to inflate when
    * first element is added.
    */
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
    

    

    public ArrayList(int initialCapacity) { 
        if (initialCapacity > 0) {
            this.elementData = new Object[initialCapacity]; 
        } else if (initialCapacity == 0) {
            this.elementData = EMPTY_ELEMENTDATA; 
        } else {
            throw new IllegalArgumentException("Illegal Capacity: "+ initialCapacity);
        }
    }



    myList = new ArrayList();
    public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }
    



    public boolean add(E e) {
        ensureCapacityInternal(size + 1); // Increments modCount!! elementData[size++] = e;
        return true;
    }

    private void ensureCapacityInternal(int minCapacity) {
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            minCapacity = Math.max(DEFAULT_CAPACITY, minCapacity); 
        }
        ensureExplicitCapacity(minCapacity);
    }

    private void ensureExplicitCapacity(int minCapacity) { 
        modCount++;
        // overflow-conscious code
        if (minCapacity - elementData.length > 0)
            grow(minCapacity);
        }
    }

    private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        int newCapacity = oldCapacity + (oldCapacity >> 1); if (newCapacity - minCapacity < 0)
        newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win: 
        elementData = Arrays.copyOf(elementData, newCapacity);
    }

    // What happens when an element is removed from ArrayList
    System.arraycopy(elementData, index+1, elementData, index, numMoved);
}
```
---

## Reverse a linked list
```
public class ReverseLL{    
    // Time Complexity: O(n)
    // Space Complexity: O(1)
    public ListNode reverseList(ListNode head) {
        
// Iterative Solution
        ListNode curr = head ;
        ListNode prev = null;
        ListNode temp;
        while(curr != null){
            temp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = temp;
        }
        return prev;
        
// Recursive Solution
//         if(head == null || head.next == null)
//             return head;
        
//         ListNode newHeadNode = reverseList(head.next);
//         head.next.next = head;
//         head.next = null;
        
//         return newHeadNode;
    }
}
```
---


## Stack using Array

```
class CustomStack {

    int[] stack;
    int index;
    
    public CustomStack(int maxSize) {
        stack = new int[maxSize];
        index = 0;
    }
    
    public void push(int x) {
        if(index < stack.length){
            stack[index] = x;
            index++;
        }
    }
    
    public int pop() {
        if(index > 0){
            int temp = stack[index - 1];
            stack[index - 1] = 0;
            index--;
            return temp;
        }        
        
        return -1;
    }
    
    public void increment(int k, int val) {
        k = Math.min(k, index);
        for(int i = 0; i < k; i++){
            stack[i] += val;
        }
    }
}
```

## Implement Queue using array

- Enqueue
- Dequeue
- Print
- Front

```

public class QueueUsingArray{
    public int[] queue;
    public int front, reat, capacity;

    Queue(int c){
        capacity = c;
        front = 0; rear = 0;
        queue = new int[c];
    }

    public void enqueue(int e){
        if(rear == capacity){
            System.out.println("Queue is full");
            return;
        }
        queue[rear] = e;
        rear++;
    }

    public void dequeue(){
        if(front == rear){
            System.out.println("Queue is empty");
            return;
        }
        
        for(int i = 0; i < rear; i++){
            queue[i] = queue[i+1];
        }
        rear--;
    }

    public int front(){
        if(front == rear){
            System.out.println("Queue is empty");
            return;
        }

        return queu[front];
    }

    public void print(){
        if(front == rear){
            System.out.println("Queue is empty");
            return;
        }

        for(int e : queue){
            System.out.print(e + " ");
        }
    }


}

```
---

## Implement HashMap
The general implementation of HashMap uses bucket which is basically a chain of linked lists and each node containing <key, value> pair.

So if we have duplicate nodes, that doesn’t matter - it will still replicate each key with it’s value in linked list node.

When we insert the pair (10, 20) and then (10, 30), there is technically no collision involved. We are just replacing the old value with the new value for a given key 10, since in both cases, 10 is equal to 10 and also the hash code for 10 is always 10.

Collision happens when multiple keys hash to the same bucket. In that case, we need to make sure that we can distinguish between those keys. Chaining collision resolution is one of those techniques which is used for this.

Time complexity: O(1) average and O(n) worst case - for all get(),put() and remove() methods.

Space complexity: O(n) - where n is the number of entries in HashMap 

CODE:
```
class MyHashMap
{
 ListNode[] nodes = new ListNode[10000];

 public int get(int key)
 {
   int index = getIndex(key);
   ListNode prev = findElement(index, key);
   return prev.next == null ? -1 : prev.next.val;
 }


 public void put(int key, int value)
 {
   int index = getIndex(key);
   ListNode prev = findElement(index, key);
   if (prev.next == null)
     prev.next = new ListNode(key, value);
   else 
     prev.next.val = value;
 }


 public void remove(int key)
 {
   int index = getIndex(key);
   ListNode prev = findElement(index, key);
   if(prev.next != null)
     prev.next = prev.next.next;
 }


 private int getIndex(int key)
 {  
   return Integer.hashCode(key) % nodes.length;
 }


 private ListNode findElement(int index, int key)
 {
   if(nodes[index] == null)
     return nodes[index] = new ListNode(-1, -1);
   ListNode prev = nodes[index];

   while(prev.next != null && prev.next.key != key)
   {
     prev = prev.next;
   }

   return prev;
 }


 private static class ListNode
 {
   int key, val;
   ListNode next;
​
   ListNode(int key, int val)
   {
     this.key = key;
     this.val = val;
   }
 }
}
```

---

## Implement HashSet
We are going to use array to implement hashset and do the operations on an array to implement hashset

Time complexity: every operation is being done in O(1) time complexity
```
class MyHashSet {

   int buckets = 1000;
   int bucketItems = 1000;
   boolean [][] storage = new boolean[buckets][];

   public int bucket(int value){ 
       return value%buckets;
   }

   public int bucketItem(int value){ 
       return value/buckets;
   }

   /** Initialize your data structure here. */

   public MyHashSet() {
   }


   public void add(int value ) {
       int bucket = bucket(value);      
       int bucketItem = bucketItem(value);
       if(storage[bucket] == null){
           storage[bucket] = new boolean[bucketItems]; 
       }
       storage[bucket][bucketItem] = true;
   }


   public void remove(int value) {
        int bucket = bucket(value);
        int bucketItem = bucketItem(value);
       if(storage[bucket] != null){
           storage[bucket][bucketItem] = false;
       }
   }


   /** Returns true if this set contains the specified element */

   public boolean contains(int value) {
       int bucket = bucket(value);
       int bucketItem = bucketItem(value);
       return storage[bucket] != null && storage[bucket][bucketItem];
   }
}
```
---
## Graph
```// Java program to print BFS traversal from a given source vertex.
// BFS(int s) traverses vertices reachable from s.
import java.io.*;
import java.util.*;

// This class represents a directed graph using adjacency list
// representation
class Graph
{
	private int V; // No. of vertices
	private LinkedList<Integer> adj[]; //Adjacency Lists

	// Constructor
	Graph(int v)
	{
		V = v;
		adj = new LinkedList[v];
		for (int i=0; i<v; ++i)
			adj[i] = new LinkedList();
	}


	// Function to add an edge into the graph
	void addEdge(int v,int w)
	{
		adj[v].add(w);
	}


	// prints BFS traversal from a given source s
	void BFS(int s)
	{
		// Mark all the vertices as not visited(By default
		// set as false)
		boolean visited[] = new boolean[V];

		// Create a queue for BFS
		LinkedList<Integer> queue = new LinkedList<Integer>();

		// Mark the current node as visited and enqueue it
		visited[s]=true;
		queue.add(s);

		while (queue.size() != 0)
		{
			// Dequeue a vertex from queue and print it
			s = queue.poll();
			System.out.print(s+" ");

			// Get all adjacent vertices of the dequeued vertex s
			// If a adjacent has not been visited, then mark it
			// visited and enqueue it
			Iterator<Integer> i = adj[s].listIterator();
			while (i.hasNext())
			{
				int n = i.next();
				if (!visited[n])
				{
					visited[n] = true;
					queue.add(n);
				}
			}
		}
	}


	// Driver method to
	public static void main(String args[])
	{
		Graph g = new Graph(4);

		g.addEdge(0, 1);
		g.addEdge(0, 2);
		g.addEdge(1, 2);
		g.addEdge(2, 0);
		g.addEdge(2, 3);
		g.addEdge(3, 3);

		System.out.println("Following is Breadth First Traversal "+
						"(starting from vertex 2)");

		g.BFS(2);
	}
}
```

### 
```
// Java program to print DFS
//mtraversal from a given given
// graph
import java.io.*;
import java.util.*;

// This class represents a
// directed graph using adjacency
// list representation
class Graph {
	private int V; // No. of vertices

	// Array of lists for
	// Adjacency List Representation
	private LinkedList<Integer> adj[];

	// Constructor
	@SuppressWarnings("unchecked") Graph(int v)
	{
		V = v;
		adj = new LinkedList[v];
		for (int i = 0; i < v; ++i)
			adj[i] = new LinkedList();
	}

	// Function to add an edge into the graph
	void addEdge(int v, int w)
	{
		adj[v].add(w); // Add w to v's list.
	}

	// A function used by DFS
	void DFSUtil(int v, boolean visited[])
	{
		// Mark the current node as visited and print it
		visited[v] = true;
		System.out.print(v + " ");

		// Recur for all the vertices adjacent to this
		// vertex
		Iterator<Integer> i = adj[v].listIterator();
		while (i.hasNext())
		{
			int n = i.next();
			if (!visited[n])
				DFSUtil(n, visited);
		}
	}

	// The function to do DFS traversal.
	// It uses recursive
	// DFSUtil()
	void DFS(int v)
	{
		// Mark all the vertices as
		// not visited(set as
		// false by default in java)
		boolean visited[] = new boolean[V];

		// Call the recursive helper
		// function to print DFS
		// traversal
		DFSUtil(v, visited);
	}

	// Driver Code
	public static void main(String args[])
	{
		Graph g = new Graph(4);

		g.addEdge(0, 1);
		g.addEdge(0, 2);
		g.addEdge(1, 2);
		g.addEdge(2, 0);
		g.addEdge(2, 3);
		g.addEdge(3, 3);

		System.out.println(
			"Following is Depth First Traversal "
			+ "(starting from vertex 2)");

		g.DFS(2);
	}
}
```

---

## Binary Search 

```
Iterative Binary Search
The main() method of IterativeBinarySearch class starts off with defining a Array of size 6, named A.
Key is the number to be searched in the list of elements.
Inside the while loop, "mid" is obtained by calculating (low+high)/2.
If number at position mid equal to key or target element then the control returns index of mid element by printing that the number has been found along with the index at which it was found.
*Else, if key or target is less than number at position mid then the portion of the Array from the mid upwards is removed from contention by making "high" equal to mid-1.
Else, it implies that key element is greater than number at position mid(as it is not less than and also not equal, hence, it has to be greater). Hence, the portion of the list from mid and downwards is removed from contention by making "low" equal to mid+1.
The while loop continues to iterate in this way till either the element is returned (indicating key has been found in the Array) or low becomes greater than high,in which case -1 is returned indicating that key could not be found and the same is printed as output.


class IterativeBinarySearch
{
	// find out if a key x exists in the sorted array A
	// or not using binary search algorithm
	public static int binarySearch(int[] A, int x)
	{
	  // search space is A[low..high]
       int low = 0, high = A.length - 1;

		// till search space consists of at-least one element
		while (low <= high)
		{
			// we find the mid value in the search space and
			// compares it with key value

			int mid = (low + high) / 2;

			// overflow can happen. Use:
			// int mid = low + (high - low) / 2;
			// int mid = right - (high - low) / 2;

			// key value is found
			if (x == A[mid]) {
				return mid;
			}

			// discard all elements in the right search space
			// including the mid element
			else if (x < A[mid]) {
				high = mid - 1;
			}

			// discard all elements in the left search space
			// including the mid element
			else {
				low = mid + 1;
			}
		}

		// x doesn't exist in the array
		return -1;
	}

	public static void main(String[] args)
	{
		int[] A = { 2, 5, 6, 8, 9, 10 };
		int key = 5;

		int index = binarySearch(A, key);

		if (index != -1) {
			System.out.println("Element found at index " + index);
		} else {
			System.out.println("Element not found in the array");
		}
	}
}

```

```
class RecursiveBinarySearch
{
	// Find out if a key x exists in the sorted array
	// A[low..high] or not using binary search algorithm
	public static int binarySearch(int[] A, int low, int high, int x)
	{
		// Base condition (search space is exhausted)
		if (low > high) {
			return -1;
		}

		// we find the mid value in the search space and
		// compares it with key value

		int mid = (low + high) / 2;

		// overflow can happen. Use beleft
		// int mid = low + (high - low) / 2;

		// Base condition (key value is found)
		if (x == A[mid]) {
			return mid;
		}

		// discard all elements in the right search space
		// including the mid element
		else if (x < A[mid]) {
			return binarySearch(A, low,  mid - 1, x);
		}

		// discard all elements in the left search space
		// including the mid element
		else {
			return binarySearch(A, mid + 1,  high, x);
		}
	}

	public static void main(String[] args)
	{
		int[] A = { 2, 5, 6, 8, 9, 10 };
		int key = 5;

		int low = 0;
		int high= A.length - 1;
		int index = binarySearch(A, low, high, key);



		if (index != -1) {
			System.out.println("Element found at index " + index);
		} else {
			System.out.println("Element not found in the array");
		}
	}
}

```
---

## Tree traversal - pre, in, post

```
package com.javadevjournal.datastructure.tree.bst;


public class BinarySearchTree {

    private Node root;

    /**
     * In order BST traversal allows to traverse tree in the sorted order.
     * This traversal follow left->current-right pattern.
     * <li>left sub-tree will be viisted first.</li>
     * <li> Current node will be viisted after left traversal</li>
     * <li>Right subtree will be visited in the end.</li>
     */
    public void inOrderTraversal() {
        inOrderTraversal(root);
    }

    public void postOrderTraversal() {
        postOrderTraversal(root);
    }

    public void preOrderTraversal() {
        preOrderTraversal(root);
    }


    /*
     Internal private method to do in order traversal.We will pass the
     root node to start with and will visit the tree recursively using the following
     path left-current-right
    */
    private void inOrderTraversal(Node node) {

        //We will continue until null or empty node is found
        if (node != null) {

            //visit the left subtree until the leaf node
            inOrderTraversal(node.left);

            //Print the node
            System.out.println(node.data);

            //process the same step for the right node
            inOrderTraversal(node.right);
        }
    }


    /*
     Internal private method to do pre order traversal.We will pass the
     root node to start with and will visit the tree recursively using the following
     path current-left-right
    */
    private void preOrderTraversal(Node node) {

        //We will continue until null or empty node is found
        if (node != null) {

            //Print the node
            System.out.println(node.data);

            //visit the left subtree until the leaf node
            inOrderTraversal(node.left);

            //process the same step for the right node
            inOrderTraversal(node.right);
        }
    }


    /*
     Internal private method to do post-order traversal.We will pass the
     root node to start with and will visit the tree recursively using the following
     path right-left-current
    */
    private void postOrderTraversal(Node node) {

        //We will continue until null or empty node is found
        if (node != null) {

            //visit the left subtree until the leaf node
            inOrderTraversal(node.left);

            //process the same step for the right node
            inOrderTraversal(node.right);

            //Print the node
            System.out.println(node.data);
        }
    }

    /**
     * Internal node class representing the node of the BST. This contains the following information
     * <li>data- actual data stored in the Tree</li>
     * <li>left - Left child of the node</li>
     * <li>right - right child of the node</li>
     */
    class Node {

        int data;
        Node left;
        Node right;

        Node(int data) {
            this.data = data;
            //this just for reading.they will be null by default
            this.left = null;
            this.right = null;
        }
    }
}

// Main program to test it
package com.javadevjournal.datastructure.tree;

import com.javadevjournal.datastructure.tree.bst.BinarySearchTree;

public class BinarySearchTreeTest {

    public static void main(String[] args) {
        BinarySearchTree bst = new BinarySearchTree();

        /* We are building a BST as below
             52
           /    \
          15     56
         /  \    /  \
        9    16 54   61
       / \
      3   10 */

        bst.insert(52);
        bst.insert(15);
        bst.insert(56);
        bst.insert(9);
        bst.insert(16);
        bst.insert(54);
        bst.insert(3);
        bst.insert(10);
        bst.insert(61);

        //inorder traversal
        bst.inOrderTraversal(); //output [3,9,10,15,16,52,54,56,61]

        //pre-order
        bst.preOrderTraversal(); //output [52,15,9,3,10,16,56,54,61]

        //post-order
        bst.postOrderTraversal(); //output [3,10,9,16,15,54,61,56,52]
    }
}

```
---

## Trie

```
package com.baeldung.trie;

import java.util.HashMap;
import java.util.Map;

class TrieNode {
    private final Map<Character, TrieNode> children = new HashMap<>();
    private boolean endOfWord;

    Map<Character, TrieNode> getChildren() {
        return children;
    }

    boolean isEndOfWord() {
        return endOfWord;
    }

    void setEndOfWord(boolean endOfWord) {
        this.endOfWord = endOfWord;
    }
}
```
---
class TrieNode {

    // R links to node children
    private TrieNode[] links;

    private final int R = 26;

    private boolean isEnd;

    public TrieNode() {
        links = new TrieNode[R];
    }

    public boolean containsKey(char ch) {
        return links[ch -'a'] != null;
    }
    public TrieNode get(char ch) {
        return links[ch -'a'];
    }
    public void put(char ch, TrieNode node) {
        links[ch -'a'] = node;
    }
    public void setEnd() {
        isEnd = true;
    }
    public boolean isEnd() {
        return isEnd;
    }
}

---
```
package com.baeldung.trie;

class Trie {
    private TrieNode root;

    Trie() {
        root = new TrieNode();
    }

    void insert(String word) {
        TrieNode current = root;

        for (char l : word.toCharArray()) {
            current = current.getChildren().computeIfAbsent(l, c -> new TrieNode());
        }
        current.setEndOfWord(true);
    }

    boolean delete(String word) {
        return delete(root, word, 0);
    }

    boolean containsNode(String word) {
        TrieNode current = root;

        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            TrieNode node = current.getChildren().get(ch);
            if (node == null) {
                return false;
            }
            current = node;
        }
        return current.isEndOfWord();
    }

    boolean isEmpty() {
        return root == null;
    }

    private boolean delete(TrieNode current, String word, int index) {
        if (index == word.length()) {
            if (!current.isEndOfWord()) {
                return false;
            }
            current.setEndOfWord(false);
            return current.getChildren().isEmpty();
        }
        char ch = word.charAt(index);
        TrieNode node = current.getChildren().get(ch);
        if (node == null) {
            return false;
        }
        boolean shouldDeleteCurrentNode = delete(node, word, index + 1) && !node.isEndOfWord();

        if (shouldDeleteCurrentNode) {
            current.getChildren().remove(ch);
            return current.getChildren().isEmpty();
        }
        return false;
    }
}
```
---

## Merge sort
```
MergeSort(arr[], l,  r)
If r > l
     1. Find the middle point to divide the array into two halves:  
             middle m = l+ (r-l)/2
     2. Call mergeSort for first half:   
             Call mergeSort(arr, l, m)
     3. Call mergeSort for second half:
             Call mergeSort(arr, m+1, r)
     4. Merge the two halves sorted in step 2 and 3:
             Call merge(arr, l, m, r)
```

```
/* Java program for Merge Sort */
class MergeSort
{
	// Merges two subarrays of arr[].
	// First subarray is arr[l..m]
	// Second subarray is arr[m+1..r]
	void merge(int arr[], int l, int m, int r)
	{
		// Find sizes of two subarrays to be merged
		int n1 = m - l + 1;
		int n2 = r - m;

		/* Create temp arrays */
		int L[] = new int[n1];
		int R[] = new int[n2];

		/*Copy data to temp arrays*/
		for (int i = 0; i < n1; ++i)
			L[i] = arr[l + i];
		for (int j = 0; j < n2; ++j)
			R[j] = arr[m + 1 + j];

		/* Merge the temp arrays */

		// Initial indexes of first and second subarrays
		int i = 0, j = 0;

		// Initial index of merged subarray array
		int k = l;
		while (i < n1 && j < n2) {
			if (L[i] <= R[j]) {
				arr[k] = L[i];
				i++;
			}
			else {
				arr[k] = R[j];
				j++;
			}
			k++;
		}

		/* Copy remaining elements of L[] if any */
		while (i < n1) {
			arr[k] = L[i];
			i++;
			k++;
		}

		/* Copy remaining elements of R[] if any */
		while (j < n2) {
			arr[k] = R[j];
			j++;
			k++;
		}
	}

	// Main function that sorts arr[l..r] using
	// merge()
	void sort(int arr[], int l, int r)
	{
		if (l < r) {
			// Find the middle point
			int m =l+ (r-l)/2;

			// Sort first and second halves
			sort(arr, l, m);
			sort(arr, m + 1, r);

			// Merge the sorted halves
			merge(arr, l, m, r);
		}
	}

	/* A utility function to print array of size n */
	static void printArray(int arr[])
	{
		int n = arr.length;
		for (int i = 0; i < n; ++i)
			System.out.print(arr[i] + " ");
		System.out.println();
	}

	// Driver code
	public static void main(String args[])
	{
		int arr[] = { 12, 11, 13, 5, 6, 7 };

		System.out.println("Given Array");
		printArray(arr);

		MergeSort ob = new MergeSort();
		ob.sort(arr, 0, arr.length - 1);

		System.out.println("\nSorted array");
		printArray(arr);
	}
}
/* This code is contributed by Rajat Mishra */
```

#### Output
```
Given array is 
12 11 13 5 6 7 
Sorted array is 
5 6 7 11 12 13
```
Time Complexity:   
Sorting arrays on different machines. Merge Sort is a recursive algorithm and time complexity can be expressed as following recurrence relation.  
> T(n) = 2T(n/2) + θ(n)

The above recurrence can be solved either using the Recurrence Tree method or the Master method. It falls in case II of Master Method and the solution of the recurrence is θ(nLogn). Time complexity of Merge Sort is  θ(nLogn) in all 3 cases (worst, average and best) as merge sort always divides the array into two halves and takes linear time to merge two halves.

Auxiliary Space: O(n)  
Algorithmic Paradigm: Divide and Conquer  
Sorting In Place: No in a typical implementation

Stable: Yes  

---
## Quick Sort

different ways.   

* Always pick first element as pivot.  
* Always pick last element as pivot (implemented below)  
* Pick a random element as pivot.  
* Pick median as pivot.  

### Pseudo Code for recursive QuickSort function : 
```
/* low  --> Starting index,  high  --> Ending index */
quickSort(arr[], low, high)
{
    if (low < high)
    {
        /* pi is partitioning index, arr[pi] is now
           at right place */
        pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);  // Before pi
        quickSort(arr, pi + 1, high); // After pi
    }
}
```
### Pseudo code for partition()  
```
/* This function takes last element as pivot, places
   the pivot element at its correct position in sorted
    array, and places all smaller (smaller than pivot)
   to left of pivot and all greater elements to right
   of pivot */
partition (arr[], low, high)
{
    // pivot (Element to be placed at right position)
    pivot = arr[high];  
 
    i = (low - 1)  // Index of smaller element and indicates the 
                   // right position of pivot found so far

    for (j = low; j <= high- 1; j++)
    {
        // If current element is smaller than the pivot
        if (arr[j] < pivot)
        {
            i++;    // increment index of smaller element
            swap arr[i] and arr[j]
        }
    }
    swap arr[i + 1] and arr[high])
    return (i + 1)
}
```



```
// Java implementation of QuickSort
import java.io.*;

class GFG{
	
// A utility function to swap two elements
static void swap(int[] arr, int i, int j)
{
	int temp = arr[i];
	arr[i] = arr[j];
	arr[j] = temp;
}

/* This function takes last element as pivot, places
the pivot element at its correct position in sorted
array, and places all smaller (smaller than pivot)
to left of pivot and all greater elements to right
of pivot */
static int partition(int[] arr, int low, int high)
{
	
	// pivot
	int pivot = arr[high];
	
	// Index of smaller element and
	// indicates the right position
	// of pivot found so far
	int i = (low - 1);

	for(int j = low; j <= high - 1; j++)
	{
		
		// If current element is smaller
		// than the pivot
		if (arr[j] < pivot)
		{
			
			// Increment index of
			// smaller element
			i++;
			swap(arr, i, j);
		}
	}
	swap(arr, i + 1, high);
	return (i + 1);
}

/* The main function that implements QuickSort
		arr[] --> Array to be sorted,
		low --> Starting index,
		high --> Ending index
*/
static void quickSort(int[] arr, int low, int high)
{
	if (low < high)
	{
		
		// pi is partitioning index, arr[p]
		// is now at right place
		int pi = partition(arr, low, high);

		// Separately sort elements before
		// partition and after partition
		quickSort(arr, low, pi - 1);
		quickSort(arr, pi + 1, high);
	}
}

// Function to print an array
static void printArray(int[] arr, int size)
{
	for(int i = 0; i < size; i++)
		System.out.print(arr[i] + " ");
		
	System.out.println();
}

// Driver Code
public static void main(String[] args)
{
	int[] arr = { 10, 7, 8, 9, 1, 5 };
	int n = arr.length;
	
	quickSort(arr, 0, n - 1);
	System.out.println("Sorted array: ");
	printArray(arr, n);
}
}

// This code is contributed by Ayush Choudhary

```

Why MergeSort is preferred over QuickSort for Linked Lists?   
In case of linked lists the case is different mainly due to difference in memory allocation of arrays and linked lists. Unlike arrays, linked list nodes may not be adjacent in memory. Unlike array, in linked list, we can insert items in the middle in O(1) extra space and O(1) time. Therefore merge operation of merge sort can be implemented without extra space for linked lists.  
In arrays, we can do random access as elements are continuous in memory. Let us say we have an integer (4-byte) array A and let the address of A[0] be x then to access A[i], we can directly access the memory at (x + i*4). Unlike arrays, we can not do random access in linked list. Quick Sort requires a lot of this kind of access. In linked list to access i’th index, we have to travel each and every node from the head to i’th node as we don’t have continuous block of memory. Therefore, the overhead increases for quick sort. Merge sort accesses data sequentially and the need of random access is low. 