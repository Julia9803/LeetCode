### 75. Sort Colors

Given an array with *n* objects colored red, white or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

**Note:** You are not suppose to use the library's sort function for this problem.

**Example:**

```
Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

**Follow up:**

- A rather straight forward solution is a two-pass algorithm using counting sort.
  First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.
- Could you come up with a one-pass algorithm using only constant space?

#### Solution:

Method1: It's like quick sort but to sort in three types. Use two pointers, one from front to back, one from back to front, one curr to point to the current index. If it is 0, then the values of pointer1 and curr are swap, pointer1 + +. If it is 2pointer 2 and curr, then the values of swap, pointer --, curr -- (curr here means that pointer1 needs to be compared again, if it is 0, then it needs to be swap again with pointer1). If it is 1, then curr + +.
Method2: Another method is too simple. Traverse the first time to find the number of 0, 1 and 2 respectively, and then traverse the fill again.

```java
class Solution {
    // 1-pass
    public void sortColors(int[] nums) {
        int p1 = 0, p2 = nums.length - 1, curr = 0;
        while(curr <= p2) {
            if(nums[curr] == 0) {
                nums[curr] = nums[p1];
                nums[p1] = 0;
                p1++;
            }
            if(nums[curr] == 2) {
                nums[curr] = nums[p2];
                nums[p2] = 2;
                p2--;
                curr--;
            }
            curr++;
        }
    }
}
```

```java
class Solution {    
    // 2-pass
    public void sortColors(int[] nums) {
        int num0 = 0,num1 = 0,num2 = 0;
        for(int i = 0;i<nums.length;i++) {
            if(nums[i] == 0) num0++;
            else if(nums[i] == 1) num1++;
            else if(nums[i] == 2) num2++;
        }
        for(int i = 0;i<nums.length;i++) {
            if(i<num0) nums[i] = 0;
            else if(i<num0 + num1) nums[i] = 1;
            else if(i<num0 + num1 + num2) nums[i] = 2;
        }
    }
}
```

##### Date 2020.3.28