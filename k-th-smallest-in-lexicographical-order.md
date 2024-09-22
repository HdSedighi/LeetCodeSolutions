Solurion: https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/solutions/5820428/optimal-solution/

Description: https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/description/


# Intuition
The problem asks for the kth smallest number in lexicographical order. The lexicographical order of numbers is essentially the order you'd get if you listed the numbers as strings, one by one, rather than by their numeric values.

To find the kth number efficiently without generating all numbers in lexicographical order, we can utilize a tree-like traversal of the lexicographical order. Starting from `1`, we can calculate how many numbers would exist between two consecutive prefixes (like `1` and `2`, or `10` and `11`). Using this, we can either move to the next prefix or go deeper into the current prefix (i.e., from `1` to `10`).

# Approach
1. Start at the smallest number (`curr = 1`).
2. Compute how many numbers exist between `curr` and the next lexicographical number (`curr + 1`) under the constraint `n`.
   - This is done by counting how many numbers start with `curr` and lie between `curr` and `curr + 1`, while staying within the range `[1, n]`.
3. If the number of steps between `curr` and `curr + 1` is smaller than `k`, move to the next number by incrementing `curr` and subtract the number of steps from `k`.
4. If the number of steps is greater than or equal to `k`, it means the kth number is within the range of numbers starting with `curr`, so move to the next level by multiplying `curr` by 10 and decrementing `k`.
5. Repeat the process until `k == 0`.

# Complexity
- Time complexity:
  The algorithm navigates through the digits of the numbers in a tree-like structure, with the number of steps roughly proportional to the number of digits in `n`. Each iteration involves calculating how many numbers are within certain ranges, which can be done in logarithmic time. Thus, the time complexity is approximately $$O(\log(n) \cdot \log(n))$$, where the first log factor comes from traversing the levels of the tree, and the second log factor from calculating the steps between prefixes.

- Space complexity:
  The space complexity is $$O(1)$$ because the approach only uses a constant amount of extra space for variables such as `curr`, `steps`, and `k`.


# Code
```csharp []
public class Solution {
    public int FindKthNumber(int n, int k) {
        int curr = 1;
        k--; // subtract 1 since we are starting with the first number
        
        while (k > 0) {
            long steps = CalculateSteps(n, curr, curr + 1);
            if (steps <= k) {
                // Move to the next number
                curr++;
                k -= (int)steps;
            } else {
                // Move down to the next level
                curr *= 10;
                k--;
            }
        }
        
        return curr;
    }

    // Calculate how many numbers exist between curr and next, under the limit n
    private long CalculateSteps(int n, long curr, long next) {
        long steps = 0;
        while (curr <= n) {
            steps += Math.Min(n + 1, next) - curr;
            curr *= 10;
            next *= 10;
        }
        return steps;
    }
}

```
