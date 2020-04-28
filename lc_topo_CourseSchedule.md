### 207. Course Schedule

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, is it possible for you to finish all courses?

 

**Example 1:**

```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
```

**Example 2:**

```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
```

 

**Constraints:**

- The input prerequisites is a graph represented by **a list of edges**, not adjacency matrices. Read more about [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs).
- You may assume that there are no duplicate edges in the input prerequisites.
- `1 <= numCourses <= 10^5`

#### Solution:

```java
class Solution {
    List<Integer>[] loop;
    int[] status;
    
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        loop = new List[numCourses];// topo
        status = new int[numCourses];// 1:visited 2:visiting 0:not marked
        for(int i = 0;i < numCourses;i++) {
            loop[i] = new LinkedList<Integer>();
        }
        for(int[] pre: prerequisites) {
            loop[pre[1]].add(pre[0]);
        }
        for(int i = 0;i < numCourses;i++) {
            if(status[i] == 0) {
                if(dfs(i) == false) return false;
            }
        }
        return true;
    }
    private boolean dfs(int i) {
        if(status[i] == 2) return false;// loop
        if(status[i] == 1) return true;// not loop
        status[i] = 2;
        for(int n = 0;n < loop[i].size();n++) {
            if(dfs(loop[i].get(n)) == false) return false;// loop
        }
        status[i] = 1;
        return true;
    }
}
```

##### Date 2020.4.29