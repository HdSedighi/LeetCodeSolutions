Solution: https://leetcode.com/problems/sum-of-prefix-scores-of-strings/solutions/5832425/beats-86-easy-solution/

Description: https://leetcode.com/problems/sum-of-prefix-scores-of-strings/description/


![image.png](https://assets.leetcode.com/users/images/739598d2-6ee1-4c5a-b314-212180d513e3_1727273764.526646.png)


# Intuition
The problem requires calculating prefix scores for each word in the array by counting how many other words share the same prefixes. A brute-force approach could involve iterating through all prefixes of each word and counting how many words match each prefix. However, this would result in high time complexity, especially for large inputs.

To optimize, we can leverage a **Trie** (prefix tree) which allows us to store and query prefixes efficiently. The Trie structure avoids duplicating common prefixes in memory and allows for quick prefix count lookups as we traverse the tree.

# Approach
1. **Trie Construction**:
   - Insert all words into a Trie. As we insert each character of a word, we update a count in each Trie node to track how many words share that prefix.
   
2. **Prefix Score Calculation**:
   - For each word, traverse the Trie from the root node, character by character. At each step, add the count from the Trie node to the total score for that word's prefix.

3. **Efficiency**:
   - The Trie allows us to efficiently track and count prefixes shared among multiple words, reducing redundant calculations and improving memory usage compared to a brute-force approach.

# Complexity
- Time complexity:
  - **Trie Construction**: Inserting a word into the Trie takes $$O(m)$$ time, where $$m$$ is the length of the word. Since we do this for each word in the list, the total time complexity for building the Trie is $$O(n \cdot m)$$, where $$n$$ is the number of words.
  - **Prefix Score Calculation**: For each word, calculating the prefix score requires traversing the Trie, which also takes $$O(m)$$ time. Therefore, the total time complexity is $$O(n \cdot m)$$.

- Space complexity:
  - **Trie Storage**: In the worst case, each character in each word could create a new node in the Trie. The total space complexity is $$O(n \cdot m)$$, where $$n$$ is the number of words and $$m$$ is the average length of the words. This is more space-efficient than storing every possible prefix separately, as common prefixes are shared in the Trie.


# Code
```csharp []
using System;
using System.Collections.Generic;

class Solution
{
    // Define a TrieNode class for Trie
    public class TrieNode
    {
        public Dictionary<char, TrieNode> Children = new Dictionary<char, TrieNode>();
        public int Count = 0; // To store how many words go through this node
    }

    // Define a Trie class
    public class Trie
    {
        public TrieNode Root;

        public Trie()
        {
            Root = new TrieNode();
        }

        // Insert a word into the trie and update the prefix counts
        public void Insert(string word)
        {
            TrieNode node = Root;
            foreach (char c in word)
            {
                if (!node.Children.ContainsKey(c))
                {
                    node.Children[c] = new TrieNode();
                }
                node = node.Children[c];
                node.Count++; // Increment the count for the prefix
            }
        }

        // Calculate the sum of prefix scores for a given word
        public int GetPrefixScore(string word)
        {
            TrieNode node = Root;
            int score = 0;
            foreach (char c in word)
            {
                if (!node.Children.ContainsKey(c)) break;
                node = node.Children[c];
                score += node.Count; // Add the count of words sharing this prefix
            }
            return score;
        }
    }

    public int[] SumPrefixScores(string[] words)
    {
        Trie trie = new Trie();
        int n = words.Length;
        int[] answer = new int[n];

        // Insert all words into the trie
        foreach (string word in words)
        {
            trie.Insert(word);
        }

        // For each word, calculate the sum of prefix scores
        for (int i = 0; i < n; i++)
        {
            answer[i] = trie.GetPrefixScore(words[i]);
        }

        return answer;
    }

}

```
