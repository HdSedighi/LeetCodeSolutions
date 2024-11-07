Solution: https://leetcode.com/problems/largest-combination-with-bitwise-and-greater-than-zero/solutions/6017331/optimal-solution/

Description: https://leetcode.com/problems/largest-combination-with-bitwise-and-greater-than-zero/description/

# Intuition
To solve this problem, we need to understand how the bitwise AND operation works in combinations. The bitwise AND of multiple numbers is greater than zero only if there is at least one bit position where all numbers in the combination have a 1. Therefore, to maximize the size of the combination with a bitwise AND greater than zero, we should look for the bit position with the highest count of numbers that have a 1 in that position. This count will give the largest combination size with a bitwise AND greater than zero.

# Approach
1. **Iterate Over Bit Positions**: Since the maximum value in the `candidates` array is \(10^7\), which fits within 24 bits, we only need to check bit positions from 0 to 23.
2. **Count Set Bits**: For each bit position, count how many numbers in the array have that particular bit set to 1. This count represents the number of candidates that could potentially form a combination with a bitwise AND greater than zero if they share this bit.
3. **Track the Maximum Count**: For each bit position, keep track of the maximum count across all bit positions. This maximum count will be the size of the largest combination that has a bitwise AND greater than zero.

# Complexity
- Time complexity:
  - The time complexity is \(O(n \times 24)\), where \(n\) is the length of the `candidates` array. We iterate through each bit position (0 to 23) and check each candidate in the array to see if the bit is set.

- Space complexity:
  - The space complexity is \(O(1)\) because we only use a few variables to store counts and track the maximum count, regardless of the input size.


# Code
```csharp []
public class Solution
{
    public int LargestCombination(int[] candidates)
    {
        int maxCount = 0;
        // We assume 24 bits, as 10^7 (maximum value of candidates[i]) can fit within 24 bits.
        for (int bit = 0; bit < 24; bit++)
        {
            int count = 0;
            foreach (int num in candidates)
            {
                // Check if the bit at position `bit` is set in `num`.
                if ((num & (1 << bit)) != 0)
                {
                    count++;
                }
            }
            // Update the maximum count if the current bit position has a higher count.
            maxCount = Math.Max(maxCount, count);
        }
        return maxCount;
    }
}

```
