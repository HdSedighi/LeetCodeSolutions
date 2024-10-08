![image.png](https://assets.leetcode.com/users/images/368380d7-4daf-4e4b-85bb-3df627247422_1728396851.638084.png)

Solution: https://leetcode.com/problems/minimum-number-of-swaps-to-make-the-string-balanced/solutions/5886811/optimal-solution-beats-92/

Description: https://leetcode.com/problems/minimum-number-of-swaps-to-make-the-string-balanced/description/

# Intuition
The problem involves finding the minimum number of swaps to make a string of brackets balanced. A balanced string of brackets ensures that every closing bracket `]` has a corresponding preceding opening bracket `[`. To solve this, we need to track the imbalance between opening and closing brackets and perform swaps to correct the imbalance. The key observation is that an imbalance occurs when closing brackets appear without a matching opening bracket, requiring a swap with an unmatched opening bracket later in the string.

# Approach
1. Traverse the string while maintaining a `balance` variable:
   - If we encounter an opening bracket `[`, we increment `balance`.
   - If we encounter a closing bracket `]`, we decrement `balance`.
2. If `balance` becomes negative (i.e., more closing brackets than opening brackets), it indicates that we need a swap.
3. Each time we perform a swap (i.e., reset the imbalance), we update the `swaps` count and restore `balance` as if the imbalance was corrected.
4. After traversing the string, the `swaps` variable will contain the minimum number of swaps needed to make the string balanced.

# Complexity
- Time complexity:  
  The algorithm performs a single pass through the string, so the time complexity is $$O(n)$$, where `n` is the length of the string.

- Space complexity:  
  Since we only use a few integer variables (`balance` and `swaps`) and do not use any additional data structures that grow with input size, the space complexity is $$O(1)$$.


# Code
```csharp []
public class Solution {
    public int MinSwaps(string s) {
        int balance = 0;  // Tracks the number of unbalanced closing brackets
        int swaps = 0;    // Tracks the number of swaps required

        foreach (char ch in s) {
            if (ch == '[') {
                balance++;  // Found an opening bracket, increases the balance
            } else {
                balance--;  // Found a closing bracket, decreases the balance
            }

            // If balance is negative, we have too many closing brackets at this point
            if (balance < 0) {
                swaps++;       // Perform a swap to balance one closing bracket
                balance = 1;   // After the swap, balance is restored as if we had an opening bracket
            }
        }

        return swaps;
    }
}

```
