### 1232. Check If It Is a Straight Line

You are given an array `coordinates`, `coordinates[i] = [x, y]`, where `[x, y]` represents the coordinate of a point. Check if these points make a straight line in the XY plane.

 

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/10/15/untitled-diagram-2.jpg)

```
Input: coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]]
Output: true
```

**Example 2:**

**![img](https://assets.leetcode.com/uploads/2019/10/09/untitled-diagram-1.jpg)**

```
Input: coordinates = [[1,1],[2,2],[3,4],[4,5],[5,6],[7,7]]
Output: false
```

 

**Constraints:**

- `2 <= coordinates.length <= 1000`
- `coordinates[i].length == 2`
- `-10^4 <= coordinates[i][0], coordinates[i][1] <= 10^4`
- `coordinates` contains no duplicate point.

#### Solution:

```java
// (x1y2-x2y1)+(x2y3-x3y2)+(x3y1-y3x1)==0
class Solution {
    public boolean checkStraightLine(int[][] coordinates) {
        if(coordinates.length == 2) return true;
        
        int pointAX = coordinates[0][0];
        int pointAY = coordinates[0][1];
        int pointBX = coordinates[1][0];
        int pointBY = coordinates[1][1];
        int pointCX = 0;
        int pointCY = 0;
        
        for(int i = 2;i < coordinates.length;i++) {
            pointCX = coordinates[i][0];
            pointCY = coordinates[i][1];
            int val = pointAX * pointBY - pointAY * pointBX + pointBX * pointCY - pointBY * pointCX + pointCX * pointAY - pointCY * pointAX;
            if(val != 0) return false;
        }
        return true;
    }
}
```

##### Date 2020.5.8