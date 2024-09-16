

solution: https://leetcode.com/problems/minimum-time-difference/solutions/5794852/easy-solution/

description:https://leetcode.com/problems/minimum-time-difference/description/

# Intuition
The problem asks for the minimum time difference between any two time points in a 24-hour format. My first thought was that since time is cyclical (i.e., it wraps around from "23:59" back to "00:00"), sorting the time points will allow us to easily compute the differences between adjacent times. Additionally, we need to handle the edge case of the wraparound, where the last time in the day should be compared to the first.

# Approach
1. **Convert time points to minutes**: Each time point in "HH:MM" format can be converted to the total number of minutes since midnight (i.e., "00:00" is 0, "23:59" is 1439).
2. **Sort the list**: Sorting the list of time points (in minutes) ensures that we can easily calculate the difference between adjacent time points.
3. **Compute minimum differences**: Iterate over the sorted list, calculating the difference between each pair of adjacent time points. Also, consider the wraparound difference (i.e., the difference between the last time point and the first, accounting for the 24-hour cycle).
4. **Return the minimum difference**: Track the smallest difference during the iteration and return it.

# Complexity
- Time complexity:
    The time complexity is $$O(n \log n)$$ where $$n$$ is the number of time points. This comes from the sorting step, which dominates the overall time complexity.

- Space complexity:
    The space complexity is $$O(n)$$, where $$n$$ is the number of time points. We need additional space to store the converted time points in minutes.


# Code
```csharp []
public class Solution {
   public int FindMinDifference(IList<string> timePoints) {
        // List to store the time in minutes
        List<int> minutes = new List<int>();

        // Convert each time point to minutes and add to the list
        foreach (var time in timePoints) {
            string[] parts = time.Split(':');
            int hour = int.Parse(parts[0]);
            int minute = int.Parse(parts[1]);
            int totalMinutes = hour * 60 + minute;
            minutes.Add(totalMinutes);
        }

        // Sort the list of times in minutes
        minutes.Sort();

        // Initialize the minimum difference to a large value
        int minDiff = int.MaxValue;

        // Calculate the difference between adjacent times
        for (int i = 1; i < minutes.Count; i++) {
            minDiff = Math.Min(minDiff, minutes[i] - minutes[i - 1]);
        }

        // Special case: difference between the last and first time, considering the clock wraparound
        minDiff = Math.Min(minDiff, (1440 - minutes[minutes.Count - 1] + minutes[0]));

        return minDiff;
    }
}
```
