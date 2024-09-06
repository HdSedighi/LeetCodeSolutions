# LeetCodeSolutions: 2028-Medium-find-missing-observations



Solution: https://leetcode.com/problems/delete-nodes-from-linked-list-present-in-array/solutions/5748225/easy-solution/

Description: https://leetcode.com/problems/delete-nodes-from-linked-list-present-in-array/description/


# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem requires us to remove nodes from a linked list if their values exist in a given array `nums`. The first thought is to traverse the linked list and compare each node's value with the values in `nums`. Since `nums` can be large, a direct search would be inefficient. To make the comparison fast, we can store `nums` in a data structure that allows for O(1) look-up time, such as a `HashSet`.

# Approach
<!-- Describe your approach to solving the problem. -->
1. **Convert `nums` to a HashSet**: By using a `HashSet`, we can check whether a node's value exists in the `nums` array in constant time.
2. **Traverse the linked list**: Use a dummy node to simplify handling edge cases, such as when the head of the list needs to be removed. Traverse the linked list with a single pointer and, for each node, check if its value exists in the `HashSet`.
3. **Modify the linked list**: If a node's value is found in the `HashSet`, skip the node by adjusting the `next` pointer of the previous node to bypass the current node. This effectively removes the node from the list.
4. **Return the modified list**: At the end, return the modified list starting from the `dummy.next`.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
The time complexity is $$O(n + m)$$, where $$n$$ is the number of nodes in the linked list, and $$m$$ is the size of the `nums` array. Building the `HashSet` takes O(m), and traversing the linked list takes O(n).

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
The space complexity is $$O(m)$$ because we store the values from `nums` in a `HashSet`. The linked list itself does not count towards auxiliary space, as we are modifying it in place.


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
    public ListNode ModifiedList(int[] nums, ListNode head) {
        // Convert nums array to a HashSet for O(1) look-up time
        HashSet<int> numsSet = new HashSet<int>(nums);

        // Create a dummy node to handle cases where the head needs to be removed
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        // Use one pointer to traverse the list and track the previous node
        ListNode current = dummy;

        while (current.next != null) {
            // If the next node's value is in numsSet, remove it by skipping it
            if (numsSet.Contains(current.next.val)) {
                current.next = current.next.next; // skip the node
            } else {
                current = current.next; // move to the next node only if no node was removed
            }
        }

        // Return the new head of the list
        return dummy.next;
    }
}

```
