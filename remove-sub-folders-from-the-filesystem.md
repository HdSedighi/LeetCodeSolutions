Solution: https://leetcode.com/problems/remove-sub-folders-from-the-filesystem/solutions/5968655/optimal-solution/

Description: https://leetcode.com/problems/remove-sub-folders-from-the-filesystem/description/

# Intuition
The key to solving this problem is to identify sub-folder relationships between folder paths. If a folder is sorted lexicographically, all its sub-folders will appear directly after it in sorted order. Thus, by iterating through the sorted list, we can easily skip over sub-folders by checking if a folder path starts with the previous folder path followed by a `"/"`. This allows us to efficiently remove sub-folders while preserving top-level folders.

# Approach
1. **Sort the List**: Sort the `folder` list lexicographically. This sorting ensures that each folder's sub-folders (if any) will immediately follow it in the list.
  
2. **Identify and Skip Sub-folders**: Iterate through each folder path in the sorted list. For each path:
   - Check if it starts with the previous folder path plus a `"/"`. If it does, it is a sub-folder and can be skipped.
   - Otherwise, add the folder to the result list, marking it as a top-level folder, and set it as the new "previous" folder for future comparisons.
  
3. **Return the Result**: At the end of the iteration, the result list contains only top-level folders, with all sub-folders removed.

# Complexity
- **Time complexity**:  
  Sorting the list of folders takes \(O(n \log n)\), where \(n\) is the number of folder paths. The single pass through the sorted list takes \(O(n)\), so the overall time complexity is \(O(n \log n + n) = O(n \log n)\).

- **Space complexity**:  
  The space complexity is \(O(n)\), where \(n\) is the size of the result list, as we store all top-level folders in the output list.


# Code
```csharp []
public class Solution {
    public IList<string> RemoveSubfolders(string[] folder) {
        Array.Sort(folder);
        List<string> result = new List<string>();

        string prev = "";
        foreach (var path in folder) {
            if (prev == "" || !path.StartsWith(prev + "/")) {
                result.Add(path);
                prev = path;
            }
        }

        return result;
    }
}
```
