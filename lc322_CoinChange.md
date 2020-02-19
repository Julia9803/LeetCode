### 322. Coin Change

You are given coins of different denominations and a total amount of money *amount*. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

**Example 1:**

```
Input: coins = [1, 2, 5], amount = 11
Output: 3 
Explanation: 11 = 5 + 5 + 1
```

**Example 2:**

```
Input: coins = [2], amount = 3
Output: -1
```

#### Solution:

```java
// dp
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] list = new int[amount+1];
        Arrays.fill(list,amount+1);
        list[0] = 0;
        
        for(int i = 1;i <= amount;i++) {//iterate buckets
            for(int j = 0;j < coins.length; j++) {//iterate coins
                if(coins[j] <= i) {// each coin need to be smaller than sum
                    list[i] = Math.min(list[i], list[i-coins[j]] + 1);// find smaller amount
                }
            }
        }
        return list[amount] == amount+1 ? -1: list[amount];
    }
}
```

```java
class Solution {
    public int coinChange(int[] coins, int amount) {        
        // recursive
        int[] count = new int[amount];
        if(amount < 1) return 0;
        return coinChange(coins, amount, count);
    }
    
    public int coinChange(int[] coins, int rem, int[] count) {
        if(rem == 0) return 0;
        if(rem < 0) return -1;
        if(count[rem-1] != 0) return count[rem-1];
        int min = Integer.MAX_VALUE;
        for(int c: coins) {
            int res = coinChange(coins, rem-c, count);
            if(res >= 0 && res < min) {
                min = res + 1;
            }
        }
        count[rem-1] = (min == Integer.MAX_VALUE) ? -1: min;
        return count[rem-1];
    }
}
```



##### Date 2020.2.19