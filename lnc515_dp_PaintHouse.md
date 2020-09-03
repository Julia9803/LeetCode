### 515. Paint House

There are a row of `n` houses, each house can be painted with one of the three colors: red, blue or green. The cost of painting each house with a certain color is different. You have to paint all the houses such that **no two adjacent houses have the same color,** and you need to cost the least. Return the minimum cost.

The cost of painting each house with a certain color is represented by a `n` x `3` cost matrix. For example, `costs[0][0]` is the cost of painting house `0` with color red; `costs[1][2]` is the cost of painting house `1` with color green, and so on... Find the minimum cost to paint all houses.

### 样例

**Example 1:**

```
Input: [[14,2,11],[11,14,5],[14,3,10]]
Output: 10
Explanation: Paint house 0 into blue, paint house 1 into green, paint house 2 into blue. Minimum cost: 2 + 5 + 3 = 10.
```

**Example 2:**

```
Input: [[1,2,3],[1,4,6]]
Output: 3
```

### 注意事项

All costs are positive integers.

#### Solution:

```java
public class Solution {
    /**
     * @param costs: n x 3 cost matrix
     * @return: An integer, the minimum cost to paint all houses
     */
    public int minCost(int[][] costs) {
        // write your code here
        int num = costs.length; // house num
        int[][] list = new int[num+1][3]; // 对前n个house，有3种染色方法，每种的价格
        list[0][0] = list[0][1] = list[0][2] = 0;
        for(int i = 1;i <= num;i++) {
            // color the house i-1
            for(int j = 0;j < 3;j++) {
                list[i][j] = Integer.MAX_VALUE;
                // color the house i-2
                for(int k = 0;k < 3;k++) {
                    if(j != k) {
                        list[i][j] = Math.min(list[i][j], list[i-1][k] + costs[i-1][j]);
                    }
                }
            }
        }
        return Math.min(list[num][0], Math.min(list[num][1], list[num][2]));
    }
}
```

##### Date 2020.8.21

