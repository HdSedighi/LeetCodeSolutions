Solution: https://leetcode.com/problems/maximum-width-ramp/solutions/5895692/optimal-solution/

Description: https://leetcode.com/problems/maximum-width-ramp/description/

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem asks for the maximum width of a ramp, where a ramp is defined as two indices `i` and `j` (with `i < j`) such that `nums[i] <= nums[j]`. My first intuition is to search for all possible pairs `(i, j)` and calculate their widths, but this would be inefficient for large arrays due to the quadratic time complexity. Instead, we can reduce the problem by finding potential starting points of the ramp using a stack to track decreasing values, and then traverse the array backwards to find the maximum width ramp.

# Approach
<!-- Describe your approach to solving the problem. -->
1. **Building a Stack**: Traverse through the array once, and push indices of potential starting points (where values are strictly decreasing) onto a stack. This ensures that elements stored in the stack are in a non-increasing order.
  
2. **Finding the Maximum Ramp**: Starting from the end of the array, check if the current value can form a ramp with the values stored in the stack. If the current value is greater than or equal to the value at the index stored on the top of the stack, calculate the ramp width and update the maximum width. Continue this process until all possible ramps are evaluated.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
  The solution involves two linear traversals of the array. First, building the stack takes $$O(n)$$ time. Second, finding the maximum ramp also takes $$O(n)$$ time as we pop elements from the stack while iterating over the array. Thus, the overall time complexity is $$O(n)$$.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
  The space complexity is determined by the size of the stack, which in the worst case can store all the indices of the array. Therefore, the space complexity is $$O(n)$$.


# Code
```csharp []
using System;
using System.Collections.Generic;

public class Solution
{
    public int MaxWidthRamp(int[] nums)
    {
        // Stack to store indices of potential ramp start points in decreasing order
        Stack<int> stack = new Stack<int>();
        
        // Traverse the array and push indices of descending elements onto the stack
        for (int i = 0; i < nums.Length; i++)
        {
            if (stack.Count == 0 || nums[stack.Peek()] > nums[i])
            {
                stack.Push(i);
            }
        }

        int maxRampWidth = 0;

        // Traverse the array backwards to find the maximum width ramp
        for (int j = nums.Length - 1; j >= 0; j--)
        {
            // Try to find the largest ramp width by comparing elements on the stack
            while (stack.Count > 0 && nums[stack.Peek()] <= nums[j])
            {
                int i = stack.Pop();
                maxRampWidth = Math.Max(maxRampWidth, j - i);
            }
        }

        return maxRampWidth;
    }
}
```
