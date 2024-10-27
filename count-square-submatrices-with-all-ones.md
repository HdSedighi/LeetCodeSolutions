Solution: https://leetcode.com/problems/count-square-submatrices-with-all-ones/solutions/5974960/optimal-solution/

Description: https://leetcode.com/problems/count-square-submatrices-with-all-ones/description/

# Counting Square Submatrices with All Ones

## Intuition
To count all square submatrices of ones in a given matrix, my first thought was to identify that any square submatrix is defined by its bottom-right corner and the number of ones surrounding it in all directions. If we know the size of the largest square that can end at a certain cell `(i, j)`, we can use that information to determine the number of squares for that cell and then sum up these squares across the matrix.

## Approach
We can use dynamic programming to solve this problem efficiently by building a `dp` table where `dp[i][j]` represents the size of the largest square submatrix with all ones that ends at cell `(i, j)`. 

1. **Initialize DP Table**: Create a 2D array `dp` of the same size as the matrix, where each entry initially contains zero.
2. **Fill DP Table**: For each cell `(i, j)`:
   - If `matrix[i][j]` is 1, calculate the size of the largest square ending at that cell by taking the minimum value of the squares ending at `(i-1, j)`, `(i, j-1)`, and `(i-1, j-1)`, and then add 1.
   - If `matrix[i][j]` is 0, the square size ending at `(i, j)` remains zero.
3. **Count Squares**: The value in each cell of `dp` represents the size of the square submatrices ending at that cell, so summing all values in `dp` gives the total count of square submatrices.

This approach leverages overlapping subproblems, where the solution to each cell depends on its neighbors, to compute the result in a single pass through the matrix.

## Complexity

- **Time Complexity**: 
  The time complexity is \(O(m \times n)\), where \(m\) is the number of rows and \(n\) is the number of columns, as we iterate over each cell in the matrix once and perform constant-time calculations.

- **Space Complexity**: 
  The space complexity is \(O(m \times n)\) because we use a 2D array `dp` of the same size as the matrix to store intermediate results.


# Code
```csharp []
public class Solution {
    public int CountSquares(int[][] matrix) {
        int rows = matrix.Length;
        int cols = matrix[0].Length;
        int totalSquares = 0;

        // Create a 2D dp array to store the size of largest square sub-matrix ending at (i, j)
        int[,] dp = new int[rows, cols];

        // Iterate through the matrix
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (matrix[i][j] == 1) {
                    if (i == 0 || j == 0) {
                        // If it's in the first row or first column, it can only be a 1x1 square
                        dp[i, j] = 1;
                    } else {
                        // Otherwise, calculate the size of the square ending at (i, j)
                        dp[i, j] = Math.Min(dp[i - 1, j], Math.Min(dp[i, j - 1], dp[i - 1, j - 1])) + 1;
                    }
                    // Add the size of the square ending at (i, j) to the total count
                    totalSquares += dp[i, j];
                }
            }
        }

        return totalSquares;
    }
}

```
