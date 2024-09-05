# LeetCodeSolutions: 2028-Medium-find-missing-observations



Solution: https://leetcode.com/problems/find-missing-observations/solutions/5741492/easy-solution-beats-82/

Description: https://leetcode.com/problems/find-missing-observations/description/

![image.png](https://assets.leetcode.com/users/images/52711ac7-9c05-4df0-8de8-89aa25c46eec_1725542068.3428433.png)


# Intuition
The problem asks us to find missing dice rolls, ensuring that the total average matches the given value. Our first thought is to calculate the total sum of all `n + m` rolls based on the average and then subtract the sum of the `m` known rolls. The remainder gives us the sum that needs to be distributed among the `n` missing rolls. We then need to check if it's possible to distribute this sum into `n` dice rolls, where each roll must have a value between 1 and 6. 

# Approach
1. First, compute the total sum for `n + m` rolls by multiplying the given mean with `n + m`.
2. Calculate the sum of the observed rolls.
3. Determine the required sum for the missing `n` rolls by subtracting the sum of observed rolls from the total sum.
4. Check if it's feasible to distribute the remaining sum across `n` rolls (each roll must be between 1 and 6). If the required sum is smaller than `n` or larger than `6 * n`, it's impossible to solve the problem, so return an empty array.
5. Distribute the missing sum evenly across the `n` rolls, ensuring that no roll exceeds 6 and no roll is less than 1.

# Complexity
- Time complexity:
  $$O(m + n)$$ 
  - We iterate through the given `m` rolls to compute their sum. Then, we construct the `n` missing rolls, which takes linear time.

- Space complexity:
  $$O(n)$$
  - We only need additional space to store the `n` missing rolls.


# Code
```csharp []
public class Solution {
   public int[] MissingRolls(int[] rolls, int mean, int n)
    {
        int m = rolls.Length;

        // Calculate the total sum needed for the n + m rolls
        int totalSum = mean * (n + m);
        
        // Calculate the sum of the m known rolls
        int knownSum = 0;
        foreach (int roll in rolls)
        {
            knownSum += roll;
        }

        // Calculate the sum needed for the n missing rolls
        int missingSum = totalSum - knownSum;

        // Check if it's possible to distribute the missing sum into n rolls
        if (missingSum < n || missingSum > 6 * n)
        {
            // If the sum is too small or too large, it's impossible to find a valid solution
            return new int[0];
        }

        // Create the result array for missing rolls
        int[] result = new int[n];

        // Distribute the missing sum as evenly as possible
        for (int i = 0; i < n; i++)
        {
            // Assign each element as close to 1 as possible while making sure we reach the missingSum
            result[i] = Math.Min(6, missingSum - (n - 1 - i));
            missingSum -= result[i];
        }

        return result;
    }
}
```
