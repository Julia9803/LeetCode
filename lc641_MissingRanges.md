### 641. Missing Ranges(Google)

Given a sorted integer array where **the range of elements are in the inclusive range [lower, upper]**, return its missing ranges.

### Example

**Example 1**

```
Input:
nums = [0, 1, 3, 50, 75], lower = 0 and upper = 99
Output:
["2", "4->49", "51->74", "76->99"]
Explanation:
in range[0,99],the missing range includes:range[2,2],range[4,49],range[51,74] and range[76,99]
```

**Example 2**

```
Input:
nums = [0, 1, 2, 3, 7], lower = 0 and upper = 7
Output:
["4->6"]
Explanation:
in range[0,7],the missing range include range[4,6]
```

#### Solution:

```java
public class Solution {
    /*
     * @param nums: a sorted integer array
     * @param lower: An integer
     * @param upper: An integer
     * @return: a list of its missing ranges
     */
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        // write your code here
        List<String> list = new ArrayList<String>();
        String t;
        if(nums.length == 0) {
            t = getString(lower, upper);
            list.add(t);
            return list;
        }
        t = getString(lower, (long)nums[0]-1);
        if(!t.equals("")) {
            list.add(t);
        }
        for(int i = 1;i < nums.length;i++) {
            t = getString((long)nums[i-1] + 1, (long)nums[i] - 1);
            if(!t.equals("")) {
                list.add(t);
            }
        }
        t = getString((long)nums[nums.length-1] + 1, upper);
        if(!t.equals("")) {
            list.add(t);
        }
        return list;
    }
    
    public String getString(long m, long n) {
        if(m > n) return "";
        else if(m == n) return String.valueOf(m);
        else return m + "->" + n;
    }
}
```

##### Date 2020.8.25