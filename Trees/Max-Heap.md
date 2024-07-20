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

Let's take an example of a max-heap with the following elements: 10,9,8,7,6,5,4,3,2,110, 9, 8, 7, 6, 5, 4, 3, 2, 110,9,8,7,6,5,4,3,2,1

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

Array Representation: 10,9,8,7,6,5,4,3,2,110, 9, 8, 7, 6, 5, 4, 3, 2, 110,9,8,7,6,5,4,3,2,1

### Operations on the Max-Heap

**Insertion Example:**

Let's insert `11` into the max-heap:

1. Add `11` at the end of the array: 10,9,8,7,6,5,4,3,2,1,1110, 9, 8, 7, 6, 5, 4, 3, 2, 1, 1110,9,8,7,6,5,4,3,2,1,11
2. Bubble up: Compare `11` with its parent `4` and swap: 10,9,8,7,6,5,11,3,2,1,410, 9, 8, 7, 6, 5, 11, 3, 2, 1, 410,9,8,7,6,5,11,3,2,1,4
3. Continue to bubble up: Compare `11` with its parent `8` and swap: 10,9,11,7,6,5,8,3,2,1,410, 9, 11, 7, 6, 5, 8, 3, 2, 1, 410,9,11,7,6,5,8,3,2,1,4
4. Continue to bubble up: Compare `11` with its parent `10` and swap: 11,9,10,7,6,5,8,3,2,1,411, 9, 10, 7, 6, 5, 8, 3, 2, 1, 411,9,10,7,6,5,8,3,2,1,4

Final max-heap:
```
       11
      /  \
     9    10
    / \  / \
   7  6  5  8
  / \ / \ /
 3  2 1 4
   
```
**Deletion Example:**

Let's remove the max element `11`:

1. Remove `11` and replace it with the last element `4`: 4,9,10,7,6,5,8,3,2,14, 9, 10, 7, 6, 5, 8, 3, 2, 14,9,10,7,6,5,8,3,2,1
2. Bubble down: Compare `4` with its children `9` and `10`, and swap with `10` (the larger child): 10,9,4,7,6,5,8,3,2,110, 9, 4, 7, 6, 5, 8, 3, 2, 110,9,4,7,6,5,8,3,2,1
3. Continue to bubble down: Compare `4` with its children `5` and `8`, and swap with `8`: 10,9,8,7,6,5,4,3,2,110, 9, 8, 7, 6, 5, 4, 3, 2, 110,9,8,7,6,5,4,3,2,1

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