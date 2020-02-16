### 19. Remove Nth Node From End of List

Given a linked list, remove the *n*-th node from the end of list and return its head.

**Example:**

```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

#### Solution:

```java
/**
 maintain a slow and a fast pointer, fast pointer goes n+1 further,
 then two pointers move forward equally until fast pointer meets the end.
 Then the n-th node is just the next of the slow pointer, make slower pointer's
 point to the next's next node.
 */

// Definition for singly-linked list.
// public class ListNode {
//      int val;
//      ListNode next;
//      ListNode(int x) { val = x; }
// }

class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode start = new ListNode(0);
        start.next = head;
        ListNode slow = start;
        ListNode fast = start;
        
        for(int i = 1;i <= n+1;i++) {
            fast = fast.next;
        }
        
        while(fast != null) {
            slow = slow.next;
            fast = fast.next;
        }
        
        slow.next = slow.next.next;
        
        return start.next;
    }
}
```

##### Date 2020.2.16

