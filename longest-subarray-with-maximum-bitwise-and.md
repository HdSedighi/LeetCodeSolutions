# LeetCodeSolutions: 2419-longest-subarray-with-maximum-bitwise-and


Solution: https://leetcode.com/problems/longest-subarray-with-maximum-bitwise-and/solutions/5786143/beats-100-easy-solution/

Description: https://leetcode.com/problems/longest-subarray-with-maximum-bitwise-and/description/

![image.png](https://assets.leetcode.com/users/images/daa5429c-040c-4e55-a63c-e92182fa86f7_1726322797.4997776.png)

# Intuition
The problem asks to find the longest subarray where the bitwise AND of all elements is the maximum possible value. My first thought is that the bitwise AND of a subarray will always be smaller than or equal to the largest element in the array. Therefore, we can simplify the problem by finding the maximum value in the array and then determining the longest contiguous subarray consisting of that maximum value.

# Approach
1. **Find the maximum element in the array:**  
   Since the bitwise AND of any subarray cannot be greater than the largest element in the array, we first determine the maximum value, `maxVal`.

2. **Traverse the array to find the longest subarray of `maxVal`:**  
   After identifying `maxVal`, we iterate through the array to find the longest contiguous subarray where all elements are equal to `maxVal`. We reset the count whenever we encounter an element that is not equal to `maxVal`, and update the maximum length as we traverse.

3. **Return the maximum length of such subarrays.**

# Complexity
- Time complexity:  
  The solution involves a single pass to find the maximum value and another pass to determine the longest subarray of `maxVal`, making the time complexity $$O(n)$$, where `n` is the length of the array.

- Space complexity:  
  The space complexity is $$O(1)$$ because we are only using a few extra variables for tracking the maximum value, current subarray length, and maximum length.

# Code
```csharp []
public class Solution {
    public int LongestSubarray(int[] nums) {
        int maxVal = 0;
        
        // Step 1: Find the maximum value in the array
        foreach (var num in nums)
        {
            if (num > maxVal)
            {
                maxVal = num;
            }
        }
        
        // Step 2: Find the longest subarray with elements equal to the maximum value
        int maxLength = 0;
        int currentLength = 0;

        foreach (var num in nums)
        {
            if (num == maxVal)
            {
                currentLength++;
                maxLength = Math.Max(maxLength, currentLength);
            }
            else
            {
                currentLength = 0;
            }
        }

        return maxLength;
    }
}
```
