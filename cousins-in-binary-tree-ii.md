Solution: https://leetcode.com/problems/cousins-in-binary-tree-ii/solutions/5957990/optimal-solution-beats-100/

Description: https://leetcode.com/problems/cousins-in-binary-tree-ii/description/

![image.png](https://assets.leetcode.com/users/images/93e7ac41-c71e-4e42-b83a-84bb78cabcc7_1729693775.3351033.png)


# Intuition
The problem involves replacing the value of each node in a binary tree with the sum of its cousins' values. Cousins are defined as nodes that are at the same depth but have different parents. Initially, I thought about traversing the tree level by level (using BFS) to collect nodes at the same level and compute their cousins' sums. However, depth-first search (DFS) could also be an efficient way to achieve this since we can manage the children of each node and maintain sums.

# Approach
1. **Initialization**: Start by setting the root node's value to `0` because it has no cousins.
2. **Depth-First Search (DFS)**: Implement a recursive DFS function that takes a list of nodes at the current level.
   - For each node, calculate the sum of the values of their children (i.e., left and right).
   - For each node, compute the new value for its children by subtracting the current node's children values from the total sum of all children at that level.
   - Collect all children nodes for the next DFS level.
3. **Recursive Traversal**: Continue the DFS process until all levels of the tree are processed.

This method ensures that each node's value is updated based on the sum of its cousins' values.

# Complexity
- Time complexity: $$O(n)$$
  - We traverse each node in the tree exactly once, where `n` is the number of nodes in the binary tree.

- Space complexity: $$O(n)$$
  - In the worst case, the depth of the recursion stack can go up to `n` (in the case of a skewed tree), and we also maintain a list to hold nodes at each level, which can be at most `n` in size.


# Code
```csharp []
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
public TreeNode ReplaceValueInTree(TreeNode root) {
        // Set the value of the root to 0 as it has no cousins
        root.val = 0;
        dfs(new List<TreeNode> { root });
        return root;
    }

    private void dfs(List<TreeNode> arr) {
        if (arr.Count == 0) return;

        int sum = 0;
        foreach (var node in arr) {
            if (node == null) continue;
            // Calculate the sum of the children of all nodes at the current level
            if (node.left != null) sum += node.left.val;
            if (node.right != null) sum += node.right.val;
        }

        List<TreeNode> childArr = new List<TreeNode>();
        foreach (var node in arr) {
            int curSum = 0;

            // Calculate the current node's children sum
            if (node.left != null) curSum += node.left.val;
            if (node.right != null) curSum += node.right.val;

            // Update the left child
            if (node.left != null) {
                node.left.val = sum - curSum; // Update value to sum of cousins
                childArr.Add(node.left); // Collect children for the next DFS level
            }
            // Update the right child
            if (node.right != null) {
                node.right.val = sum - curSum; // Update value to sum of cousins
                childArr.Add(node.right); // Collect children for the next DFS level
            }
        }

        // Recur for the next level
        dfs(childArr);
    }
}
```
