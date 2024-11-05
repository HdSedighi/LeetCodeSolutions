Solution: https://leetcode.com/problems/minimum-number-of-changes-to-make-binary-string-beautiful/solutions/6011603/optimal-solution/

Description: https://leetcode.com/problems/minimum-number-of-changes-to-make-binary-string-beautiful/description/

# Intuition
To solve the problem of making a binary string "beautiful," we need to ensure that the string can be partitioned into substrings of even length, consisting entirely of `0`s or entirely of `1`s. My first thought is to iterate through the string in pairs, checking if they are the same or different. If they are different, we would need to change one character to make the pair uniform. 

# Approach
The approach involves:
1. Traversing the string in pairs (two characters at a time).
2. Counting how many pairs consist of different characters.
3. Each pair that has different characters requires one change to make them uniform.
4. The total count of required changes gives us the minimum number of changes needed to transform the string into a beautiful string.

The algorithm can be implemented efficiently in a single pass through the string.

# Complexity
- Time complexity: $$O(n)$$
  
- Space complexity: $$O(1)$$


# Code
```csharp []
public class Solution {
    public int MinChanges(string s) {
        int changes = 0;
        
        // Traverse in pairs
        for (int i = 0; i < s.Length; i += 2) {
            // If the two consecutive characters are different, we need to change one of them
            if (s[i] != s[i + 1]) {
                changes++;
            }
        }

        return changes;
    }
}
```
