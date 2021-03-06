### 915. Partition Array into Disjoint Intervals

Given an array `A`, partition it into two (contiguous) subarrays `left` and `right` so that:

- Every element in `left` is less than or equal to every element in `right`.
- `left` and `right` are non-empty.
- `left` has the smallest possible size.

Return the **length** of `left` after such a partitioning. It is guaranteed that such a partitioning exists.

 

**Example 1:**

```
Input: [5,0,3,8,6]
Output: 3
Explanation: left = [5,0,3], right = [8,6]
```

**Example 2:**

```
Input: [1,1,1,0,6,12]
Output: 4
Explanation: left = [1,1,1,0], right = [6,12]
```

 

**Note:**

1. `2 <= A.length <= 30000`
2. `0 <= A[i] <= 10^6`
3. It is guaranteed there is at least one way to partition `A` as described.

####  Solution:

```java
class Solution {
    public int partitionDisjoint(int[] A) {
        int n = A[0];
        int max = n;
        int i = 1;
        while(i < A.length) {
            if(A[i] >= max) {
                int j = i + 1;
                int m = A[i];
                while(j < A.length) {
                    if(A[j] < max) break;
                    if(A[j] > m) m = A[j];
                    j++;
                }
                if(j == A.length) return i;
                max = m;
                i = j + 1;
            } else
            i++;
        }
        return A.length-1;
    }
}
```

##### Date 2020.9.5