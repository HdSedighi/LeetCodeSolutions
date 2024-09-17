Solution: https://leetcode.com/problems/uncommon-words-from-two-sentences/solutions/5799893/optimal-solution/
Description:https://leetcode.com/problems/uncommon-words-from-two-sentences/description/

# Intuition
The problem requires finding words that appear exactly once in one sentence and not at all in the other sentence. My first thought was to split both sentences into individual words and count how many times each word appears. If a word appears exactly once across both sentences, it's an uncommon word.

# Approach
1. Split both `s1` and `s2` into individual words.
2. Use a dictionary to count the occurrence of each word from both sentences.
3. Iterate over the dictionary and collect words that appear exactly once.
4. Return the list of uncommon words.

This approach ensures that we capture uncommon words from both sentences by keeping track of how many times each word appears.

# Complexity
- Time complexity:
  The time complexity is $$O(n)$$, where $$n$$ is the total number of words in both sentences combined. This is because we iterate over each word twice: once to build the frequency dictionary and once to filter the uncommon words.

- Space complexity:
  The space complexity is $$O(n)$$, where $$n$$ is the total number of words in both sentences combined. We need space to store the word counts in the dictionary.


# Code
```csharp []
public class Solution {
    public string[] UncommonFromSentences(string s1, string s2) {
        // Split the sentences into words
        var words = s1.Split(' ').Concat(s2.Split(' '));

        // Create a dictionary to count the occurrences of each word
        var wordCount = new Dictionary<string, int>();
        foreach (var word in words)
        {
            if (wordCount.ContainsKey(word))
            {
                wordCount[word]++;
            }
            else
            {
                wordCount[word] = 1;
            }
        }

        // Return words that appear exactly once
        return wordCount.Where(w => w.Value == 1).Select(w => w.Key).ToArray();
    }
    
}
```
