### 671. Second Minimum Node In a Binary Tree

Given a non-empty special binary tree consisting of nodes with the non-negative value, where each node in this tree has exactly `two` or `zero` sub-node. If the node has two sub-nodes, then this node's value is the smaller value among its two sub-nodes. More formally, the property `root.val = min(root.left.val, root.right.val)` always holds.

Given such a binary tree, you need to output the **second minimum** value in the set made of all the nodes' value in the whole tree.

If no such second minimum value exists, output -1 instead.

**Example 1:**

```
Input: 
    2
   / \
  2   5
     / \
    5   7

Output: 5
Explanation: The smallest value is 2, the second smallest value is 5.
```

 

**Example 2:**

```
Input: 
    2
   / \
  2   2

Output: -1
Explanation: The smallest value is 2, but there isn't any second smallest value.
```

####  Solution:

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    // this solution is for binary search tree
//     public int findSecondMinimumValue(TreeNode root) {
//         Stack<TreeNode> stack = new Stack<>();
//         TreeNode curr = root;
//         int pre = 0;
        
//         while(curr != null || !stack.empty()) {
//             while(curr != null) {
//                 stack.push(curr);
//                 curr = curr.left;
//             }
//             curr = stack.pop();
//             if(pre == 0) pre = curr.val;
//             else if(pre != 0 && curr.val != pre) break;
//             curr = curr.right;
//         }
//         return curr == null ? -1: curr.val;
//     }
    
    public int findSecondMinimumValue(TreeNode root) {
        if(root.left == null) return -1;
        int l = root.left.val == root.val ? findSecondMinimumValue(root.left): root.left.val;
        int r = root.right.val == root.val ? findSecondMinimumValue(root.right): root.right.val;
        return l == -1 || r == -1 ? Math.max(l,r) : Math.min(l,r);
    }
}
```

##### Date 2020.4.1