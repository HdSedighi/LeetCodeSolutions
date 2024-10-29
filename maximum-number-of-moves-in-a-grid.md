Solution: https://leetcode.com/problems/maximum-number-of-moves-in-a-grid/solutions/5982879/optimal-solution/

Description: https://leetcode.com/problems/maximum-number-of-moves-in-a-grid/description/

# Intuition
To solve this problem, we observe that for each cell in the grid, we need to check possible moves to neighboring cells in the next column. Since moves can only be made to cells with strictly greater values, we can employ a **dynamic programming** approach to store the maximum moves possible starting from each cell. This way, we avoid redundant calculations and ensure that the solution is optimized.

# Approach
1. **Define DP State**: Let `dp[i][j]` represent the maximum number of moves starting from cell `(i, j)` in the matrix.
2. **Initialization**: Set all cells in the first column to `0` since no moves have been made yet at the start.
3. **Transitions**:
   - For each cell `(i, j)`, try to move to any of the cells `(i - 1, j + 1)`, `(i, j + 1)`, or `(i + 1, j + 1)`.
   - Only move to a cell if it has a strictly larger value than the current cell.
   - Update `dp[i][j]` as `1 + dp[newRow][newCol]` for valid moves.
4. **Compute the Answer**: The result is the maximum value of `dp[i][0]` over all rows `i`, as we are allowed to start from any cell in the first column.

# Complexity
- **Time Complexity**: \(O(m \times n)\), where \(m\) is the number of rows and \(n\) is the number of columns. Each cell is visited once, and transitions are handled in constant time.
  
- **Space Complexity**: \(O(m \times n)\) for the DP table to store results of subproblems for each cell in the grid.


# Code
```csharp []
public class Solution {
    public int MaxMoves(int[][] grid) {
        int m = grid.Length;
        int n = grid[0].Length;
        int[][] dp = new int[m][];
        
        // Initialize the dp array
        for (int i = 0; i < m; i++) {
            dp[i] = new int[n];
            Array.Fill(dp[i], -1);
        }
        
        int maxMoves = 0;
        
        // Try starting from each cell in the first column
        for (int i = 0; i < m; i++) {
            maxMoves = Math.Max(maxMoves, DFS(grid, dp, i, 0));
        }
        
        return maxMoves;
    }
    
    private int DFS(int[][] grid, int[][] dp, int row, int col) {
        // Check if the position is valid
        if (row < 0 || row >= grid.Length || col >= grid[0].Length) return 0;
        
        // Return precomputed result
        if (dp[row][col] != -1) return dp[row][col];
        
        int maxMoves = 0;
        
        // List of possible moves
        int[] dRow = {-1, 0, 1};
        int[] dCol = {1, 1, 1};
        
        for (int i = 0; i < 3; i++) {
            int newRow = row + dRow[i];
            int newCol = col + dCol[i];
            
            if (newRow >= 0 && newRow < grid.Length && newCol < grid[0].Length && grid[newRow][newCol] > grid[row][col]) {
                maxMoves = Math.Max(maxMoves, 1 + DFS(grid, dp, newRow, newCol));
            }
        }
        
        dp[row][col] = maxMoves;
        return maxMoves;
    }
}
```
