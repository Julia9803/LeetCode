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
    public List<Integer> postorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        LinkedList<Integer> res = new LinkedList<>();
        TreeNode curr = root;
        
        while(curr != null || !stack.empty()) {
            if(curr != null) {
                res.addFirst(curr.val);
                stack.add(curr);
                curr = curr.right;
            } else {
                TreeNode tmp = stack.pop();
                curr = tmp.left;
            }
        }
        return res;
    }
}
```

##### Date 2020.3.31