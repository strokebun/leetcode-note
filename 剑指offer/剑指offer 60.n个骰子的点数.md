### 剑指offer 60.n个骰子的点数

把n个骰子扔在地上，所有骰子朝上一面的点数之和为s。输入n，打印出s的所有可能的值出现的概率。 

你需要用一个浮点数数组返回答案，其中第 i 个元素代表这 n 个骰子所能掷出的点数集合中第 i 小的那个的概率。

``` markdown
输入: 1
输出: [0.16667,0.16667,0.16667,0.16667,0.16667,0.16667]

输入: 2
输出: [0.02778,0.05556,0.08333,0.11111,0.13889,0.16667,0.13889,0.11111,0.08333,0.05556,0.02778]
```

**思路：** 动态规划

投掷总数为 `6^n`，问题的关键是求出每个点数对应的情况个数。

定义 `dp[i][j]` 为 `i` 个骰子和为 `j` 的情况数，可以得到状态转移方程

`dp[i][j] = sum(dp[i-1][j-k]), k=1-6`，状态初值为 `dp[1][i] = 1, i=1-6`

``` java
class Solution {
    public double[] dicesProbability(int n) {
        int[][] dp = new int[n+1][6*n+1];
        for (int i = 1; i <= 6; i++) {
            dp[1][i] = 1;
        }
        for (int i = 2; i <= n; i++) {
            for (int j = i; j <= 6*n; j++) {
                for (int k = 1; k <= 6; k++) {
                    if (j <= k) {
                        break;
                    }
                    dp[i][j] += dp[i-1][j-k];
                }
            }
        }
        double all = Math.pow(6, n);
        int start = n, end = 6*n;
        double[] ans = new double[end - start + 1];
        for (int i = 0; i < ans.length; i++) {
            ans[i] = dp[n][i+start] * 1.0 / all;
        }
        return ans;
    }
}
```

