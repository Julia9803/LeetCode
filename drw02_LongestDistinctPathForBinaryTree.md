### Longest Distinct Path for Binary Tree

![img](https://i.ibb.co/B4BTn4N/2020-09-06-4-55-43.png)

```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");
import java.util.*;

class Solution {
    Map<Integer, Integer> map; // node value, length
    public int solution(Tree node) {
        // write your code in Java SE 8
        map = new HashMap<Integer, Integer>();
        if(node == null) return 0;
        int res = dfs(node);
        return res;
    }
    public int dfs(Tree node) {
        if(node == null) return map.size();
        int t;
        if(!map.containsKey(node.x))
            map.put(node.x, 0);
        map.put(node.x, map.get(node.x)+1);
        if(map.get(node.x) > 1) {
            map.put(node.x, map.get(node.x)-1);
            return map.size();
        }
        int max = Math.max(dfs(node.l),dfs(node.r));
        map.put(node.x, map.get(node.x)-1);
        if(map.get(node.x) == 0)
            map.remove(node.x);
        return max;
    }
}
```

##### Date 2020.9.6