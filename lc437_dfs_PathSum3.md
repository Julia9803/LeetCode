### 437. Path Sum III

You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

**Example:**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
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
    public int pathSum(TreeNode root, int sum) {
        if(root == null) return 0;
        return pathSumSub(root, sum) + pathSum(root.left, sum) + pathSum(root.right, sum);
    }
    
    public int pathSumSub(TreeNode root, int sum) {
        int res = 0;
        if(root == null) return 0;
        if(root.val == sum) res++;
        res += pathSumSub(root.left, sum-root.val);
        res += pathSumSub(root.right, sum-root.val);
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
    public int pathSum(TreeNode root, int sum) {
        Map<Integer,Integer> map = new HashMap<>();
        map.put(0,1);
        return pathSumSub(root,0,sum,map);
    }
    
    public int pathSumSub(TreeNode root, int total, int target, Map<Integer,Integer> map) {
        if(root == null) return 0;
        total += root.val;
        int res = map.getOrDefault(total-target,0);
        map.put(total, map.getOrDefault(total,0) + 1);
        res += pathSumSub(root.left,total,target,map) + pathSumSub(root.right,total,target,map);
        map.put(total, map.get(total) - 1);
        return res;
    }
 }
```

##### Date 2020.3.13