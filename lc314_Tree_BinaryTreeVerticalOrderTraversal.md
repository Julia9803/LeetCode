### 314. Binary Tree Vertical Order Traversal

Given the `root` of a binary tree, return ***the vertical order traversal** of its nodes' values*. (i.e., from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from **left to right**.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/28/vtree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[9],[3,15],[20],[7]]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/01/28/vtree2-1.jpg)

```
Input: root = [3,9,8,4,0,1,7]
Output: [[4],[9],[3,0,1],[8],[7]]
```

**Example 3:**

![img](https://assets.leetcode.com/uploads/2021/01/28/vtree2.jpg)

```
Input: root = [3,9,8,4,0,1,7,null,null,null,2,5]
Output: [[4],[9,5],[3,0,1],[8,2],[7]]
```

**Example 4:**

```
Input: root = []
Output: []
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

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
    public List<List<Integer>> verticalOrder(TreeNode root) {
        // each col mapping with ArrayList
        List<List<Integer>> res = new ArrayList<>();
        Queue<Integer> cols = new LinkedList<>();
        Queue<TreeNode> nodes = new LinkedList<>();
        Map<Integer,ArrayList<Integer>> map = new HashMap<>();
        int min = 0;
        int max = 0;
        cols.add(0);
        nodes.add(root);
        
        if(root == null) return res;
        
        while(!nodes.isEmpty()) {
            int col = cols.poll();
            TreeNode node = nodes.poll();
            if(!map.containsKey(col)) {
                map.put(col, new ArrayList<Integer>());
            }
            map.get(col).add(node.val);
            
            if(node.left != null) {
                cols.add(col - 1);
                nodes.add(node.left);
                min = Math.min(min, col - 1);
            }
            if(node.right != null) {
                cols.add(col + 1);
                nodes.add(node.right);
                max = Math.max(max, col + 1);
            }
        }
        
        for(int i = min;i <= max;i++) {
            res.add(map.get(i));
        }
        return res;
    }
}
```

##### Date 2021.9.12