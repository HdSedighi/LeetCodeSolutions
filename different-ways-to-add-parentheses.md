
![image.png](https://assets.leetcode.com/users/images/d6fd8784-0ca8-45ee-ae90-385a0e59e37f_1726752367.2607343.png)


Solution : https://leetcode.com/problems/different-ways-to-add-parentheses/solutions/5808578/beats-90-easy-solution/

Description: https://leetcode.com/problems/different-ways-to-add-parentheses/description/

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem asks to compute all possible results from different ways of grouping numbers and operators in a given expression. The intuition is that this is a problem that involves dividing the expression into parts and recursively solving each part. Since there are multiple ways to parenthesize an expression with binary operators, recursion is a natural approach to explore all combinations. By splitting the expression at each operator, and recursively solving for the left and right parts, we can compute all possible results. Memoization can help optimize the solution by storing results of previously computed sub-expressions.

# Approach
<!-- Describe your approach to solving the problem. -->
1. **Recursive Division**: We start by checking each character in the expression. When we find an operator (`+`, `-`, `*`), we split the expression into two sub-expressions: left and right. We recursively compute all possible results for the left and right parts.
   
2. **Combining Results**: After computing the results for the left and right parts, we combine them using the operator. This is done for every possible operator in the expression.

3. **Memoization**: To avoid redundant calculations, we use memoization to store the results of already computed sub-expressions. This ensures that for repeated sub-expressions, the solution is computed only once.

4. **Base Case**: If the expression is a number (i.e., it contains no operators), we directly return that number as the result.

5. **Iterating through operators**: By iterating through each operator and splitting the expression accordingly, we explore all possible ways of grouping the expression. For each operator, the recursive calls ensure that all combinations of left and right parts are explored.

6. **Result Aggregation**: After splitting and recursively computing all sub-expressions, the results are aggregated, and we return a list of all possible outcomes.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
The time complexity is difficult to compute exactly due to the recursive nature of the solution. However, in the worst case, the expression can generate a Catalan number of groupings. Thus, the time complexity is approximately $$O(n \cdot 2^n)$$, where \(n\) is the length of the expression. This is because at each operator, the expression is split into two parts, and the number of splits grows exponentially with the size of the expression.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
The space complexity is $$O(n \cdot 2^n)$$, where \(n\) is the length of the expression. This includes the space used by the recursion stack (depth of recursion is proportional to the length of the expression) and the space required to store results of sub-expressions in the memoization dictionary.

# Code
```csharp []
public class Solution {
    // Dictionary to store results for sub-expressions
    private Dictionary<string, List<int>> memo = new Dictionary<string, List<int>>();

    public IList<int> DiffWaysToCompute(string expression)
    {
        // Check if the result for this expression is already computed
        if (memo.ContainsKey(expression))
            return memo[expression];
        
        List<int> result = new List<int>();

        // Iterate through the expression to find operators
        for (int i = 0; i < expression.Length; i++)
        {
            char c = expression[i];

            // If the current character is an operator, split the expression
            if (c == '+' || c == '-' || c == '*')
            {
                // Compute the result for the left part
                IList<int> left = DiffWaysToCompute(expression.Substring(0, i));

                // Compute the result for the right part
                IList<int> right = DiffWaysToCompute(expression.Substring(i + 1));

                // Combine the results of the left and right parts using the operator
                foreach (int l in left)
                {
                    foreach (int r in right)
                    {
                        switch (c)
                        {
                            case '+':
                                result.Add(l + r);
                                break;
                            case '-':
                                result.Add(l - r);
                                break;
                            case '*':
                                result.Add(l * r);
                                break;
                        }
                    }
                }
            }
        }

        // If the expression does not contain any operators, it's a number
        if (result.Count == 0)
        {
            result.Add(int.Parse(expression));
        }

        // Store the result in the memo dictionary
        memo[expression] = result;

        return result;
    }
  }

```
