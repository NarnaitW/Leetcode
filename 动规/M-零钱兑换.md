# [零钱兑换](https://leetcode-cn.com/problems/coin-change/)

## Java
```java
public static int coinChange(int[] coins, int amount) {
    int[] dp=new int[amount+1];
    dp[0]=0;
    for(int i=1;i<amount+1;i++) {
        dp[i] = Integer.MAX_VALUE;
        for (int j = 0; j < coins.length; j++) {
            if (i - coins[j] < 0) {
                continue;
            }
            if (dp[i - coins[j]] >= 0) {
                dp[i] = dp[i] < (dp[i - coins[j]] + 1) ? dp[i] : dp[i - coins[j]] + 1;
            }
        }
        dp[i] = dp[i] != Integer.MAX_VALUE ? dp[i] : -1;
    }
    return dp[amount];
}
```
