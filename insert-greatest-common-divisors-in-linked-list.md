# LeetCodeSolutions: 2807-insert-greatest-common-divisors-in-linked-list


Solution: https://leetcode.com/problems/insert-greatest-common-divisors-in-linked-list/solutions/5766504/beats-92-optimal-solution/

Description: https://leetcode.com/problems/insert-greatest-common-divisors-in-linked-list/description/

![image.png](https://assets.leetcode.com/users/images/0aed1dcf-81f6-4b0a-9f7f-6bdfef1069b4_1725980394.0446627.png)

# Intuition
The problem asks to insert a new node between every pair of adjacent nodes in a linked list. The value of this node is the Greatest Common Divisor (GCD) of the values of the two nodes. 

The first thought is to traverse the linked list, and for each pair of adjacent nodes, compute the GCD of their values and insert a new node with that GCD in between them. This requires iterating over each node and performing the GCD computation, which can be done efficiently using the Euclidean algorithm.

# Approach
1. Start at the head of the linked list.
2. While traversing the list:
   - For each pair of adjacent nodes, calculate the GCD of their values.
   - Create a new node containing this GCD value.
   - Insert this new node between the current node and the next node.
3. Move to the next pair and repeat the process until reaching the end of the list.
4. Return the modified linked list.

To compute the GCD of two numbers, we can use the Euclidean algorithm, which runs in logarithmic time relative to the smaller number.

# Complexity
- Time complexity:
  - Each node is visited once, and for every pair of adjacent nodes, the GCD is computed. The Euclidean algorithm used for the GCD calculation takes $$O(\log(\min(a, b)))$$, where `a` and `b` are the values of adjacent nodes. 
  - Overall, the time complexity is $$O(n \log k)$$, where `n` is the number of nodes in the list, and `k` is the average value of the node values.

- Space complexity:
  - We are modifying the linked list in place, so no extra space is required for the list modification. However, the recursive GCD calculation may use stack space.
  - Thus, the space complexity is $$O(1)$$ if ignoring the recursive call stack (for Euclidean GCD calculation), or $$O(\log k)$$ accounting for the stack space.


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
    // Function to calculate GCD of two numbers
    private int GCD(int a, int b) {
        if (b == 0) return a;
        return GCD(b, a % b);
    }

    public ListNode InsertGreatestCommonDivisors(ListNode head) {
        // Start from the head node
        ListNode current = head;

        // Traverse through the list until we reach the last node
        while (current != null && current.next != null) {
            // Get the GCD of current node value and next node value
            int gcdValue = GCD(current.val, current.next.val);

            // Create a new node with the GCD value
            ListNode gcdNode = new ListNode(gcdValue);

            // Insert the GCD node between current and next
            gcdNode.next = current.next;
            current.next = gcdNode;

            // Move to the next pair (skipping the newly inserted GCD node)
            current = gcdNode.next;
        }

        // Return the modified linked list
        return head;
    }

    // Helper function to print the linked list (for testing)
    public void PrintList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            Console.Write(current.val + " ");
            current = current.next;
        }
        Console.WriteLine();
    }
}
```
