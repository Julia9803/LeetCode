### 54. Spiral Matrix

Given an `m x n` `matrix`, return *all elements of the* `matrix` *in spiral order*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

```
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

 

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 10`
- `-100 <= matrix[i][j] <= 100`

#### Solution:

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        int rowStart = 0;
        int rowEnd = matrix.length - 1;
        int colStart = 0;
        int colEnd = matrix[0].length - 1;
        List<Integer> res = new ArrayList<>();
        while(rowStart <= rowEnd && colStart <= colEnd) {
            // right
            for(int j = colStart;j <= colEnd;j++) {
                res.add(matrix[rowStart][j]);
            }
            rowStart++;
            // down
            for(int j = rowStart;j <= rowEnd;j++) {
                res.add(matrix[j][colEnd]);
            }
            colEnd--;
            // left
            if(rowStart <= rowEnd) {
                for(int j = colEnd;j >= colStart;j--) {
                    res.add(matrix[rowEnd][j]);
                }
            }
            rowEnd--;
            // up
            if(colStart <= colEnd) {
               for(int j = rowEnd;j >= rowStart;j--) {
                    res.add(matrix[j][colStart]);
                } 
            }
            colStart++;
        }
        return res;
    }
}
```

##### Date 2021.8.19