### 105. Construct Binary Tree from Preorder and Inorder Traversal

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**
You may assume that duplicates do not exist in the tree.

For example, given

```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```

Return the following binary tree:

```
    3
   / \
  9  20
    /  \
   15   7
```

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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder.length == 0) return null;
        return helper(preorder, inorder, 0, 0, preorder.length-1);
    }
    private TreeNode helper(int[] preorder, int[] inorder, int pre_st, int in_st, int in_end) {
        if(pre_st > preorder.length - 1 || in_st > in_end) return null;
        TreeNode root = new TreeNode(preorder[pre_st]);
        int index = in_st;
        for(int i = in_st;i <= in_end;i++) {
            if(inorder[i] == root.val) {
                index = i;
                break;
            }
        }
        root.left = helper(preorder, inorder, pre_st + 1, in_st, index - 1);
        root.right = helper(preorder, inorder, pre_st + index - in_st + 1, index + 1, in_end);
        return root;
    }
}
```

##### Date 2020.4.6