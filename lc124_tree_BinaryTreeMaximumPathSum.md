### 124. Binary Tree Maximum Path Sum

Given a **non-empty** binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain **at least one node** and does not need to go through the root.

**Example 1:**

```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```

**Example 2:**

```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
```

#### Solution:

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    int res = Integer.MIN_VALUE;
    
    public int maxPathSum(TreeNode root) {
        // 1. return root and one child
        // 2. max = left + root + right
        if(root == null) return 0;
        helper(root);
        return res;
    }
    
    public int helper(TreeNode root) {
        if(root == null) return 0;
        int l = Math.max(helper(root.left),0);
        int r = Math.max(helper(root.right),0);
        res = Math.max(res, root.val + l + r);
        return Math.max(l,r) + root.val;
    }
}
```

##### Date 2020.4.29