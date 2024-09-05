# LeetCodeSolutions: 874-Medium-walking-robot-simulation


Solution: https://leetcode.com/problems/walking-robot-simulation/solutions/5736515/optimal-solution-beats-93-7/

Description: https://leetcode.com/problems/walking-robot-simulation/description/

![image.png](https://assets.leetcode.com/users/images/1f367f31-ed8e-4ba2-821f-3d155edb18bf_1725458305.8043625.png)

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem can be broken down into managing the robot's movements in a 2D plane based on a sequence of commands and obstacles. The first thought is to simulate the robot's movement step-by-step, turning and moving based on the commands, while checking for obstacles along the way. The goal is to track the robot's maximum distance from the origin at any point during its journey.

# Approach
<!-- Describe your approach to solving the problem. -->
1. **Direction Management**: The robot has four possible directions to face: North, East, South, and West. We can represent these directions using pairs of (dx, dy) values corresponding to movement in the X and Y axes.

2. **Command Processing**: 
   - For a left turn (`-2`), adjust the current direction counterclockwise.
   - For a right turn (`-1`), adjust the current direction clockwise.
   - For a move command (positive integer), move the robot in the current direction step by step, checking if each move would land on an obstacle.

3. **Obstacle Handling**: Convert the list of obstacles into a set for fast lookups. If a move would cause the robot to land on an obstacle, it stays in its current position for that move.

4. **Distance Calculation**: After each move, calculate the squared Euclidean distance from the origin `(0, 0)` and update the maximum distance recorded.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
  - The time complexity is $$O(n + m)$$, where $$n$$ is the number of commands and $$m$$ is the number of obstacles. Processing each command takes $$O(1)$$ time, and checking for obstacles takes $$O(1)$$ per step due to the set lookup.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
  - The space complexity is $$O(m)$$, where $$m$$ is the number of obstacles stored in a set.


# Code
```csharp []
public class Solution {
   public int RobotSim(int[] commands, int[][] obstacles)
    {
        // Directions are represented as (dx, dy) pairs: North, East, South, West
        int[][] directions = new int[4][] {
            new int[] {0, 1},  // North
            new int[] {1, 0},  // East
            new int[] {0, -1}, // South
            new int[] {-1, 0}  // West
        };

        // Start at origin (0, 0)
        int x = 0, y = 0;
        int directionIndex = 0; // Start facing North (index 0)
        int maxDistanceSquared = 0;

        // Convert obstacles array to a set for fast lookup
        HashSet<(int, int)> obstacleSet = new HashSet<(int, int)>();
        foreach (var obstacle in obstacles)
        {
            obstacleSet.Add((obstacle[0], obstacle[1]));
        }

        // Process each command
        foreach (int command in commands)
        {
            if (command == -2) // Turn left 90 degrees
            {
                directionIndex = (directionIndex + 3) % 4;
            }
            else if (command == -1) // Turn right 90 degrees
            {
                directionIndex = (directionIndex + 1) % 4;
            }
            else // Move forward k units
            {
                int dx = directions[directionIndex][0];
                int dy = directions[directionIndex][1];

                for (int i = 0; i < command; i++)
                {
                    int newX = x + dx;
                    int newY = y + dy;

                    // Check if the new position is an obstacle
                    if (obstacleSet.Contains((newX, newY)))
                    {
                        break; // Stop moving forward if there's an obstacle
                    }

                    x = newX;
                    y = newY;

                    // Update the maximum distance squared from the origin
                    maxDistanceSquared = Math.Max(maxDistanceSquared, x * x + y * y);
                }
            }
        }

        return maxDistanceSquared;
    }
}
```
