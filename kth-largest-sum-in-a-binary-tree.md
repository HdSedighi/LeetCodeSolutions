Solution: https://leetcode.com/problems/kth-largest-sum-in-a-binary-tree/solutions/5952590/optimal-solution-beats-100/

Description: https://leetcode.com/problems/kth-largest-sum-in-a-binary-tree/description/

![image.png](https://assets.leetcode.com/users/images/ec065fba-78ea-4ac0-a2a7-e5d65c1156ab_1729603215.9225123.png)

# Intuition
The problem requires calculating the sum of node values at each level of a binary tree and returning the kth largest sum. My first thought was to perform a level-order traversal (BFS) to compute the sum at each level. Once we have the sums, sorting them in descending order allows easy access to the kth largest sum.

# Approach
1. **Level Order Traversal (BFS)**: Using a queue, we traverse the tree level by level. For each level, sum up the node values.
2. **Storing Level Sums**: As we process each level, store its sum in a list.
3. **Sorting**: After gathering all the level sums, sort them in descending order.
4. **Return kth Largest**: If `k` is within the number of levels, return the kth largest sum; otherwise, return `-1`.
5. **Overflow Handling**: Since node values can be large, use the `long` data type to store sums to avoid overflow.

# Complexity
- Time complexity:  
  The time complexity is dominated by the BFS traversal and sorting of the level sums. BFS takes $$O(n)$$ time where `n` is the number of nodes in the tree. Sorting the level sums takes $$O(l \log l)$$ where `l` is the number of levels. In the worst case, the number of levels is proportional to the number of nodes, so the overall time complexity is $$O(n \log n)$$.

- Space complexity:  
  We use a queue for the BFS, which can hold up to $$O(n)$$ nodes at the deepest level. Additionally, we store level sums, which is at most $$O(l)$$, where `l` is the number of levels. Since `l` can be proportional to `n`, the space complexity is $$O(n)$$.


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
    public long KthLargestLevelSum(TreeNode root, int k) {
        if (root == null) return -1;

        // Use a queue to perform level order traversal
        Queue<TreeNode> queue = new Queue<TreeNode>();
        queue.Enqueue(root);

        List<long> levelSums = new List<long>();

        // Perform level-order traversal (BFS) to calculate level sums
        while (queue.Count > 0) {
            int levelSize = queue.Count;
            long levelSum = 0;  // Use long to avoid overflow

            for (int i = 0; i < levelSize; i++) {
                TreeNode currentNode = queue.Dequeue();
                levelSum += currentNode.val;  // Sum the values of the current level

                if (currentNode.left != null) queue.Enqueue(currentNode.left);
                if (currentNode.right != null) queue.Enqueue(currentNode.right);
            }

            levelSums.Add(levelSum);  // Store the sum of the current level
        }

        // Sort the level sums in descending order and check if we have at least 'k' levels
        levelSums.Sort((a, b) => b.CompareTo(a));  // Sort in descending order

        return (k <= levelSums.Count) ? levelSums[k - 1] : -1;
    }
}

```
