#### 128. Longest Consecutive Sequence(Google FaceBook)

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

Your algorithm should run in O(*n*) complexity.

**Example:**

```
Input: [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

#### Solution:

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if(nums.length == 0) return 0;
        Set<Integer> set = new HashSet<Integer>();
        for(int i: nums) set.add(i);
        int res = 1;
        for(int n: nums) {
            if(set.remove(n)) {
                int tmp = 1;
                int t = n;
                while(set.remove(t-1)) t--;
                tmp += (n - t);
                t = n;
                while(set.remove(t+1)) t++;
                tmp += (t - n);
                res = Math.max(res, tmp);
            }
        }
        return res;
    }
}
```

##### Date 2020.8.26