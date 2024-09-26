Solution: https://leetcode.com/problems/my-calendar-i/solutions/5836513/optimal-solution/

Description: https://leetcode.com/problems/my-calendar-i/description/

# Intuition
When considering how to manage a calendar and prevent double bookings, my first thought was to store the booked events in a data structure that allows efficient checks for overlaps. Given that events are defined by start and end times, the challenge is to ensure that any new event being booked does not intersect with existing ones. The half-open interval [start, end) allows for clear rules on how to identify overlaps.

# Approach
To solve this problem, I decided to use a list to store the booked events. When a new event is requested, the program iterates through the existing events to check for any overlaps. The key condition for two events `(start1, end1)` and `(start2, end2)` to overlap is:
- `max(start1, start2) < min(end1, end2)`

This condition ensures that there is some common time between the two events. If an overlap is detected, the method returns `false`; otherwise, it adds the new event to the list and returns `true`.

This simple yet effective approach allows for straightforward implementation and efficient checks.

# Complexity
- Time complexity: $$O(n)$$  
  Each booking requires checking against all existing events, which takes linear time in the worst case, where `n` is the number of booked events.

- Space complexity: $$O(n)$$  
  In the worst case, all booked events are stored in the list, leading to linear space usage relative to the number of events.


# Code
```csharp []
using System;
using System.Collections.Generic;

public class MyCalendar
{
    private List<(int start, int end)> events;

    public MyCalendar()
    {
        events = new List<(int start, int end)>();
    }

    public bool Book(int start, int end)
    {
        // Check for overlapping events
        foreach (var evt in events)
        {
            // If the new event overlaps with an existing event, return false
            if (Math.Max(start, evt.start) < Math.Min(end, evt.end))
            {
                return false;
            }
        }
        
        // If no overlap, add the event and return true
        events.Add((start, end));
        return true;
    }
}

```
