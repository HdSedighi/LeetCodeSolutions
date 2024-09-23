Solution: https://leetcode.com/problems/extra-characters-in-a-string/solutions/5825271/optimal-solution/

Descroption: https://leetcode.com/problems/extra-characters-in-a-string/description/

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem involves breaking a string into substrings such that all substrings exist in a given dictionary, and any unused characters are counted as extra. Our goal is to minimize these extra characters. My first thought was to use dynamic programming, where we progressively build solutions for substrings of increasing lengths and find the optimal break points using the dictionary.

# Approach
<!-- Describe your approach to solving the problem. -->
We will use dynamic programming to track the minimum number of extra characters for each prefix of the string `s`.

1. **DP Array**: Create a DP array where `dp[i]` represents the minimum number of extra characters left over for the prefix of `s` ending at index `i-1`.
2. **Dictionary Lookup**: Store the dictionary words in a `HashSet` to enable O(1) average-time lookups.
3. **Substring Matching**: For each index `i` from 1 to `n` (where `n` is the length of `s`), we check all possible substrings `s[j:i]` where `j < i`. If a substring is found in the dictionary, we update the DP value for `dp[i]`. 
4. **Extra Character Case**: If no valid dictionary word is found for the substring ending at `i`, we add 1 extra character for that index and update `dp[i]` accordingly.
5. **Final Result**: The value in `dp[n]` will give us the minimum number of extra characters left after optimally breaking the string.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
The time complexity is $$O(n^2)$$, where `n` is the length of the string `s`. This is because for each index `i`, we check all substrings that end at `i`, resulting in a nested loop over the string. Each substring lookup in the dictionary is done in constant time due to the `HashSet`.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
The space complexity is $$O(n + m)$$, where `n` is the length of the string `s` (for the DP array) and `m` is the total size of the dictionary (used to store the dictionary in the `HashSet`).


# Code
```csharp []
using System;
using System.Collections.Generic;

public class Solution
{
    public int MinExtraChar(string s, IList<string> dictionary)
    {
        int n = s.Length;
        var dp = new int[n + 1];

        // Initialize dp array. dp[i] means the minimum extra characters left when considering the prefix of length i
        for (int i = 0; i <= n; i++)
            dp[i] = i;

        HashSet<string> dictSet = new HashSet<string>(dictionary);

        for (int i = 1; i <= n; i++)
        {
            // Try to match any substring ending at index i-1
            for (int j = 0; j < i; j++)
            {
                string substring = s.Substring(j, i - j);
                if (dictSet.Contains(substring))
                {
                    dp[i] = Math.Min(dp[i], dp[j]);
                }
            }
            dp[i] = Math.Min(dp[i], dp[i - 1] + 1); // Add 1 if we don't use the character at index i-1
        }

        return dp[n];
    }
}

```
