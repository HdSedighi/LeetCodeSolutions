# LeetCodeSolutions: 2220-easy-minimum-bit-flips-to-convert-number


Solution: https://leetcode.com/problems/minimum-bit-flips-to-convert-number/solutions/5771368/easy-solution/

Description: https://leetcode.com/problems/minimum-bit-flips-to-convert-number/description/

# Intuition
The problem asks for the minimum number of bit flips required to convert one integer into another. My first thought was that we can directly compare the binary representations of the two numbers and count how many bits differ between them. This can be done efficiently using the XOR operation, as it highlights the bits that differ between the two numbers by producing a `1` where the bits differ and `0` where they are the same. We can then simply count the number of `1`s in the result to determine how many bit flips are needed.

# Approach
1. Perform the XOR operation between `start` and `goal`. The result will have `1` in every position where the bits of `start` and `goal` differ.
2. Count the number of `1`s in the result, as this gives the number of bit flips required to convert `start` to `goal`.
3. To count the `1`s, we can use a loop where we check the least significant bit (using `xor & 1`) and right-shift the `xor` result until all bits have been processed.

# Complexity
- Time complexity:  
  The time complexity is $$O(b)$$, where $$b$$ is the number of bits in the binary representation of the larger number (which is constant for integers, typically up to 32 bits). In the worst case, we perform a constant number of operations proportional to the bit length, so this is essentially $$O(1)$$ for fixed-size integers.

- Space complexity:  
  The space complexity is $$O(1)$$ because we only use a few variables to store intermediate values like the XOR result and the count of differing bits.


# Code
```csharp []
public class Solution {
    public int MinBitFlips(int start, int goal) {
        // XOR of start and goal will give us the bits that are different
        int xor = start ^ goal;
        
        // Count the number of 1's in the binary representation of xor
        int count = 0;
        
        while (xor > 0)
        {
            // Increment count if the last bit is 1
            count += xor & 1;
            
            // Right shift xor to check the next bit
            xor >>= 1;
        }
        
        return count;
    }
}
```
