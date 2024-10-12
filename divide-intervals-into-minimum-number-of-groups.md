Solution: https://leetcode.com/problems/divide-intervals-into-minimum-number-of-groups/solutions/5903494/optimal-solution/

DEscription: https://leetcode.com/problems/divide-intervals-into-minimum-number-of-groups/description/

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem asks us to group intervals such that no two intervals in the same group overlap. The key idea is to realize that the number of groups required depends on the maximum number of overlapping intervals at any point in time. If multiple intervals overlap, they need to be placed in separate groups. To track these overlaps, we can treat the interval endpoints as events and count how many intervals are active (overlapping) at any given time.

# Approach
<!-- Describe your approach to solving the problem. -->
1. **Event-based approach**: 
   - For each interval, treat the start as a `+1` event and the end as a `-1` event. The number of overlapping intervals at any time is the sum of these events.
   - Specifically, we add a start event for the beginning of each interval and an end event for one unit past the end of the interval to ensure the boundary condition (e.g., [1,5] and [5,8] intersect at 5).
   
2. **Sorting events**: 
   - Sort the events by time. In case of a tie (i.e., two events happen at the same time), prioritize the end event (`-1`) over the start event (`+1`) to avoid falsely counting two intervals as overlapping when they only share a boundary.

3. **Counting the maximum overlap**: 
   - Traverse through the sorted events and maintain a running count of active intervals. Track the maximum number of simultaneous active intervals, as this will represent the minimum number of groups required.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
  - Sorting the events takes \(O(n \log n)\), where \(n\) is the number of intervals.
  - Traversing the sorted list of events takes \(O(n)\).
  - Therefore, the overall time complexity is \(O(n \log n)\).

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
  - We use an additional list to store the events, which has \(2n\) elements since each interval contributes two events (start and end). Thus, the space complexity is \(O(n)\).


# Code
```csharp []
using System;
using System.Collections.Generic;

public class Solution
{
    public int MinGroups(int[][] intervals)
    {
        // List to hold both start and end points as events
        List<(int time, int type)> events = new List<(int time, int type)>();

        // Fill the events list with start and end points
        foreach (var interval in intervals)
        {
            events.Add((interval[0], 1));  // Start of interval (marked as +1)
            events.Add((interval[1] + 1, -1));  // End of interval (marked as -1)
        }

        // Sort events based on time; if two events have the same time, prioritize the 'end' (-1) event
        events.Sort((a, b) =>
        {
            if (a.time == b.time)
                return a.type.CompareTo(b.type);  // Sort by type if times are equal
            return a.time.CompareTo(b.time);  // Otherwise, sort by time
        });

        int maxGroups = 0;
        int currentGroups = 0;

        // Traverse through the events to find the maximum overlap
        foreach (var ev in events)
        {
            currentGroups += ev.type;  // Add 1 for a start, subtract 1 for an end
            maxGroups = Math.Max(maxGroups, currentGroups);  // Track the maximum number of overlaps
        }

        return maxGroups;  // The maximum number of overlaps is the minimum number of groups needed
    }
}

```
