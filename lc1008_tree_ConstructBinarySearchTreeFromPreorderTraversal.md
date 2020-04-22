### 1008. Construct Binary Search Tree from Preorder Traversal

Return the root node of a binary **search** tree that matches the given `preorder` traversal.

*(Recall that a binary search tree is a binary tree where for every node, any descendant of `node.left` has a value `<` `node.val`, and any descendant of `node.right` has a value `>` `node.val`. Also recall that a preorder traversal displays the value of the `node` first, then traverses `node.left`, then traverses `node.right`.)*

 

**Example 1:**

```
Input: [8,5,1,7,10,12]
Output: [8,5,10,1,7,null,12]
```

 

**Note:** 

1. `1 <= preorder.length <= 100`
2. The values of `preorder` are distinct.

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
    int split = 0;
    public TreeNode bstFromPreorder(int[] preorder) {
        return helper(preorder, 0, preorder.length);
    }
    private TreeNode helper(int[] preorder, int start, int end) {
        if(start >= end) return null;
        TreeNode root = new TreeNode(preorder[start]);
        split = start;
        while(split < end && preorder[split] <= preorder[start]) {
            split++;
        }
        root.left = helper(preorder, start + 1, split);
        root.right = helper(preorder, split, end);
        return root;
    }
}
```

##### Date 2020.4.21