Solution: https://leetcode.com/problems/delete-characters-to-make-fancy-string/solutions/5993347/optimal-solution/

Description: https://leetcode.com/problems/delete-characters-to-make-fancy-string/description/

# Intuition
To solve this problem, we observe that the goal is to ensure no three consecutive characters in the string are the same. Therefore, the intuition is to iterate through the string while keeping track of consecutive characters, and only add a character to the result if it doesn’t create a sequence of three consecutive identical characters.

# Approach
1. Initialize a `StringBuilder` to build the result string efficiently.
2. Keep a `consecutiveCount` variable to track the count of consecutive characters.
3. Start by adding the first character of the input string to the result.
4. For each subsequent character:
   - Check if it matches the previous character. If it does, increment `consecutiveCount`.
   - If `consecutiveCount` is less than 3, add the character to the result; otherwise, skip it.
   - If the character is different from the previous one, reset `consecutiveCount` to 1 and add the character to the result.
5. Continue this process until the entire string is processed.
6. Convert the `StringBuilder` to a string and return it as the final result.

This approach ensures that we only add characters that won’t create three consecutive identical characters, resulting in a "fancy" string with minimal deletions.

# Complexity
- **Time complexity:** $$O(n)$$, where $$n$$ is the length of the input string. We make a single pass through the string to construct the result, making this approach linear in time.
  
- **Space complexity:** $$O(n)$$, where $$n$$ is the length of the input string. The additional space is used for the `StringBuilder` to construct the result.


# Code
```csharp []
public class Solution
{
    public string MakeFancyString(string s)
    {
        // Initialize a StringBuilder for the result
        var result = new System.Text.StringBuilder();
        
        // To track the count of consecutive identical characters
        int consecutiveCount = 1;
        
        // Start with the first character
        result.Append(s[0]);
        
        for (int i = 1; i < s.Length; i++)
        {
            // If the current character is the same as the previous one
            if (s[i] == s[i - 1])
            {
                consecutiveCount++;
            }
            else
            {
                // Reset the count if it's a different character
                consecutiveCount = 1;
            }
            
            // Add the character to the result only if it doesn't form three consecutive identical characters
            if (consecutiveCount < 3)
            {
                result.Append(s[i]);
            }
        }
        
        // Convert StringBuilder to string and return
        return result.ToString();
    }
}

```
