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

```

public class QueueUsingArray{
    public int[] queue;

Queue(int c){
    queue = new int
}
}

```