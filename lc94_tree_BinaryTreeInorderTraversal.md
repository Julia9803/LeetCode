### 94. Binary Tree Inorder Traversal

Given a binary tree, return the *inorder* traversal of its nodes' values.

**Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
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
    // 1. recursive
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null) return res;
        dfs(root, res);
        return res;
    }
    private void dfs(TreeNode root, List<Integer> res) {
        if(root == null) return;
        dfs(root.left, res);
        res.add(root.val);
        dfs(root.right, res);
    }
}
```

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
    // 2. iterative
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;
        if(root == null) return res;
        
        while(curr != null || !stack.empty()) {
            while(curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            res.add(curr.val);
            curr = curr.right;
        }
        return res;
    }
}
```

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
    // 3. Morris space O(1)
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        TreeNode curr = root;
        TreeNode pre;
        if(root == null) return res;
        
        while(curr != null) {
            // 1. if curr has left child, find rightmost node from left child, move it to the top
            if(curr.left != null) {
                pre = curr.left;
                // find rightmost node pre
                while(pre.right != null) {
                    pre = pre.right;
                }
                pre.right = curr; // set node pre to top
                TreeNode tmp = curr;
                curr = curr.left; // set rightmost node as curr
                tmp.left = null;
            } else {
                // 2. if curr has no left child, add curr
                res.add(curr.val);
                curr = curr.right;
            }
        }
        return res;
    }
}
```

##### Date 2020.3.30