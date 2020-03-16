### 39. Combination Sum

Given a **set** of candidate numbers (`candidates`) **(without duplicates)** and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sums to `target`.

The **same** repeated number may be chosen from `candidates` unlimited number of times.

**Note:**

- All numbers (including `target`) will be positive integers.
- The solution set must not contain duplicate combinations.

**Example 1:**

```
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```

**Example 2:**

```
Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

#### Solution:

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> cur = new ArrayList<>();
        Arrays.sort(candidates);
        dfs(candidates, target, 0, cur, res);
        return res;
    }
    
    public void dfs(int[] candidates, int target, int s, List<Integer> cur, List<List<Integer>> res) {
        if(target == 0) {
            res.add(new ArrayList<Integer>(cur));
        }
        for(int i = s;i < candidates.length;i++) {
            if(candidates[i] > target) break;
            cur.add(candidates[i]);
            dfs(candidates, target - candidates[i], i, cur, res);
            cur.remove(cur.get(cur.size()-1));
        }
    }
}
```

##### Date 2020.3.17