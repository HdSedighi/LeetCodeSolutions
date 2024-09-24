Solution: https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix/solutions/5828517/optimal-solution/

Description:https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix/description/

# Intuition
The problem requires finding the longest common prefix between numbers from two different arrays. My first thought was to use a strategy that builds prefixes for numbers in one array and then compares those prefixes with numbers in the other array. This would help identify the longest common prefix efficiently by using a dictionary to store the prefixes, allowing for fast lookup.

# Approach
1. **Build a Prefix Map**: 
   - For each number in `arr1`, convert the number to a string and generate all possible prefixes (e.g., for the number `123`, generate `1`, `12`, `123`). 
   - Store these prefixes in a dictionary where the keys are the prefixes and the values are the count of occurrences (though for this problem, we don't need the count, just the existence of the prefix).

2. **Check for Common Prefixes**: 
   - For each number in `arr2`, generate all its prefixes and check if any of them exist in the prefix map created from `arr1`. 
   - If a common prefix is found, track its length and update the maximum length of any common prefix found across all pairs.

3. **Return the Longest Prefix Length**: 
   - After iterating through all pairs of numbers, return the length of the longest common prefix found. If no common prefix exists, return `0`.

# Complexity
- Time complexity:
  - Building the prefix map for `arr1` takes `O(m * d1)`, where `m` is the number of elements in `arr1`, and `d1` is the average number of digits in the elements of `arr1`.
  - Checking for common prefixes with `arr2` takes `O(n * d2)`, where `n` is the number of elements in `arr2`, and `d2` is the average number of digits in the elements of `arr2`.
  - So the overall time complexity is $$O(m * d1 + n * d2)$$.

- Space complexity:
  - The space complexity is dominated by the storage required for the prefix map. The total number of prefixes that can be generated is proportional to the sum of the lengths of the numbers in `arr1`. Therefore, the space complexity is $$O(m * d1)$$ for storing the prefixes from `arr1`.


# Code
```csharp []
using System;
using System.Collections.Generic;

public class Solution
{
    public int LongestCommonPrefix(int[] arr1, int[] arr2)
    {
        Dictionary<string, int> prefixMap = new Dictionary<string, int>();

        // Step 1: Build the prefix map for arr1
        foreach (int num in arr1)
        {
            string strNum = num.ToString();
            string prefix = "";
            foreach (char ch in strNum)
            {
                prefix += ch;
                if (prefixMap.ContainsKey(prefix))
                {
                    prefixMap[prefix]++;
                }
                else
                {
                    prefixMap[prefix] = 1;
                }
            }
        }

        int maxLength = 0;

        // Step 2: Check for common prefixes in arr2
        foreach (int num in arr2)
        {
            string strNum = num.ToString();
            string prefix = "";
            foreach (char ch in strNum)
            {
                prefix += ch;
                if (prefixMap.ContainsKey(prefix))
                {
                    maxLength = Math.Max(maxLength, prefix.Length);
                }
            }
        }

        return maxLength;
    }
}
```
