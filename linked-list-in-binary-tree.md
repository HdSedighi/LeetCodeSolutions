# LeetCodeSolutions: 1367-Medium-Linked List in Binary Tree



Solution: https://leetcode.com/problems/linked-list-in-binary-tree/solutions/5751842/optimal-solution-beats-100/

Description: https://leetcode.com/problems/linked-list-in-binary-tree/description/

![image.png](https://assets.leetcode.com/users/images/2d85a364-a4ca-4364-9c5a-48384831901c_1725727140.1202838.png)

# Intuition
The problem requires us to determine whether a linked list can be found as a downward path in a binary tree. The first step is to understand that a downward path in the binary tree means starting from any node and following its children downwards to match the entire linked list. 

To solve this problem, the approach is to traverse the binary tree and, at each node, check if a path starting from that node matches the linked list. The traversal can be performed using Depth-First Search (DFS), as it allows us to explore all possible paths from each node in the tree.

# Approach
1. **Depth-First Search (DFS) Traversal**: Start by performing a DFS traversal of the binary tree. For each node in the binary tree, check if there is a path that matches the linked list starting from that node.

2. **Matching Function**: For each node in the binary tree, use a helper function to check if the path starting from that node matches the linked list. This involves recursively checking each child node of the current node to see if it matches the next value in the linked list.

3. **Recursive Matching**: If a match is found starting from a node, return `True`. If not, continue the DFS traversal to explore other possible starting nodes in the binary tree.

4. **Termination**: If the linked list is fully matched or all possible paths are explored and no match is found, return the result accordingly.

# Complexity
- Time complexity: $$O(m \cdot n)$$
  - Here, \( m \) is the number of nodes in the binary tree and \( n \) is the number of nodes in the linked list. In the worst case, each node in the binary tree is visited, and for each node, a match operation (which involves traversing the linked list) is performed.

- Space complexity: $$O(h + n)$$
  - Where \( h \) is the height of the binary tree, representing the space needed for the recursive call stack during DFS. \( n \) represents the space needed to store the linked list nodes temporarily during matching.


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
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public bool IsSubPath(ListNode head, TreeNode root) {
        if (head == null) return true;
        if (root == null) return false;

        // Start DFS from the root
        return DFS(root, head);
    }

    private bool DFS(TreeNode node, ListNode listNode) {
        if (node == null) return false;

        // Check if current node starts the path
        if (IsMatch(node, listNode)) return true;

        // Continue DFS in both subtrees
        return DFS(node.left, listNode) || DFS(node.right, listNode);
    }

    private bool IsMatch(TreeNode node, ListNode listNode) {
        if (listNode == null) return true; // Reached end of the linked list
        if (node == null) return false; // Reached end of the binary tree path

        if (node.val != listNode.val) return false;

        // Continue matching down the path
        return IsMatch(node.left, listNode.next) || IsMatch(node.right, listNode.next);
    }
}

```
