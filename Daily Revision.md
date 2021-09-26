## ArrayList
public class ArrayList{
    transient Object[] elementData;

    public ArrayList(int initialCapacity) { if (initialCapacity > 0) {
        this.elementData = new Object[initialCapacity]; } else if (initialCapacity == 0) {
            this.elementData = EMPTY_ELEMENTDATA; } else {
            throw new IllegalArgumentException("Illegal Capacity: "+ initialCapacity);
        }
    }


     myList = new ArrayList();
    public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }
}


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