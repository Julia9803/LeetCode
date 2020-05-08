### 993. Cousins in Binary Tree

In a binary tree, the root node is at depth `0`, and children of each depth `k` node are at depth `k+1`.

Two nodes of a binary tree are *cousins* if they have the same depth, but have **different parents**.

We are given the `root` of a binary tree with unique values, and the values `x` and `y` of two different nodes in the tree.

Return `true` if and only if the nodes corresponding to the values `x` and `y` are cousins.

 

**Example 1:
![img](https://assets.leetcode.com/uploads/2019/02/12/q1248-01.png)**

```
Input: root = [1,2,3,4], x = 4, y = 3
Output: false
```

**Example 2:
![img](https://assets.leetcode.com/uploads/2019/02/12/q1248-02.png)**

```
Input: root = [1,2,3,null,4,null,5], x = 5, y = 4
Output: true
```

**Example 3:**

**![img](https://assets.leetcode.com/uploads/2019/02/13/q1248-03.png)**

```
Input: root = [1,2,3,null,4], x = 2, y = 3
Output: false
```

 

**Note:**

1. The number of nodes in the tree will be between `2` and `100`.
2. Each node has a unique integer value from `1` to `100`.

####  Solution:

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
    private int xFloor = 0;
    private int yFloor = 0;
    private TreeNode xParent = null;
    private TreeNode yParent = null;
    
    public boolean isCousins(TreeNode root, int x, int y) {
        dfs(root, null, x, y, 1);
        return (xFloor == yFloor) && (xParent != yParent);
    }
    
    private void dfs(TreeNode curr, TreeNode parent, int x, int y, int floor) {
        if(curr == null) return;
        if(curr.val == x) {
            xFloor = floor;
            xParent = parent;
        } else if(curr.val == y) {
            yFloor = floor;
            yParent = parent;
        }
        dfs(curr.left, curr, x, y, floor + 1);
        dfs(curr.right, curr, x, y, floor + 1);
    }
}
```

```java
// bfs
class Solution {
    
    public boolean isCousins(TreeNode root, int x, int y) {
        Queue<TreeNode> queue = new LinkedList<>();
        boolean hasX = false;
        boolean hasY = false;
        
        queue.offer(root);
        while(!queue.isEmpty()) {
            int size = queue.size();
            for(int i = 0;i < size;i++) {
                TreeNode t = queue.poll();
                if(t.val == x) hasX = true;
                if(t.val == y) hasY = true;
                if(t.left != null && t.right != null) {
                    if(t.left.val == x && t.right.val == y) return false;
                    if(t.left.val == y && t.right.val == x) return false;
                }
                if(t.left != null) queue.offer(t.left);
                if(t.right != null) queue.offer(t.right);
            }
            if(hasX && hasY) return true;
            else if(hasX || hasY) return false;
        }
        return false;
    }
}
```

##### Date 2020.5.7