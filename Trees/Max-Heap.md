### Explanation of Max-Heap Data Structure

A **Max-Heap** is a complete binary tree where each node is greater than or equal to its children. This property makes it suitable for use cases where you need quick access to the largest element, such as in a priority queue.

#### Properties of Max-Heap:

1. **Complete Binary Tree**: All levels are fully filled except possibly for the last level, which is filled from left to right.
2. **Heap Property**: Every parent node has a value greater than or equal to its children. Formally, for every node iii:
    - A[i] ≥ A[2i+1]   (if the left child exists)
    - A[i] ≥ A[2i+2]  (if the right child exists)

#### Operations on Max-Heap:

1. **Insertion**:
    
    - Add the new element at the end of the tree (as the last node).
    - Restore the heap property by comparing the added element with its parent and swapping if necessary (bubble up).
2. **Deletion (Removing the max element)**:
    
    - Remove the root element (the max element).
    - Move the last element to the root.
    - Restore the heap property by comparing the root with its children and swapping with the larger child if necessary (bubble down).
3. **Peek**:
    
    - Return the root element without removing it (constant time).

### Example of Max-Heap Tree

Let's take an example of a max-heap with the following elements: 10,9,8,7,6,5,4,3,2,1

#### Tree Structure

```
       10
      /  \
     9    8
    / \  / \
   7  6  5  4
  / \ /
 3  2 1

```

### Sketch of Max-Heap

Here is the visual representation of the max-heap:

```
       10
      /  \
     9    8
    / \  / \
   7  6  5  4
  / \ /
 3  2 1

```

### Detailed Explanation of Tree Nodes

- **Root Node**: 10
    - **Left Child**: 9
        - **Left Child of 9**: 7
            - **Left Child of 7**: 3
            - **Right Child of 7**: 2
        - **Right Child of 9**: 6
    - **Right Child**: 8
        - **Left Child of 8**: 5
            - **Left Child of 5**: 1
        - **Right Child of 8**: 4

### Max-Heap in Array Representation

A max-heap can be efficiently represented using an array. The parent-child relationship can be derived from the indices of the array:

- Parent of node at index iii is at index ⌊i−12⌋\left\lfloor \frac{i-1}{2} \right\rfloor⌊2i−1​⌋
- Left child of node at index iii is at index 2i+12i + 12i+1
- Right child of node at index iii is at index 2i+22i + 22i+2

For the given example:

Array Representation: 10,9,8,7,6,5,4,3,2,1

### Operations on the Max-Heap

**Insertion Example:**

Let's insert `11` into the max-heap:

1. Add `11` at the end of the array: 10,9,8,7,6,5,4,3,2,1,11
2. Bubble up: Compare `11` with its parent `6` and swap: 10,9,8,7,11,5,4,3,2,1,6
3. Continue to bubble up: Compare `11` with its parent `9` and swap: 10,11,8,7,9,5,4,3,2,1,6
4. Continue to bubble up: Compare `11` with its parent `10` and swap: 11,10,8,7,9,5,4,3,2,1,6

Final max-heap:
```
       11
      /  \
     10    8
    / \   / \
   7   9  5  4
  / \ / \ 
 3  2 1 6
   
```
**Deletion Example:**

Let's remove the max element `11`:

1. Remove `11` and replace it with the last element `6`: 6,10,8,7,9,5,4,3,2,1
2. Bubble down: Compare `6` with its children `10` and `8`, and swap with `10` (the larger child): 10,6,8,7,9,5,4,3,2,1
3. Continue to bubble down: Compare `6` with its children `7` and `9`, and swap with `9`: 10,9,8,7,6,5,4,3,2,1

Final max-heap:

```
       10
      /  \
     9    8
    / \  / \
   7  6  5  4
  / \ /
 3  2 1

```

### Conclusion

A max-heap is a complete binary tree where every parent node is greater than or equal to its children, making it ideal for efficiently finding and removing the largest element. The priority queue implementation in Java can be adapted to function as a max-heap using a custom comparator. The insertion and deletion operations maintain the heap property, ensuring the structure remains a valid max-heap.


**Java Example**

**MaxHeap.java**
```java
import java.util.Arrays;

public class MaxHeap {
    private int[] heap;
    private int size;
    private int capacity;

    public MaxHeap(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        heap = new int[capacity];
    }

    private int parent(int index) {
        return (index - 1) / 2;
    }

    private int leftChild(int index) {
        return 2 * index + 1;
    }

    private int rightChild(int index) {
        return 2 * index + 2;
    }

    private void swap(int index1, int index2) {
        int temp = heap[index1];
        heap[index1] = heap[index2];
        heap[index2] = temp;
    }

    private void ensureExtraCapacity() {
        if (size == capacity) {
            heap = Arrays.copyOf(heap, capacity * 2);
            capacity *= 2;
        }
    }

    public void insert(int key) {
        ensureExtraCapacity();
        heap[size] = key;
        size++;
        heapifyUp(size - 1);
    }

    private void heapifyUp(int index) {
        while (index != 0 && heap[parent(index)] < heap[index]) {
            swap(index, parent(index));
            index = parent(index);
        }
    }

    public int extractMax() {
        if (size == 0) throw new IllegalStateException("Heap is empty");
        int max = heap[0];
        heap[0] = heap[size - 1];
        size--;
        heapifyDown(0);
        return max;
    }

    private void heapifyDown(int index) {
        int largest = index;
        int left = leftChild(index);
        int right = rightChild(index);

        if (left < size && heap[left] > heap[largest]) {
            largest = left;
        }

        if (right < size && heap[right] > heap[largest]) {
            largest = right;
        }

        if (largest != index) {
            swap(index, largest);
            heapifyDown(largest);
        }
    }

    public int getMax() {
        if (size == 0) throw new IllegalStateException("Heap is empty");
        return heap[0];
    }

    public int getSize() {
        return size;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public static void main(String[] args) {
        MaxHeap maxHeap = new MaxHeap(10);
        maxHeap.insert(3);
        maxHeap.insert(10);
        maxHeap.insert(5);
        maxHeap.insert(6);
        maxHeap.insert(2);

        System.out.println("Max value: " + maxHeap.getMax()); // Should print 10
        System.out.println("Extracted max value: " + maxHeap.extractMax()); // Should print 10
        System.out.println("Max value after extraction: " + maxHeap.getMax()); // Should print 6
    }
}

```
### Explanation

1. **Class Definition**:
    
    - The `MaxHeap` class defines the structure and methods for the max heap.
2. **Constructor**:
    
    - Initializes the heap with a given capacity.
3. **Helper Methods**:
    
    - `parent(int index)`: Returns the parent index of the given index.
    - `leftChild(int index)`: Returns the left child index of the given index.
    - `rightChild(int index)`: Returns the right child index of the given index.
    - `swap(int index1, int index2)`: Swaps the elements at the given indices.
    - `ensureExtraCapacity()`: Doubles the array size if the heap is full.
4. **Main Operations**:
    
    - `insert(int key)`: Inserts a new element into the heap.
    - `heapifyUp(int index)`: Ensures the heap property is maintained after insertion.
    - `extractMax()`: Removes and returns the maximum element from the heap.
    - `heapifyDown(int index)`: Ensures the heap property is maintained after extraction.
    - `getMax()`: Returns the maximum element without removing it.
    - `getSize()`: Returns the current size of the heap.
    - `isEmpty()`: Checks if the heap is empty.
5. **Main Method**:
    
    - Demonstrates the usage of the `MaxHeap` class by performing some basic operations.