Solution: https://leetcode.com/problems/count-the-number-of-fair-pairs/solutions/6042445/optimal-solution/

Description: https://leetcode.com/problems/count-the-number-of-fair-pairs/description/

# Intuition
The problem requires counting pairs `(i, j)` where `i < j` and the sum of `nums[i] + nums[j]` lies within a specified range `[lower, upper]`. A brute-force approach would be too slow for large inputs, as it would involve checking all possible pairs, which has a time complexity of \(O(n^2)\).

The first insight to optimize the solution is to **sort the array**. Once sorted, we can leverage two-pointer or binary search techniques to quickly find the count of valid pairs for each element in the array. This reduces the problem to a series of range queries within the sorted list.

# Approach
1. **Sorting the Array**: Start by sorting `nums` in ascending order. This allows us to efficiently find valid pairs that satisfy the sum range `[lower, upper]`.
  
2. **Binary Search for Bounds**:
   - For each element `nums[i]`, use binary search to find:
     - The smallest index `low` such that `nums[i] + nums[low] >= lower`.
     - The largest index `high` such that `nums[i] + nums[high] <= upper`.
   - This can be efficiently done using two helper functions: `LowerBound` and `UpperBound`, which use binary search to find the first and last valid positions, respectively.

3. **Counting Valid Pairs**: For each valid `i`, the count of pairs `(i, j)` that satisfy the conditions is `high - low + 1`, which is accumulated in a running total, `fairPairs`.

4. **Binary Search Helper Functions**:
   - `LowerBound` finds the smallest index such that `nums[i] + nums[j] >= lower`.
   - `UpperBound` finds the largest index such that `nums[i] + nums[j] <= upper`.

# Complexity
- **Time complexity**: \(O(n \log n)\)
  - Sorting the array takes \(O(n \log n)\).
  - For each element in `nums`, we perform two binary searches, each taking \(O(\log n)\).
  - Therefore, the overall time complexity is \(O(n \log n)\).

- **Space complexity**: \(O(1)\) (excluding the input array if sorted in place)
  - No extra data structures are used beyond a few variables and helper functions.


# Code
```csharp []
public class Solution
{
    public long CountFairPairs(int[] nums, int lower, int upper)
    {
        Array.Sort(nums);
        int n = nums.Length;
        long fairPairs = 0;

        for (int i = 0; i < n - 1; i++)
        {
            // Use binary search to find the smallest index `low` such that nums[i] + nums[low] >= lower
            int low = LowerBound(nums, i + 1, n - 1, lower - nums[i]);

            // Use binary search to find the largest index `high` such that nums[i] + nums[high] <= upper
            int high = UpperBound(nums, i + 1, n - 1, upper - nums[i]);

            if (low != -1 && high != -1 && low <= high)
            {
                fairPairs += (high - low + 1);
            }
        }

        return fairPairs;
    }

    private int LowerBound(int[] nums, int left, int right, int target)
    {
        while (left <= right)
        {
            int mid = left + (right - left) / 2;
            if (nums[mid] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }
        return left;
    }

    private int UpperBound(int[] nums, int left, int right, int target)
    {
        while (left <= right)
        {
            int mid = left + (right - left) / 2;
            if (nums[mid] <= target)
                left = mid + 1;
            else
                right = mid - 1;
        }
        return right;
    }
}

```
