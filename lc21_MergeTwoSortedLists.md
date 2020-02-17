### 21. Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        //iterate way
        ListNode res = new ListNode(0);
        ListNode curr = res;
        
        while(l1 != null || l2 != null) {
            if(l1 == null) {
                curr.next = l2;
                break;
            } else if(l2 == null) {
                curr.next = l1;
                break;
            } else {
                int v1 = l1.val;
                int v2 = l2.val;
                if(v1 <= v2) {
                    curr.next = new ListNode(v1);
                    curr = curr.next;
                    l1 = l1.next;
                }else if(v1 > v2) {
                    curr.next = new ListNode(v2);
                    curr = curr.next;
                    l2 = l2.next;
                }
            }
        }
        return res.next;
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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {        
        //recursive way
        if(l1 == null || l2 == null) return l1 == null? l2:l1;
        if(l1.val <= l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        }
        else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
```

##### Date 2020.2.17