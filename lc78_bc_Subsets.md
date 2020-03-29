### 78. Subsets

Given a set of **distinct** integers, *nums*, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

#### Solution:

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        Arrays.sort(nums);
        dfs(nums, res, new ArrayList<Integer>(),0);
        return res;
    }
    public void dfs(int[] nums, List<List<Integer>> res, List<Integer> tmp, int start) {
        res.add(new ArrayList<Integer>(tmp));
        for(int i = start;i<nums.length;i++) {
            tmp.add(nums[i]);
            dfs(nums, res, tmp, i + 1);
            tmp.remove(tmp.size()-1);
        }
    }
}
```

##### Date 2020.3.29