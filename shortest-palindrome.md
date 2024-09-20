Solution:https://leetcode.com/problems/shortest-palindrome/solutions/5813114/beats-100-easy-solution/

Description: https://leetcode.com/problems/shortest-palindrome/description/


![image.png](https://assets.leetcode.com/users/images/809f0a8a-c1e3-48e1-b060-810d5c0bf606_1726854256.4433455.png)

# Intuition
The problem requires converting a string into a palindrome by adding characters to the front. To minimize the number of characters added, the idea is to maximize the prefix of the string that is already a palindrome. Once we know how much of the string is a palindrome, we can add the minimum number of characters (the non-palindromic part in reverse) to the front to form the palindrome.

# Approach
1. **Reverse the string**: By reversing the string, we can check how much of the string's prefix matches its suffix, which indicates the largest palindromic prefix.
   
2. **Concatenate the original string and its reverse**: To avoid matching between the original and reversed string parts, we separate them with a special character (like `#`). This helps prevent false overlaps in the KMP matching process.

3. **KMP Algorithm**: Use the KMP (Knuth-Morris-Pratt) algorithm to find the longest proper prefix that is also a suffix of the concatenated string. This gives us the longest palindromic prefix in the original string.

4. **Result**: The shortest palindrome can be constructed by adding the non-palindromic part of the reversed string (which comes after the longest palindromic prefix) in front of the original string.

# Complexity
- **Time complexity**:
  The time complexity of the solution is $$O(n)$$, where $$n$$ is the length of the string `s`. This is because both the reversal of the string and the computation of the KMP table take linear time.

- **Space complexity**:
  The space complexity is $$O(n)$$ as we are storing the reversed string and the KMP table, both of which are proportional to the length of `s`.

# Code
```csharp []
public class Solution {
    public string ShortestPalindrome(string s)
    {
        if (string.IsNullOrEmpty(s)) return s;

        string rev = new string(s.ToCharArray().Reverse().ToArray());
        string combined = s + "#" + rev;

        // Calculate the KMP table (partial match table)
        int[] kmpTable = BuildKMPTable(combined);

        // Find the characters we need to add to the front
        int charactersToAdd = s.Length - kmpTable[combined.Length - 1];

        return rev.Substring(0, charactersToAdd) + s;
    }

    private int[] BuildKMPTable(string s)
    {
        int n = s.Length;
        int[] table = new int[n];
        int j = 0; // Length of the previous longest prefix suffix

        for (int i = 1; i < n; i++)
        {
            while (j > 0 && s[i] != s[j])
            {
                j = table[j - 1]; // Fall back in the table
            }

            if (s[i] == s[j])
            {
                j++;
            }

            table[i] = j;
        }

        return table;
    }
}
```
