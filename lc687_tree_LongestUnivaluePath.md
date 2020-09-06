### 687. Longest Univalue Path

Given a binary tree, find the length of the longest path where each node in the path has the same value. This path may or may not pass through the root.

The length of path between two nodes is represented by the number of edges between them.

 

**Example 1:**

**Input:**

```
              5
             / \
            4   5
           / \   \
          1   1   5
```

**Output:** 2

 

**Example 2:**

**Input:**

```
              1
             / \
            4   5
           / \   \
          4   4   5
```

**Output:** 2

 

**Note:** The given binary tree has not more than 10000 nodes. The height of the tree is not more than 1000.

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
    int res = 0;
    public int longestUnivaluePath(TreeNode root) {
        if(root == null) return 0;
        dfs(root);
        return res;
    }
    public int dfs(TreeNode node) {
        if(node == null) return 0;
        int left = dfs(node.left);
        int right = dfs(node.right);
        int resl = 0, resr = 0;
        if(node.left != null && node.val == node.left.val)
            resl = left + 1;
        if(node.right != null && node.val == node.right.val)
            resr = right + 1;
        res = Math.max(res, resl + resr);
        return Math.max(resl, resr);
    }
}
```

##### Date 2020.9.6