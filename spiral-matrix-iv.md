# LeetCodeSolutions: 2326-spiral-matrix-iv


Solution: https://leetcode.com/problems/spiral-matrix-iv/solutions/5761393/beats-90-easy-solution/

Description: https://leetcode.com/problems/spiral-matrix-iv/description/

![image.png](https://assets.leetcode.com/users/images/5e26d58d-7127-477d-9536-1440f1af0174_1725896829.0218847.png)

# Intuition
The problem requires filling an `m x n` matrix with elements from a linked list in a spiral order (clockwise). My first thought was to simulate the spiral traversal by maintaining four boundaries (`top`, `bottom`, `left`, `right`) that shrink as we traverse the matrix in layers. We can keep moving in four directions: left to right, top to bottom, right to left, and bottom to top, until all values from the linked list are exhausted. If there are remaining empty spaces, they can be filled with `-1`.

# Approach
1. **Matrix Initialization**: Create a 2D matrix with `m` rows and `n` columns, filled initially with `-1`.
2. **Boundary Pointers**: Use four variables: `top`, `bottom`, `left`, and `right` to define the boundaries of the spiral traversal.
3. **Spiral Traversal**:
    - Traverse from left to right across the `top` row and then shrink the `top` boundary.
    - Traverse from top to bottom along the `right` column and then shrink the `right` boundary.
    - Traverse from right to left along the `bottom` row and then shrink the `bottom` boundary.
    - Traverse from bottom to top along the `left` column and then shrink the `left` boundary.
4. **Handling the Linked List**: As we traverse the matrix in spiral order, insert the values from the linked list into the corresponding matrix positions. If the list ends before filling the matrix, the remaining positions will stay as `-1`.
5. **End Condition**: Continue this process while there are elements in the linked list and the boundaries haven’t crossed each other.

# Complexity
- **Time complexity**:
  The matrix has `m * n` elements, and we visit each element exactly once in spiral order. Thus, the time complexity is:
  $$O(m \times n)$$

- **Space complexity**:
  The space complexity is determined by the size of the matrix we need to create, which is proportional to the number of elements:
  $$O(m \times n)$$


# Code
```csharp []
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public int[][] SpiralMatrix(int m, int n, ListNode head) {
        int[][] matrix = new int[m][];
        for (int i = 0; i < m; i++) {
            matrix[i] = new int[n];
            Array.Fill(matrix[i], -1); // Fill with -1 by default
        }

        int top = 0, bottom = m - 1, left = 0, right = n - 1;
        ListNode current = head;

        while (top <= bottom && left <= right && current != null) {
            // Traverse from left to right on the top row
            for (int i = left; i <= right && current != null; i++) {
                matrix[top][i] = current.val;
                current = current.next;
            }
            top++; // Move top boundary down

            // Traverse from top to bottom on the right column
            for (int i = top; i <= bottom && current != null; i++) {
                matrix[i][right] = current.val;
                current = current.next;
            }
            right--; // Move right boundary left

            // Traverse from right to left on the bottom row
            for (int i = right; i >= left && current != null; i--) {
                matrix[bottom][i] = current.val;
                current = current.next;
            }
            bottom--; // Move bottom boundary up

            // Traverse from bottom to top on the left column
            for (int i = bottom; i >= top && current != null; i--) {
                matrix[i][left] = current.val;
                current = current.next;
            }
            left++; // Move left boundary right
        }

        return matrix;
    }
}
```
