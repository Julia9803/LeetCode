### 874. Walking Robot Simulation

A robot on an infinite grid starts at point (0, 0) and faces north. The robot can receive one of three possible types of commands:

- `-2`: turn left 90 degrees
- `-1`: turn right 90 degrees
- `1 <= x <= 9`: move forward `x` units

Some of the grid squares are obstacles. 

The `i`-th obstacle is at grid point `(obstacles[i][0], obstacles[i][1])`

If the robot would try to move onto them, the robot stays on the previous grid square instead (but still continues following the rest of the route.)

Return the **square** of the maximum Euclidean distance that the robot will be from the origin.

 

**Example 1:**

```
Input: commands = [4,-1,3], obstacles = []
Output: 25
Explanation: robot will go to (3, 4)
```

**Example 2:**

```
Input: commands = [4,-1,4,-2,4], obstacles = [[2,4]]
Output: 65
Explanation: robot will be stuck at (1, 4) before turning left and going to (1, 8)
```

####  Solution:

```java
//my own way
class Solution {
    private int max = 0;
    public int robotSim(int[] commands, int[][] obstacles) {
        int direction = 0; // 0 north 1 east 2 south 3 west
        int res = 0;
        int[] spot = {0,0};
        for(int i = 0;i<commands.length;i++) {
            if(commands[i] > 0) {
                spot = checkObstacle(direction, commands[i], spot, obstacles);
                // System.out.println(spot[0] + " " + spot[1]); 
            } else if(commands[i] == -1) {
                if(direction != 3) direction++;
                else direction = 0;
            } else if(commands[i] == -2) {
                if(direction != 0) direction--;
                else direction = 3;
            }
        }
        return max;
    }
    
    public int[] checkObstacle(int direction, int step, int[] spot, int[][] obstacles) {
        int[] res = {0,0};
        int[] each;
        int[] nearObs = null;
        boolean hasObs = false;

        if(direction == 0) {
            for(int i = 0;i<obstacles.length;i++) {
                each = obstacles[i];
                if(each[0] == spot[0] && each[1] <= (spot[1] + step) && each[1] > spot[1]) {
                    hasObs = true;
                    if(nearObs == null) nearObs = each;
                    else if(each[1] < nearObs[1]) {
                        nearObs = each;
                    }
                }
            }
            if(hasObs) {
                res[0] = nearObs[0];
                res[1] = nearObs[1] - 1;
            } else {
                res[0] = spot[0];
                res[1] = spot[1] + step;
            }
        } else
        if(direction == 1) {
            for(int i = 0;i<obstacles.length;i++) {
            each = obstacles[i];
            if(each[1] == spot[1] && each[0] <= (spot[0] + step) && each[0] > spot[0]) {
                hasObs = true;
                if(nearObs == null) nearObs = each;
                    else if(each[0] < nearObs[0]) {
                        nearObs = each;
                    }
                }
            }
            if(hasObs) {
                res[1] = nearObs[1];
                res[0] = nearObs[0] - 1;
            } else {
                res[1] = spot[1];
                res[0] = spot[0] + step;
            }
        } else
        if(direction == 2) {
            for(int i = 0;i<obstacles.length;i++) {
            each = obstacles[i];
            if(each[0] == spot[0] && each[1] >= (spot[1] - step) && each[1] < spot[1]) {
                hasObs = true;
                if(nearObs == null) nearObs = each;
                    else if(each[1] > nearObs[1]) {
                        nearObs = each;
                    }
                }
            }
            if(hasObs) {
                res[0] = nearObs[0];
                res[1] = nearObs[1] + 1;
            } else {
                res[0] = spot[0];
                res[1] = spot[1] - step;
            }
        } else
        if(direction == 3) {
            for(int i = 0;i<obstacles.length;i++) {
            each = obstacles[i];
            if(each[1] == spot[1] && each[0] >= (spot[0] - step) && each[0] < spot[0]) {
                hasObs = true;
                if(nearObs == null) nearObs = each;
                    else if(each[0] > nearObs[0]) {
                        nearObs = each;
                    }
                }
            }
            if(hasObs) {
                res[1] = nearObs[1];
                res[0] = nearObs[0] + 1;
            } else {
                res[1] = spot[1];
                res[0] = spot[0] - step;
            }
        }
        // calculate 
        int now = (int)Math.pow(res[0],2) + (int)Math.pow(res[1],2);
        if(now > max) max = now;
        
        return res;
    }
}
```

```java
// others solution
class Solution {    
    public int robotSim(int[] commands, int[][] obstacles) {
        Set<String> set = new HashSet<>(); // put obstacle
        int[][] dirMapping = new int[][]{{0,1},{1,0},{0,-1},{-1,0}}; // two dimentional array init
        int direction = 0;
        int res = 0;
        int x = 0;
        int y = 0;
        
        for(int[] each: obstacles) {
            set.add(each[0] + " " + each[1]);
        }
        
        for(int c: commands) {
            if(c == -1) {
                direction++;
                if(direction == 4) direction = 0;
            }
            if(c == -2) {
                direction--;
                if(direction == -1) direction = 3;
            }
            while(c-- > 0 && !set.contains((x + dirMapping[direction][0]) + " " + (y + dirMapping[direction][1]))) { // see if there is an obstacle foward
                x += dirMapping[direction][0];
                y += dirMapping[direction][1];
            }
            res = Math.max(res, (int)Math.pow(x,2) + (int)Math.pow(y,2));
        }
        return res;
    }
}
```

##### Date 2020.2.18

