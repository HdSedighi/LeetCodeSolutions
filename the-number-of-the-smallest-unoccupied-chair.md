Solution: https://leetcode.com/problems/the-number-of-the-smallest-unoccupied-chair/solutions/5900226/optimal-solution/

Description: https://leetcode.com/problems/the-number-of-the-smallest-unoccupied-chair/description/

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The main challenge is efficiently assigning friends to the smallest available chair when they arrive and managing chair availability when they leave. Since arrivals and departures happen at specific times, we need to simulate the process in the correct sequence. A priority queue (or sorted set) can be used to manage the smallest available chair, and sorting the events by time ensures friends sit in the correct order.

# Approach
<!-- Describe your approach to solving the problem. -->
1. **Event List Creation**: For each friend, we create two events: one for their arrival and one for their departure. Each event records the time, the friend index, and whether it's an arrival or departure event.
2. **Sort Events**: We sort all the events by time, prioritizing arrivals over departures if two events happen at the same time.
3. **Manage Chairs**: Use a `SortedSet<int>` to manage the available chairs. This allows us to always pick the smallest unoccupied chair efficiently. When a friend arrives, they sit in the smallest available chair, and when they leave, their chair becomes available again.
4. **Track Target Friend**: As we process each event, we track the chair the target friend sits on and return the chair number when they arrive.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
  Sorting the events takes \(O(n \log n)\), where \(n\) is the number of friends. Each insertion and removal operation in the `SortedSet` takes \(O(\log n)\). Therefore, the overall time complexity is \(O(n \log n)\).

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
  We need \(O(n)\) space to store the event list and chair assignments for each friend. Hence, the space complexity is \(O(n)\).


# Code
```csharp []
using System;
using System.Collections.Generic;

public class Solution
{
    public int SmallestChair(int[][] times, int targetFriend)
    {
        int n = times.Length;
        
        // Create a list of all events (arrival and leaving) and a mapping to friend index
        List<(int time, int friendIndex, bool isArrival)> events = new List<(int, int, bool)>();
        for (int i = 0; i < n; i++)
        {
            events.Add((times[i][0], i, true));  // Arrival event
            events.Add((times[i][1], i, false)); // Leaving event
        }
        
        // Sort events by time (if two events have the same time, handle arrival before departure)
        events.Sort((a, b) => a.time == b.time ? a.isArrival.CompareTo(b.isArrival) : a.time.CompareTo(b.time));
        
        // Min-heap for available chairs
        SortedSet<int> availableChairs = new SortedSet<int>();
        for (int i = 0; i < n; i++)
            availableChairs.Add(i);  // Initially, chairs 0 to n-1 are available
        
        // Array to store which chair each friend sits on
        int[] friendToChair = new int[n];
        
        foreach (var e in events)
        {
            int time = e.time;
            int friendIndex = e.friendIndex;
            bool isArrival = e.isArrival;
            
            if (isArrival)
            {
                // Friend arrives, take the smallest available chair
                int chair = availableChairs.Min;
                availableChairs.Remove(chair);
                friendToChair[friendIndex] = chair;
                
                // If this is the target friend, return their chair number
                if (friendIndex == targetFriend)
                    return chair;
            }
            else
            {
                // Friend leaves, return their chair to the available set
                availableChairs.Add(friendToChair[friendIndex]);
            }
        }
        
        return -1;  // Should never reach here
    }
}

```
