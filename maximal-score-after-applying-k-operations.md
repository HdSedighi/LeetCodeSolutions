Solution: https://leetcode.com/problems/maximal-score-after-applying-k-operations/solutions/5911647/optimal-solution/

Description: https://leetcode.com/problems/maximal-score-after-applying-k-operations/description/


# Intuition
The problem involves maximizing the score by repeatedly selecting the largest element from the array and applying a modification (dividing by 3 and taking the ceiling). This hints towards an approach where we always need access to the largest element efficiently, making a max-heap (or priority queue) the ideal data structure. Each time we pick the largest element, we add it to our score and modify it, then insert the modified value back into the heap. This process is repeated exactly `k` times.

# Approach
1. Use a max-heap (priority queue) to always access the largest element efficiently.
2. Initially, insert all elements of the `nums` array into the heap.
3. For each of the `k` operations:
   - Extract the maximum element from the heap.
   - Add this element to the score.
   - Compute the new value by dividing the element by 3 and taking the ceiling.
   - Insert the modified value back into the heap.
4. After performing `k` operations, the accumulated score is the result.

# Complexity
- Time complexity:
  - Inserting elements into the heap takes \(O(n \log n)\).
  - For each of the `k` operations, extracting the maximum element and reinserting a modified value takes \(O(\log n)\).
  - Thus, the overall time complexity is \(O(n \log n + k \log n)\), which simplifies to \(O((n + k) \log n)\).

- Space complexity:
  - The space required is \(O(n)\) because we store all elements of the array in the heap.


# Code
```csharp []
class Solution {
    public long MaxKelements(int[] nums, int k) {
        // Max-heap priority queue
        PriorityQueue<int, int> maxHeap = new PriorityQueue<int, int>(Comparer<int>.Create((a, b) => b.CompareTo(a)));
        
        // Add all elements to the max-heap
        foreach (var num in nums) {
            maxHeap.Enqueue(num, num);
        }

        long score = 0;

        // Apply the operation exactly k times
        for (int i = 0; i < k; i++) {
            // Extract the largest element
            int maxVal = maxHeap.Dequeue();
            score += maxVal;
            
            // Calculate the new value (ceil(maxVal / 3))
            int newVal = (int)Math.Ceiling(maxVal / 3.0);
            
            // Insert the updated value back into the heap
            maxHeap.Enqueue(newVal, newVal);
        }

        return score;
    }
}

```
