### 145. Binary Tree Postorder Traversal

Given a binary tree, return the *postorder* traversal of its nodes' values.

**Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [3,2,1]
```

**Follow up:** Recursive solution is trivial, could you do it iteratively?

#### Solution:

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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        TreeNode curr = root;
        if(root == null) return res;
        helper(curr, res);
        return res;
    }
    
    private void helper(TreeNode curr, List<Integer> res) {
        if(curr == null) return;
        helper(curr.left, res);
        helper(curr.right, res);
        res.add(curr.val);
    }
}
```

##### Date 2020.3.30