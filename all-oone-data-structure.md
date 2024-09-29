Solution: https://leetcode.com/problems/all-oone-data-structure/solutions/5848408/optimal-solution/

Description: https://leetcode.com/problems/all-oone-data-structure/description/

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The initial thought was to use data structures that efficiently maintain the count of each key while also allowing easy retrieval of both the minimum and maximum counts. The problem required a solution where each operation (increment, decrement, get min/max key) could be performed in constant or logarithmic time. This led to considering a combination of a hash map for count tracking and an ordered set for efficiently finding min and max keys.

# Approach
<!-- Describe your approach to solving the problem. -->
The approach uses two main data structures:
1. A dictionary (`count`) to store the count of each string key, which allows constant-time access and update of counts.
2. A sorted set (`set`) to keep track of the keys and their counts in a way that maintains the ordering of counts.

The operations are handled as follows:
- **Increment (`inc`)**: We first remove the old count entry from the sorted set, update the count in the dictionary, and then add the new count entry back to the set. This ensures that the set always has the latest count for each key.
- **Decrement (`dec`)**: Similarly, we remove the old count entry, decrement the count, and if the count is greater than zero, add the updated entry back to the set. If the count reaches zero, the key is removed from the dictionary.
- **Get Max/Min Key**: Since the sorted set keeps the entries ordered by count, retrieving the maximum or minimum key is simply a matter of accessing the last or first element of the set, respectively.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
  - **Increment (`inc`)**: $$O(\log n)$$ due to operations on the sorted set.
  - **Decrement (`dec`)**: $$O(\log n)$$ due to operations on the sorted set.
  - **Get Max/Min Key (`getMaxKey`/`getMinKey`)**: $$O(1)$$ since accessing the first or last element of the sorted set is constant time.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
  - **Space Complexity**: $$O(n)$$ where $$n$$ is the number of unique keys in the data structure. This is due to storing the counts in both the dictionary and the sorted set.


# Code
```csharp []
using System;
using System.Collections.Generic;

public class AllOne
{
    private Dictionary<string, int> count; // Stores the count of each key
    private SortedSet<(int Count, string Key)> set; // Sorted set to keep counts and keys

    public AllOne()
    {
        count = new Dictionary<string, int>();
        set = new SortedSet<(int, string)>();
    }

    // Increment the count of the key
    public void Inc(string key)
    {
        int n = count.ContainsKey(key) ? count[key] : 0; // Get current count
        count[key] = n + 1; // Increment the count

        set.Remove((n, key)); // Remove the old pair from set
        set.Add((n + 1, key)); // Insert the new pair with updated count
    }

    // Decrement the count of the key
    public void Dec(string key)
    {
        if (count.ContainsKey(key))
        {
            int n = count[key]; // Get current count
            set.Remove((n, key)); // Remove the old pair from set

            if (n - 1 > 0)
            {
                count[key] = n - 1; // Decrement the count
                set.Add((n - 1, key)); // Insert updated pair if count > 0
            }
            else
            {
                count.Remove(key); // Remove the key from map if count reaches 0
            }
        }
    }

    // Get the key with the maximum count
    public string GetMaxKey()
    {
        if (set.Count > 0)
        {
            return set.Max.Key; // Last element gives the maximum
        }
        return "";
    }

    // Get the key with the minimum count
    public string GetMinKey()
    {
        if (set.Count > 0)
        {
            return set.Min.Key; // First element gives the minimum
        }
        return "";
    }
}
```
