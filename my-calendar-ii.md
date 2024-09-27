Solution: https://leetcode.com/problems/my-calendar-ii/solutions/5841302/beats-90-optimal-solution/

Descroption: https://leetcode.com/problems/my-calendar-ii/description/

![image.png](https://assets.leetcode.com/users/images/196eb2be-4913-46db-ba8c-95c0450b91bd_1727468552.7050464.png)

# Intuition
The problem requires us to add events to a calendar while ensuring that no time period is triple-booked. My first thought was to use an approach where we keep track of all the bookings and check for conflicts each time we add a new event. If the new event overlaps with two existing bookings, it would cause a triple booking, so we need to avoid this.

To solve this problem efficiently, we can maintain two lists:
- One list (`bookings`) to store all the individual bookings.
- Another list (`doubleBookings`) to store the overlapping portions of events that are already double-booked.

By keeping track of these two lists, we can determine whether adding a new event would cause a triple booking.

# Approach
The approach involves two key lists:
1. **Bookings List**: This list keeps track of all the booked events.
2. **Double Bookings List**: This list tracks the intervals where two bookings overlap.

For each new event, the process is as follows:
1. Iterate over the intervals in `doubleBookings`. If the new event overlaps with any interval in `doubleBookings`, then adding this event would lead to a triple booking, and we should return `false`.
2. If no triple booking would occur, iterate over the intervals in `bookings` and check if there is an overlap between the new event and the existing booking. If an overlap exists, add the overlapping interval to the `doubleBookings` list.
3. Finally, add the new event to the `bookings` list.

By using two lists, we ensure that we only add events if they do not cause any triple bookings.

# Complexity
- Time complexity:
  - Each booking operation iterates over the `bookings` and `doubleBookings` lists, resulting in a time complexity of $$O(n)$$, where $$n$$ is the number of previously booked events.
  
- Space complexity:
  - The space complexity is also $$O(n)$$, as we maintain two lists (`bookings` and `doubleBookings`) that store up to `n` intervals.


# Code
```csharp []
public class MyCalendarTwo {

    private List<int[]> bookings;
    private List<int[]> doubleBookings;

    public MyCalendarTwo()
    {
        bookings = new List<int[]>();
        doubleBookings = new List<int[]>();
    }

    public bool Book(int start, int end)
    {
        // Check if the new event would cause a triple booking
        foreach (var db in doubleBookings)
        {
            if (Math.Max(db[0], start) < Math.Min(db[1], end))
            {
                return false; // Triple booking would occur
            }
        }

        // Add overlapping intervals to the double bookings list
        foreach (var booking in bookings)
        {
            int overlapStart = Math.Max(booking[0], start);
            int overlapEnd = Math.Min(booking[1], end);
            if (overlapStart < overlapEnd)
            {
                doubleBookings.Add(new int[] { overlapStart, overlapEnd });
            }
        }

        // Add the new booking to the bookings list
        bookings.Add(new int[] { start, end });
        return true;
    }
}

/**
 * Your MyCalendarTwo object will be instantiated and called as such:
 * MyCalendarTwo obj = new MyCalendarTwo();
 * bool param_1 = obj.Book(start,end);
 */
```
