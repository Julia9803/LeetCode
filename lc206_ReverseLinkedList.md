### 206. Reverse Linked List

Reverse a singly linked list.

**Example:**

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

**Follow up:**

A linked list can be reversed either iteratively or recursively. Could you implement both?

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
    public ListNode reverseList(ListNode head) {
        // iterative
        ListNode newHead = null;
        ListNode next = null;
        while(head != null) {
            next = head.next;
            head.next = newHead;
            newHead = head;
            head = next;
        }
        return newHead;
    }
}
```

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
    public ListNode reverseList(ListNode head) {
        // recursive
        return reverse(head, null);
    }
    
    public ListNode reverse(ListNode head, ListNode newHead) {
        if(head == null) return newHead;
        ListNode next = head.next;
        head.next = newHead;
        return reverse(next, head);
    }
}
```

##### Date 2020.2.24