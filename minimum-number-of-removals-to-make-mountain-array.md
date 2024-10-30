Solution: https://leetcode.com/problems/minimum-number-of-removals-to-make-mountain-array/solutions/5986631/optimal-solution/

Description: https://leetcode.com/problems/minimum-number-of-removals-to-make-mountain-array/description/

# Intuition
To make an array a mountain array, we need to find an increasing subsequence followed by a decreasing subsequence with a peak element in between. The key to solving this problem efficiently is recognizing that we only need to make modifications around the peak element, as long as we ensure that both the left and right sides of the peak are valid increasing and decreasing subsequences, respectively. This leads us to think of using dynamic programming to calculate the longest increasing subsequence (LIS) up to each index and the longest decreasing subsequence (LDS) from each index.

# Approach
1. **Define LIS and LDS Arrays**: 
   - Use two arrays, `left` and `right`, where:
     - `left[i]` represents the length of the longest increasing subsequence that ends at `i`.
     - `right[i]` represents the length of the longest decreasing subsequence that starts at `i`.
   
2. **Calculate Longest Increasing Subsequences (`left` Array)**:
   - Traverse from left to right and for each `i`, find the longest increasing subsequence that ends at that index. Update `left[i]` based on previous LIS values up to `i`.

3. **Calculate Longest Decreasing Subsequences (`right` Array)**:
   - Traverse from right to left and for each `i`, find the longest decreasing subsequence that starts at that index. Update `right[i]` based on previous LDS values starting from `i`.
   
4. **Find the Minimum Removals**:
   - For each possible peak element (`1 <= i <= n-2`), check if it forms a valid mountain array, i.e., `left[i] > 1` and `right[i] > 1`. Calculate the combined length of LIS and LDS at `i`, and subtract from the total length of the array to get the number of removals required. Keep track of the minimum removals.

5. **Return the Minimum Removals**.

# Complexity
- **Time complexity**: 
  - The time complexity is \(O(n^2)\) because, for each element, we may need to traverse up to `n` elements to compute LIS and LDS, resulting in quadratic complexity.
  
- **Space complexity**:
  - The space complexity is \(O(n)\), as we only need two arrays of length `n` to store LIS and LDS values.



# Code
```csharp []
public class Solution
{
    public int MinimumMountainRemovals(int[] nums)
    {
        int n = nums.Length;
        int[] left = new int[n];
        int[] right = new int[n];

        // Fill left array with longest increasing subsequence lengths
        for (int i = 0; i < n; i++)
        {
            left[i] = 1;
            for (int j = 0; j < i; j++)
            {
                if (nums[j] < nums[i])
                {
                    left[i] = Math.Max(left[i], left[j] + 1);
                }
            }
        }

        // Fill right array with longest decreasing subsequence lengths
        for (int i = n - 1; i >= 0; i--)
        {
            right[i] = 1;
            for (int j = n - 1; j > i; j--)
            {
                if (nums[j] < nums[i])
                {
                    right[i] = Math.Max(right[i], right[j] + 1);
                }
            }
        }

        int minRemovals = int.MaxValue;

        // Calculate minimum removals needed to make nums a mountain array
        for (int i = 1; i < n - 1; i++)
        {
            // A valid peak must have both left[i] > 1 and right[i] > 1
            if (left[i] > 1 && right[i] > 1)
            {
                int currentLength = left[i] + right[i] - 1;
                minRemovals = Math.Min(minRemovals, n - currentLength);
            }
        }

        return minRemovals;
    }
}

```
