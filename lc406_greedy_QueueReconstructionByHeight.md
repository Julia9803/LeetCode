### 406. Queue Reconstruction by Height

Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers `(h, k)`, where `h` is the height of the person and `k` is the number of people in front of this person who have a height greater than or equal to `h`. Write an algorithm to reconstruct the queue.

**Note:**
The number of people is less than 1,100.

 

**Example**

```
Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```

####  Solution:

```java
// input [[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]
/** 
Arrays.sort(),重载排序，<0 -》正序，>0 -》逆序
List接口中的add方法有如下两种重载方式：
        ① boolean add(E e);
        ② void add(int index, E element); // add element to index regardless of others position
*/
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        Arrays.sort(people, (a, b) -> (a[0] == b[0]) ? a[1] - b[1] : b[0] - a[0]);
        // [[7,0],[7,1],[6,1],[5,0],[5,2],[4,4]]
        List<int[]> res = new LinkedList<>();
        for(int[] p: people) res.add(p[1], p);
        return res.toArray(new int[people.length][2]);
    }
}
```

##### Date 2020.5.12