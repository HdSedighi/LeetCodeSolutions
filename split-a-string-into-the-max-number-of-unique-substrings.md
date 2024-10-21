Solution: https://leetcode.com/problems/split-a-string-into-the-max-number-of-unique-substrings/solutions/5947764/optimal-solution-beats-100/
Description: https://leetcode.com/problems/split-a-string-into-the-max-number-of-unique-substrings/description/


![image.png](https://assets.leetcode.com/users/images/1730007c-fead-47df-9273-a5aab160b74f_1729522243.4601429.png)

# Intuition
The problem requires splitting a string into the maximum number of unique substrings. The first intuition is to explore all possible ways to split the string, ensuring that each substring is unique. Since we need to maximize the number of unique substrings, a backtracking approach comes to mind where we attempt different splits and track the substrings used so far. This way, we can explore every possible combination while ensuring substrings are not reused.

# Approach
1. Use a backtracking algorithm to explore every possible way to split the string.
2. At each step, take a substring starting from the current position, and if it hasn't been used before, add it to a set of unique substrings.
3. Recursively continue the process for the remaining part of the string.
4. Keep track of the maximum number of unique substrings found during the recursive exploration.
5. After each recursive call, backtrack by removing the current substring from the set to try other possibilities.

By exploring all possible ways to split the string and only considering unique substrings, we can find the maximum number of unique splits.

# Complexity
- Time complexity:
  The time complexity is approximately $$O(2^n)$$ where $$n$$ is the length of the string. This is because, for each character in the string, we decide whether to start a new substring, leading to an exponential number of possibilities.

- Space complexity:
  The space complexity is $$O(n)$$, where $$n$$ is the length of the string. This is due to the recursive call stack and the space required to store the set of unique substrings.


# Code
```csharp []
class Solution
{
    public int MaxUniqueSplit(string s)
    {
        return Backtrack(s, new HashSet<string>(), 0);
    }

    private int Backtrack(string s, HashSet<string> uniqueSubstrings, int start)
    {
        // If we've reached the end of the string, return 0 (no more substrings to split)
        if (start == s.Length)
            return 0;

        int maxSplits = 0;

        // Try every possible substring starting from 'start' position
        for (int i = start; i < s.Length; i++)
        {
            // Take the substring from 'start' to 'i'
            string currentSubstring = s.Substring(start, i - start + 1);

            // If the substring is not already used, add it and continue to backtrack
            if (!uniqueSubstrings.Contains(currentSubstring))
            {
                uniqueSubstrings.Add(currentSubstring);

                // Recursively call Backtrack for the rest of the string and count splits
                int remainingSplits = Backtrack(s, uniqueSubstrings, i + 1);
                
                // Update the maximum number of unique splits
                maxSplits = Math.Max(maxSplits, 1 + remainingSplits);

                // Remove the substring after backtracking
                uniqueSubstrings.Remove(currentSubstring);
            }
        }

        return maxSplits;
    }
}
```
