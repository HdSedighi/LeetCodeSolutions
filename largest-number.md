Solution: https://leetcode.com/problems/largest-number/solutions/5804747/easy-solution/

Description: https://leetcode.com/problems/largest-number/description/

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem requires us to arrange a list of non-negative integers such that their concatenation forms the largest possible number. My first thought was that this could be done by sorting the numbers in a way that prioritizes the most significant digits. However, simply sorting based on the numbers themselves wouldn’t work due to different digit lengths. The key insight is that for any two numbers `a` and `b`, we should compare the concatenated strings `a + b` and `b + a` and sort them accordingly.

# Approach
<!-- Describe your approach to solving the problem. -->
1. Convert each integer in the list to a string so that we can concatenate them for comparison.
2. Sort the string list using a custom comparator that compares the concatenated results of two numbers. Specifically, for two strings `a` and `b`, compare `a + b` and `b + a`, and sort them in descending order based on which concatenation is larger.
3. After sorting, if the largest number is `0`, return "0" (to handle cases like `[0, 0]`).
4. Join the sorted strings into a single string and return the result.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
  Sorting the array of numbers takes $$O(n \log n)$$, where $$n$$ is the number of elements in the list. The custom comparator involves string concatenation, which in the worst case takes $$O(k)$$ per comparison, where $$k$$ is the average number of digits of the numbers. Thus, the total time complexity is $$O(n \log n \cdot k)$$.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
  The space complexity is $$O(n)$$, where $$n$$ is the number of integers in the list. We need additional space to store the string representations of the integers and the result.


# Code
```csharp []
public class Solution {
     public string LargestNumber(int[] nums) {
        // Convert each number to a string
        List<string> numStrings = new List<string>();
        foreach (var num in nums) {
            numStrings.Add(num.ToString());
        }
        
        // Sort the strings using a custom comparison rule
        numStrings.Sort((a, b) => string.Compare(b + a, a + b));

        // If the largest number is "0", the result should be "0" (to handle cases like [0, 0])
        if (numStrings[0] == "0") {
            return "0";
        }

        // Join the sorted strings into one large number
        return string.Join("", numStrings);
    }
}
```
