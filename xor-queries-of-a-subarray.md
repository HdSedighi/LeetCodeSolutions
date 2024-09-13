# LeetCodeSolutions: 1310- medium- xor-queries-of-a-subarray

Solution: https://leetcode.com/problems/xor-queries-of-a-subarray/solutions/5782731/beats-100-easy-solution/
Description: https://leetcode.com/problems/xor-queries-of-a-subarray/description/

![image.png](https://assets.leetcode.com/users/images/39797663-f7b3-4872-a5c6-617c8813c2a5_1726255168.879867.png).

# Intuition
The problem asks for the XOR of elements in a given range multiple times. XOR is a useful operation here because it has properties that make it easy to compute ranges efficiently. Specifically, XOR is both commutative and associative, which means that you can precompute a prefix XOR array. With the prefix XOR, each query can be computed in constant time by taking the XOR of two values from this array. 

This approach avoids the inefficiency of recomputing the XOR for the range from scratch for each query.

# Approach
1. **Prefix XOR Array**: We create an array `prefixXor` where `prefixXor[i]` represents the XOR of all elements from the start of the array up to index `i-1`. This allows us to compute any range XOR efficiently.
   
2. **Range XOR Calculation**: 
   - For each query `[left, right]`, the XOR of elements between `left` and `right` can be obtained as:
     \[
     \text{XOR from left to right} = \text{prefixXor}[right + 1] \oplus \text{prefixXor}[left]
     \]
   This is because XOR-ing the prefix up to `right + 1` removes the contribution of the elements before `left`.

3. **Efficiency**: This approach allows us to precompute the XOR in linear time, and then each query is answered in constant time by leveraging the prefix XOR array.

# Complexity
- Time complexity:
  - Precomputing the `prefixXor` array takes O(n), where n is the length of the input array.
  - Each query is processed in O(1) time, so for `q` queries, it takes O(q).
  - Overall time complexity: $$O(n + q)$$

- Space complexity:
  - We use an additional array `prefixXor` of size n+1 to store the XOR results.
  - Therefore, the space complexity is $$O(n)$$.


# Code
```csharp []
public class Solution {
    public int[] XorQueries(int[] arr, int[][] queries) {
        int n = arr.Length;
        int[] prefixXor = new int[n + 1]; // prefixXor[i] will store XOR of arr[0] to arr[i-1]

        // Compute the prefix XOR array
        for (int i = 1; i <= n; i++) {
            prefixXor[i] = prefixXor[i - 1] ^ arr[i - 1];
        }

        int[] result = new int[queries.Length];

        // Process each query
        for (int i = 0; i < queries.Length; i++) {
            int left = queries[i][0];
            int right = queries[i][1];

            // XOR of elements from arr[left] to arr[right] is:
            // prefixXor[right+1] ^ prefixXor[left]
            result[i] = prefixXor[right + 1] ^ prefixXor[left];
        }

        return result;
    }
}
```
