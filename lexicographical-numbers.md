Solution: https://leetcode.com/problems/lexicographical-numbers/solutions/5817178/beats-82-easy-solution/

Description: https://leetcode.com/problems/lexicographical-numbers/description/


![image.png](https://assets.leetcode.com/users/images/1e94cfb5-5eb2-440f-94e4-2ac5f5458d9f_1726940877.006746.png)

# Intuition
The first thought to solve this problem is to recognize that lexicographical order can be seen as a depth-first traversal of a tree, where each node represents a number and the branches represent appending digits (from 0 to 9). Starting from `1`, you can explore each level by multiplying by 10 and incrementing as necessary.

The key is to explore numbers in the lexicographical order (i.e., numbers like 1, 10, 100, etc.) and skip over numbers that exceed the given `n`.

# Approach
The approach is to use a depth-first traversal strategy to generate numbers from `1` to `n` in lexicographical order:
- Start with the number `1`.
- Try to "go deeper" by multiplying the current number by `10` (which gives the next lexicographical level).
- If multiplying by `10` exceeds `n`, increment the current number instead.
- If incrementing results in a number with a trailing zero (like 10, 20, etc.), adjust by dividing out the zeroes to maintain lexicographical order.
- Continue this process until you have collected all numbers from `1` to `n`.

# Complexity
- Time complexity:
  The time complexity is $$O(n)$$ because we are visiting each number between `1` and `n` exactly once in a lexicographical sequence.

- Space complexity:
  The space complexity is $$O(1)$$ in terms of extra space (ignoring the result list), since we do not use any additional data structures that scale with input size `n`. The result list is the only space used to store the output.


# Code
```csharp []
public class Solution {
    public IList<int> LexicalOrder(int n) {
         List<int> result = new List<int>();
        int current = 1;

        // Loop until we reach the total number
        for (int i = 0; i < n; i++)
        {
            result.Add(current);
            if (current * 10 <= n)
            {
                // Move to the next lexicographical level
                current *= 10;
            }
            else
            {
                // Increment the current number
                if (current >= n)
                {
                    current /= 10;
                }
                current++;
                // Skip trailing zeros
                while (current % 10 == 0)
                {
                    current /= 10;
                }
            }
        }

        return result;
    }
}
```
