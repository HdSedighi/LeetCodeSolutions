Solution: https://leetcode.com/problems/flip-equivalent-binary-trees/solutions/5962846/optimal-solution-beats-100/

Description: https://leetcode.com/problems/flip-equivalent-binary-trees/description/

![image.png](https://assets.leetcode.com/users/images/62ef224c-ddbe-43db-98dc-6a26508933d0_1729780304.6470184.png)


# Intuition
The problem requires us to determine whether two binary trees can become equivalent by performing a series of flip operations on their nodes. A flip operation involves swapping the left and right subtrees of a node. 

My first thought is that the core of the problem lies in comparing the structure of the two trees in different possible configurations. Since we are allowed to flip nodes, we need to check whether flipping the left and right children of a node can lead to equivalent trees. This suggests a recursive approach where we check each node and its children in both possible (flipped and non-flipped) configurations.

# Approach
1. **Base Case**: 
   - If both nodes being compared are `null`, they are trivially equivalent.
   - If one is `null` and the other is not, or if their values differ, the trees are not equivalent.
   
2. **Recursive Case**: 
   - For each node, we recursively check two conditions:
     1. The left child of `root1` is equivalent to the left child of `root2`, and the right child of `root1` is equivalent to the right child of `root2` (i.e., no flip required).
     2. The left child of `root1` is equivalent to the right child of `root2`, and the right child of `root1` is equivalent to the left child of `root2` (i.e., a flip occurred).
   
   If either condition holds true for all nodes, then the trees are flip equivalent.

This approach ensures that we explore all possible ways the trees can be made equivalent by flipping nodes where needed.

# Complexity
- Time complexity:
  The time complexity of this solution is $$O(n)$$ where $$n$$ is the number of nodes in the smaller tree. This is because, in the worst case, we must visit every node once to check both the flipped and non-flipped conditions.

- Space complexity:
  The space complexity is $$O(h)$$ where $$h$$ is the height of the tree, due to the recursive call stack. In the worst case, this can be $$O(n)$$ if the tree is skewed (i.e., the height is equal to the number of nodes).


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
     public bool FlipEquiv(TreeNode root1, TreeNode root2)
    {
        // If both nodes are null, the trees are equivalent
        if (root1 == null && root2 == null) return true;

        // If one of them is null or values are not the same, trees are not equivalent
        if (root1 == null || root2 == null || root1.val != root2.val) return false;

        // Recursively check two possible scenarios:
        // 1. The children are not flipped: left with left and right with right
        // 2. The children are flipped: left with right and right with left
        return (FlipEquiv(root1.left, root2.left) && FlipEquiv(root1.right, root2.right)) ||
               (FlipEquiv(root1.left, root2.right) && FlipEquiv(root1.right, root2.left));
    }
}
```
