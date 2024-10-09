Solution: https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/solutions/5891412/easy-optimal-solution/

Description: https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/description/

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The goal is to ensure that the string of parentheses is balanced by adding the minimum number of moves (either opening or closing parentheses). We can track the balance of parentheses while traversing the string by counting how many opening parentheses `(` are unmatched and how many closing parentheses `)` appear without a corresponding open one. By counting these two situations, we can easily determine the number of moves required to balance the string.

# Approach
<!-- Describe your approach to solving the problem. -->
We iterate through the string while maintaining two counters: `open` to track unmatched opening parentheses `(` and `close` to track unmatched closing parentheses `)`. 

- If we encounter an opening parenthesis `(`, we increment the `open` counter.
- If we encounter a closing parenthesis `)`, we first check if there are any unmatched opening parentheses (`open > 0`). If there are, we decrement the `open` counter to signify a match. If there are no unmatched opening parentheses, we increment the `close` counter to track the unmatched closing parentheses.
  
At the end of the iteration, the total number of unmatched parentheses is the sum of `open` (remaining unmatched opening parentheses) and `close` (remaining unmatched closing parentheses). This gives us the minimum number of moves required to make the string valid.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
The time complexity is $$O(n)$$ because we are iterating through the string once, where `n` is the length of the input string.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
The space complexity is $$O(1)$$ as we only need a few variables (`open` and `close`) to track the count of unmatched parentheses. We do not use any additional data structures that grow with input size.


# Code
```csharp []
public class Solution {
    public int MinAddToMakeValid(string s) {
        int open = 0; // Tracks unmatched '('
        int close = 0; // Tracks unmatched ')'

        foreach (char c in s) {
            if (c == '(') {
                open++; // Found an unmatched '('
            } else {
                if (open > 0) {
                    open--; // Found a matching ')' for an unmatched '('
                } else {
                    close++; // Found an unmatched ')'
                }
            }
        }

        // The total number of moves needed is the sum of unmatched '(' and unmatched ')'
        return open + close;
    }
}

```
