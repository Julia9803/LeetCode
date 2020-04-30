###  Leftmost Column with at Least a One

*(This problem is an **interactive problem**.)*

A binary matrix means that all elements are `0` or `1`. For each **individual** row of the matrix, this row is sorted in non-decreasing order.

Given a row-sorted binary matrix binaryMatrix, return leftmost column index(0-indexed) with at least a `1` in it. If such index doesn't exist, return `-1`.

**You can't access the Binary Matrix directly.** You may only access the matrix using a `BinaryMatrix` interface:

- `BinaryMatrix.get(row, col)` returns the element of the matrix at index `(row, col)` (0-indexed).
- `BinaryMatrix.dimensions()` returns a list of 2 elements `[rows, cols]`, which means the matrix is `rows * cols`.

Submissions making more than `1000` calls to `BinaryMatrix.get` will be judged *Wrong Answer*. Also, any solutions that attempt to circumvent the judge will result in disqualification.

For custom testing purposes you're given the binary matrix `mat` as input in the following four examples. You will not have access the binary matrix directly.

 

**Example 1:**

**![img](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-5.jpg)**

```
Input: mat = [[0,0],[1,1]]
Output: 0
```

**Example 2:**

**![img](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-4.jpg)**

```
Input: mat = [[0,0],[0,1]]
Output: 1
```

**Example 3:**

**![img](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-3.jpg)**

```
Input: mat = [[0,0],[0,0]]
Output: -1
```

**Example 4:**

**![img](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-6.jpg)**

```
Input: mat = [[0,0,0,1],[0,0,1,1],[0,1,1,1]]
Output: 1
```

 

**Constraints:**

- `rows == mat.length`
- `cols == mat[i].length`
- `1 <= rows, cols <= 100`
- `mat[i][j]` is either `0` or `1`.
- `mat[i]` is sorted in a non-decreasing way.

#### Solution:

```java
/**
 * // This is the BinaryMatrix's API interface.
 * // You should not implement it, or speculate about its implementation
 * interface BinaryMatrix {
 *     public int get(int row, int col) {}
 *     public List<Integer> dimensions {}
 * };
 */

class Solution {
    public int leftMostColumnWithOne(BinaryMatrix binaryMatrix) {
        int m = binaryMatrix.dimensions().get(0);// row
        int n = binaryMatrix.dimensions().get(1);// col
        int i = 0, j = n - 1;
        int tmp = 0, res = -1;
        while(j >= 0 && i < m) {
            tmp = binaryMatrix.get(i,j);
            if(tmp == 1) {
                if(j == 0) {// for left corner
                    res = 0;
                    break;
                    }
                j--;// move left if meet 1
            }
            if(tmp == 0) {
                if(i == m - 1) {
                    if(j == n - 1) {res = -1; break;}// for total 0 matrix 
                    res = j + 1;// for bottom corner
                    break;
                }
                i++;// move down if meet 0
            }
        }
        return res;
    }
}
```

##### Date 2020.5.1