Solution: https://leetcode.com/problems/add-two-numbers/solutions/5978625/optimal-solution/

Description: https://leetcode.com/problems/add-two-numbers/description/

# Intuition
The problem requires us to add two numbers represented by two linked lists, with digits stored in reverse order. My first thought was to simulate the addition process as if we were doing it by hand, digit by digit, from the least significant to the most significant position. Since the linked lists are already in reverse order, we can start from the head and move through each node while keeping track of any carry-over from the addition.

# Approach
1. **Initialize a Dummy Node**: We create a dummy head node that will allow us to easily build the resulting linked list without worrying about special cases for the head.
2. **Traverse Both Lists**: We iterate over the nodes in both `l1` and `l2` simultaneously. At each step, we:
   - Sum the values of the current nodes in `l1` and `l2` (if they exist) and add any carry from the previous step.
   - Calculate the carry for the next step by dividing the sum by 10.
   - Store the result of `sum % 10` in a new node in the result linked list.
3. **Handle Remaining Carry**: After the loop, if there's any remaining carry, add it as a final node in the result list.
4. **Return the Result**: The result is stored starting from `dummyHead.next`, as `dummyHead` was just a placeholder.

This approach ensures that we handle lists of different lengths and also accommodate any carry left over after both lists are fully traversed.

# Complexity
- **Time Complexity**: $$O(\max(m, n))$$, where \( m \) and \( n \) are the lengths of `l1` and `l2`. We process each node in both linked lists once.
  
- **Space Complexity**: $$O(\max(m, n))$$, since we create a new linked list to store the result, which can be as long as the longer of `l1` or `l2`, plus one extra node if there is a final carry.


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
     public ListNode AddTwoNumbers(ListNode l1, ListNode l2) {
        // Dummy node to act as the start of the resulting linked list
        ListNode dummyHead = new ListNode(0);
        ListNode current = dummyHead;
        int carry = 0;

        // Loop while either l1 or l2 has remaining nodes, or there is a carry to process
        while (l1 != null || l2 != null || carry != 0) {
            int sum = carry;

            // Add the values from the current nodes of l1 and l2, if they exist
            if (l1 != null) {
                sum += l1.val;
                l1 = l1.next;
            }
            if (l2 != null) {
                sum += l2.val;
                l2 = l2.next;
            }

            // Calculate the carry for the next iteration and the digit to store in the result
            carry = sum / 10;
            int digit = sum % 10;

            // Add the new digit to the resulting list
            current.next = new ListNode(digit);
            current = current.next;
        }

        // Return the next node of dummyHead, which is the actual start of the result list
        return dummyHead.next;
    }
}
```
