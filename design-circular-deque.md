Solution: https://leetcode.com/problems/design-circular-deque/solutions/5843845/beats-100-easy-optimal-solution/

Description: https://leetcode.com/problems/design-circular-deque/description/

![image.png](https://assets.leetcode.com/users/images/328611e8-c22a-4102-8b59-b0483fcf903e_1727530729.047404.png)


# Intuition
The problem can be solved by using an array-based circular buffer. The idea is to maintain two pointers (`front` and `rear`) to keep track of the two ends of the deque, while using modular arithmetic to handle the wrap-around nature of the circular structure. This helps efficiently add or remove elements from either end.

The `front` and `rear` pointers will be adjusted after each insert or delete operation using modular arithmetic. We need to be careful to correctly update these pointers to handle the circular nature without going out of bounds.

# Approach
The `MyCircularDeque` class is implemented using an array of fixed size (`capacity`) to store the elements, with additional properties such as `front`, `rear`, and `count`:
1. **Initialization**: 
   - The deque is initialized with a maximum size (`capacity`).
   - Set `front` to `0` and `rear` to `capacity - 1` initially.
   - `count` keeps track of the current number of elements in the deque.

2. **Insert Operations**:
   - **`insertFront(value)`**: Add an element at the front by decrementing `front` using modular arithmetic. If the deque is full, return `false`.
   - **`insertLast(value)`**: Add an element at the rear by incrementing `rear` using modular arithmetic. If the deque is full, return `false`.

3. **Delete Operations**:
   - **`deleteFront()`**: Remove an element from the front by incrementing `front` using modular arithmetic. If the deque is empty, return `false`.
   - **`deleteLast()`**: Remove an element from the rear by decrementing `rear` using modular arithmetic. If the deque is empty, return `false`.

4. **Access Operations**:
   - **`getFront()`**: Return the element at the `front` pointer, or `-1` if the deque is empty.
   - **`getRear()`**: Return the element at the `rear` pointer, or `-1` if the deque is empty.

5. **Utility Operations**:
   - **`isEmpty()`**: Returns `true` if `count` is `0`.
   - **`isFull()`**: Returns `true` if `count` is equal to `capacity`.

This approach ensures that each operation takes constant time, and the use of modular arithmetic helps effectively handle the wrap-around nature of the deque.

# Complexity
- **Time Complexity**: 
  - Each operation (`insertFront`, `insertLast`, `deleteFront`, `deleteLast`, `getFront`, `getRear`, `isEmpty`, `isFull`) takes constant time: $$O(1)$$. This is because all operations are performed in a straightforward manner using direct indexing or arithmetic, without the need for iteration.

- **Space Complexity**: 
  - The space complexity is $$O(k)$$, where `k` is the maximum size of the deque. This is because we use an array of size `k` to store the elements of the deque.


# Code
```csharp []
public class MyCircularDeque
{
    private int[] deque;
    private int front;
    private int rear;
    private int capacity;
    private int count;

    public MyCircularDeque(int k)
    {
        capacity = k;
        deque = new int[k];
        front = 0;
        rear = k - 1;
        count = 0;
    }

    public bool InsertFront(int value)
    {
        if (IsFull()) return false;
        front = (front - 1 + capacity) % capacity;
        deque[front] = value;
        count++;
        return true;
    }

    public bool InsertLast(int value)
    {
        if (IsFull()) return false;
        rear = (rear + 1) % capacity;
        deque[rear] = value;
        count++;
        return true;
    }

    public bool DeleteFront()
    {
        if (IsEmpty()) return false;
        front = (front + 1) % capacity;
        count--;
        return true;
    }

    public bool DeleteLast()
    {
        if (IsEmpty()) return false;
        rear = (rear - 1 + capacity) % capacity;
        count--;
        return true;
    }

    public int GetFront()
    {
        if (IsEmpty()) return -1;
        return deque[front];
    }

    public int GetRear()
    {
        if (IsEmpty()) return -1;
        return deque[rear];
    }

    public bool IsEmpty()
    {
        return count == 0;
    }

    public bool IsFull()
    {
        return count == capacity;
    }
}

```
