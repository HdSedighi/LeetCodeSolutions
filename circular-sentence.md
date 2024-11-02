Solution: https://leetcode.com/problems/circular-sentence/solutions/5998164/optimal-solution/

Description: https://leetcode.com/problems/circular-sentence/description/

# Intuition
To determine if a sentence is circular, we need to verify if:
1. The last character of each word matches the first character of the next word.
2. The last character of the last word matches the first character of the first word.

The circular nature of the problem hints at using modular arithmetic, which makes it easy to connect the last element back to the first.

# Approach
1. **Split the Sentence**: Split the sentence into words using spaces as delimiters.
2. **Loop Through Words**: Iterate through each word in the list:
   - For each word, compare its last character to the first character of the next word.
   - For the last word, compare its last character to the first character of the first word to satisfy the circular condition.
3. **Return Result**: If any pair of characters does not match the circular condition, return `false`. If all pairs satisfy the condition, return `true`.

The code uses modular indexing to simplify the circular check, ensuring that when we reach the last word, we can wrap around to the first word by using the modulus operator (`%`).

# Complexity
- **Time complexity**:  
  $$O(n)$$, where \( n \) is the number of characters in the sentence. This is because splitting the sentence into words and iterating through them both take linear time.

- **Space complexity**:  
  $$O(m)$$, where \( m \) is the number of words. We store the words in an array after splitting, which requires space proportional to the number of words.


# Code
```csharp []

public class Solution
{
    public bool IsCircularSentence(string sentence)
    {
        // Split the sentence into words by spaces
        string[] words = sentence.Split(' ');

        // Check the circular condition for each word pair
        for (int i = 0; i < words.Length; i++)
        {
            string currentWord = words[i];
            string nextWord = words[(i + 1) % words.Length];

            // Check if the last character of the current word
            // is equal to the first character of the next word
            if (currentWord[^1] != nextWord[0])
            {
                return false;
            }
        }

        // If all conditions are met, return true
        return true;
    }
}

```
