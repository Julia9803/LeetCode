### 47. Permutations II

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

**Example:**

```
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

#### Solution:

The 2nd solution has better performance.

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        int len = nums.length;
        List<Integer> curr = new ArrayList<Integer>();
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        boolean[] used = new boolean[len];
        Arrays.sort(nums);
        for(int i = 0;i<len;i++) {
            used[i] = false;
        }
        dfs(nums, used, curr, res);
        return res;
        
    }
    private void dfs(int[] nums, boolean[] used, List<Integer> curr, List<List<Integer>> res) {
        if(curr.size() == nums.length && !res.contains(curr)) {
            res.add(new ArrayList<Integer>(curr));
            return;
        }
        for(int i = 0;i<nums.length;i++) {
            if(used[i] == true) continue;
            used[i] = true;
            curr.add(nums[i]);
            dfs(nums, used, curr, res);
            curr.remove(curr.size()-1);
            used[i] = false;
        }
    }
}
```

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        int len = nums.length;
        List<Integer> curr = new ArrayList<Integer>();
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        boolean[] used = new boolean[len];
        Arrays.sort(nums);
        for(int i = 0;i<len;i++) {
            used[i] = false;
        }
        dfs(nums, used, curr, res);
        return res;
        
    }

    private void dfs(int[] nums, boolean[] used, List<Integer> curr, List<List<Integer>> res) {
        if(curr.size() == nums.length) {
            res.add(new ArrayList<Integer>(curr));
            return;
        }
        for(int i = 0;i<nums.length;i++) {
            if(used[i] == true) continue;
            // only do if previous duplicate is used
            if(i > 0 && nums[i-1] == nums[i] && !used[i-1]) continue;
            used[i] = true;
            curr.add(nums[i]);
            dfs(nums, used, curr, res);
            curr.remove(curr.size()-1);
            used[i] = false;
        }
    }
}
```

