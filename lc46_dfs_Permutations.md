### 46. Permutations

Given a collection of **distinct** integers, return all possible permutations.

**Example:**

```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

#### Solution:

**Caution**: It's wrong to add curr in res.add(), because that's just a pointer of curr, and will be deleted after curr removed.

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        int len = nums.length;
        List<Integer> curr = new ArrayList<Integer>();
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        
        boolean[] used = new boolean[len];
        for(int i = 0;i < len;i++) {
            used[i] = false;
        }
        
        dfs(nums, 0, len, used, curr, res);
        return res;
    }
    
    private void dfs(int[] nums, int s, int n, boolean[] used, List<Integer> curr, List<List<Integer>> res) {
        if(s == n) {
            res.add(new ArrayList<Integer>(curr));
            return;
        }
        for(int i = 0;i < nums.length; i++) {
            if(used[i] == true) continue;
            used[i] = true;
            curr.add(nums[i]);
            dp(nums, s + 1, n, used, curr, res);
            curr.remove(curr.get(curr.size()-1));
            used[i] = false;
        }
    }
}
```

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        int len = nums.length;
        List<Integer> curr = new ArrayList<Integer>();
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        
        dfs(nums, curr, res);
        return res;
    }
    
    private void dfs(int[] nums, List<Integer> curr, List<List<Integer>> res) {
        if(curr.size() == nums.length) {
            res.add(new ArrayList<Integer>(curr));
            return;
        }
        for(int i = 0;i < nums.length; i++) {
            if(curr.contains(nums[i])) continue;
            curr.add(nums[i]);
            dp(nums, curr, res);
            curr.remove(curr.get(curr.size()-1));
        }
    }
}
```

##### Date 2020.3.23