### 49. Group Anagrams

Given an array of strings, group anagrams together.

**Example:**

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**

- All inputs will be in lowercase.
- The order of your output does not matter.

#### Solution:

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if(strs == null || strs.length == 0) return new ArrayList<List<String>>();
        Map<String,ArrayList<String>> list = new HashMap<String,ArrayList<String>>();
        for(String str: strs) {
            char[] arr = str.toCharArray();
            Arrays.sort(arr);
            String s = String.valueOf(arr);
            if(!list.containsKey(s)) list.put(s,new ArrayList<String>());
            list.get(s).add(str);
        }
        return new ArrayList<List<String>>(list.values());
    }
}
```

##### Date 2020.3.26