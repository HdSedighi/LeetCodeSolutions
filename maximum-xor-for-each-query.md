Solution: https://leetcode.com/problems/maximum-xor-for-each-query/solutions/6023475/optimal-solution/

DEscription: https://leetcode.com/problems/maximum-xor-for-each-query/description/

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem requires us to find a `k` for each query such that it maximizes the XOR of all elements in the array along with `k`. Since XOR flips bits, the best way to maximize it is by XORing with the highest possible value within the specified bit limit. Observing that `nums` is sorted and we need to remove the last element after each query, we can leverage a cumulative XOR to keep track of the array's XOR state without recalculating it from scratch each time.

# Approach
<!-- Describe your approach to solving the problem. -->
1. **Initial XOR Calculation**:
   - Calculate the XOR of all elements in `nums` once at the start, storing it as `cumulativeXOR`. This will serve as our starting XOR value.
2. **Define Maximum k Value**:
   - Compute the maximum possible `k` value using `maximumBit`, which is \(2^{\text{maximumBit}} - 1\). This value, with all bits set within the limit, will ensure we achieve the maximum XOR when combined with the cumulative XOR.
3. **Process Each Query**:
   - For each query (starting from the full array and reducing its size by one element each time):
     - XOR the `cumulativeXOR` with `maxK` to determine the optimal `k` for the current query.
     - Update `cumulativeXOR` by removing the last element of `nums` (using XOR) to prepare for the next query.
4. **Result Storage**:
   - Store each result in an `answer` array in reverse order, so that by the end, it aligns with the query order.

This approach minimizes recalculation, making it efficient and fitting within the problem’s constraints.

# Complexity
- Time complexity:
  $$O(n)$$ - We perform a single pass to calculate the initial cumulative XOR and another pass to process each query, making this linear with respect to `n`.

- Space complexity:
  $$O(n)$$ - The only additional space required is for the `answer` array of size `n`, making space complexity linear as well.


# Code
```csharp []
public class Solution {
    public int[] GetMaximumXor(int[] nums, int maximumBit) {
        int n = nums.Length;
        int[] answer = new int[n];
        
        // Step 1: Calculate the initial XOR of all elements in nums
        int cumulativeXOR = 0;
        foreach (int num in nums) {
            cumulativeXOR ^= num;
        }
        
        // Step 2: Determine the maximum value `k` can have (all bits set for maximumBit)
        int maxK = (1 << maximumBit) - 1;
        
        // Step 3: Process each query from the end to the beginning of nums
        for (int i = 0; i < n; i++) {
            // Find k that maximizes the XOR with the current cumulative XOR
            answer[i] = cumulativeXOR ^ maxK;
            
            // Update the cumulative XOR by removing the last element of the current array
            cumulativeXOR ^= nums[n - 1 - i];
        }
        
        return answer;
    }
}

```
