### 234. Palindrome Linked List

Given a singly linked list, determine if it is a palindrome.

**Example 1:**

```
Input: 1->2
Output: false
```

**Example 2:**

```
Input: 1->2->2->1
Output: true
```

**Follow up:**
Could you do it in O(n) time and O(1) space?

#### Solution:

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        /** split the List to two with fast and slow pointer
         reverse last half, then compare
         **/
        ListNode fast = head, slow = head;
        while(fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        if(fast != null) slow = slow.next; // odd nodes
        slow = reverse(slow);
        
        while(slow != null) { // compare
            if(head.val != slow.val) return false;
            head = head.next;
            slow = slow.next;
        }
        return true;
    }
    
    public ListNode reverse(ListNode slow) {
        ListNode newHead = null;
        while(slow != null) {
            ListNode next = slow.next;
            slow.next = newHead;
            newHead = slow;
            slow = next;
        }
        return newHead;
    }
}
```

##### Date 2020.2.24