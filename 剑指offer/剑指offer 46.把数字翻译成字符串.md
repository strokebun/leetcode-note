### 剑指offer 46.把数字翻译成字符串

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

``` markdown
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

**思路：** 动态规划

设 `dp[i]` 为以第 `i` 位数结尾的翻译个数，可以得到状态转移方程

`dp[i] = dp[i-2] + dp[i-1], 最近两个数可以进行翻译`

`dp[i] = dp[i-1], 无法翻译`

状态初值 `dp[0] = 1`

``` java
class Solution {
    public int translateNum(int num) {
        String s = String.valueOf(num);
        char[] ch = s.toCharArray();
        int[] dp = new int[ch.length];
        dp[0] = 1;
        for(int i = 1; i < ch.length;i++){
            dp[i] = dp[i - 1];
            int cur = (ch[i - 1] - '0' ) * 10 + (ch[i] - '0');
            if(cur > 9 && cur < 26){
                if(i - 2 < 0){
                    dp[i]++;
                }else{
                    dp[i] += dp[i - 2];
                }
            }
        }
        return dp[dp.length - 1];
    }
}
```

