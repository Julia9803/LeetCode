### 34. Find First and Last Position of Element in Sorted Array

Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

If the target is not found in the array, return `[-1, -1]`.

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

**Example 2:**

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

#### Solution:

A change form of binary search.

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if(nums.length == 0) return new int[]{-1,-1};
        int first = getNext(nums, target);
        if(first == nums.length || nums[first] != target) return new int[]{-1,-1};
        int last = getNext(nums, target + 1) - 1;
        return new int[]{first, last};
    }
    
    public int getNext(int[] nums, int target) {
        int lo = 0, hi = nums.length; // tricky
        while(lo < hi) {
            int mid = (lo + hi)/2;
            // System.out.println(mid + " " + nums[mid]);
            if(target > nums[mid]) lo = mid + 1;
            // wrong statement below because it may returns not the first or last
            // else if(target == nums[mid]) return mid;
            // else hi = mid - 1;
            else hi = mid;
        }
        return lo;
    }
}
```

Traditional binary search.

```java
package com.company;

public class Main {

    public static void main(String[] args) {
        int[]a = {1,2,3,4,5};
        int key = 6;

        int res = binarySearch(a, key);
        System.out.print(res);
    }

    private static int binarySearch(int[] a, int key) {
        int lo = 0, hi = a.length - 1;
        while(lo <= hi) {
            int mid = (lo + hi)/2;
            if(key == a[mid]) return mid;
            if(key > a[mid]) lo = mid + 1;
            else hi = mid - 1;
        }
        return -1;
    }
}
```

##### Date 2020.3.15