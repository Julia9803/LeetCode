### 347. Top K Frequent Elements

Given a non-empty array of integers, return the ***k\*** most frequent elements.

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]
```

**Note:** 

- You may assume *k* is always valid, 1 ≤ *k* ≤ number of unique elements.
- Your algorithm's time complexity **must be** better than O(*n* log *n*), where *n* is the array's size.
- It's guaranteed that the answer is unique, in other words the set of the top k frequent elements is unique.
- You can return the answer in any order.

#### Solution:

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer,Integer> map = new HashMap<>();
        List<Integer>[] freq = new List[nums.length+1];
        List<Integer> arr = new ArrayList<>();
        
        for(int num: nums) {
            if(!map.containsKey(num))
                map.put(num,1);
            else
                map.put(num, map.get(num) + 1);
        }

        for(int key: map.keySet()) {
            int t = map.get(key);
            if(freq[t] == null)
                freq[t] = new ArrayList<Integer>();
            freq[t].add(key);
        }
        
        for(int i = freq.length-1;i >= 0 && arr.size() < k;i--) {
            if(freq[i] != null)
                arr.addAll(freq[i]);
        }
        int[] res = arr.stream().mapToInt(i -> i).toArray();
        return res;
    }
}
```

##### Date 2020.5.5