# LeetCodeSolutions: 725-Medium-split-linked-list-in-parts



Solution: https://leetcode.com/problems/split-linked-list-in-parts/solutions/5756699/beats-94-easy-optimal-solution/

Description: https://leetcode.com/problems/split-linked-list-in-parts/description/

![image.png](https://assets.leetcode.com/users/images/6b73e2ff-a70d-4f7e-aa12-c4beeb7e8861_1725811141.788712.png)

# Intuition
To solve the problem of splitting a singly linked list into `k` parts with as equal size as possible, start by understanding that the total length of the linked list determines how the nodes can be distributed. The aim is to divide the list into `k` parts such that each part has almost the same number of nodes. If there are extra nodes, they should be distributed to the earlier parts. The final parts can be shorter if there aren't enough nodes to fill them.

# Approach
1. **Calculate Total Length**: Traverse the linked list once to determine its total length. This helps in calculating the size of each part and the number of parts that need an extra node.

2. **Determine Part Size and Extra Nodes**: 
   - Calculate the base size of each part using integer division of the total length by `k` (`partSize = totalLength / k`).
   - Compute the number of extra nodes that need to be distributed to some parts to balance out the size (`extraNodes = totalLength % k`).

3. **Split the List**:
   - Initialize a result array of size `k` to store the heads of the `k` parts.
   - Iterate through the linked list and for each part, build it based on the calculated sizes:
     - Create each part by iterating through the list and collecting nodes up to the calculated size (including extra nodes where necessary).
     - Disconnect the end of each part from the rest of the list.
     - Store the head of each part in the result array.

4. **Return the Result**: Return the array containing the heads of the `k` parts.

# Complexity
- Time complexity: $$O(n)$$  
  The list is traversed once to determine its length and then again to split it into parts. Thus, the overall time complexity is linear with respect to the number of nodes in the list.

- Space complexity: $$O(1)$$  
  The space complexity is constant, excluding the input and output. The result array of size `k` is used to store the heads of the parts, which requires space proportional to `k`, but the operations do not require additional space beyond this.

# Code
```csharp []
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
   public ListNode[] SplitListToParts(ListNode head, int k) {
        // Step 1: Calculate the total length of the list
        int totalLength = 0;
        ListNode current = head;
        while (current != null) {
            totalLength++;
            current = current.next;
        }

        // Step 2: Determine the size of each part and the number of extra nodes
        int partSize = totalLength / k;
        int extraNodes = totalLength % k;

        // Step 3: Create an array to store the result
        ListNode[] result = new ListNode[k];
        current = head;
        for (int i = 0; i < k; i++) {
            ListNode partHead = current;
            ListNode partTail = null;
            int currentPartSize = partSize + (extraNodes-- > 0 ? 1 : 0);

            // Build the current part
            for (int j = 0; j < currentPartSize; j++) {
                if (current != null) {
                    partTail = current;
                    current = current.next;
                }
            }

            // Disconnect the current part from the remaining list
            if (partTail != null) {
                partTail.next = null;
            }

            // Store the head of the current part
            result[i] = partHead;
        }

        return result;
    }
}
```
