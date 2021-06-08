### 剑指offer 44.数字序列中某一位的数字

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

``` markdown
输入：n = 3
输出：3

输入：n = 11
输出：0
```

**思路：** 找规律

每一个 `digit` 位数的起始值为 `start`（2 位数的起始值为 10），共有 `9 * start` 个数字（10-99 共有 90 个数字），这些数字位数为 `9*start*digit`。故通过该范围确定第 `n` 位数属于几位数，位于哪个数字。

``` java
class Solution {
    public int findNthDigit(int n) {
        int digit = 1;
        long start = 1, count = 9;
        while (n > count) {
            n -= count;
            start *= 10;
            digit++;
            count = start * digit * 9;
        } 
        // n-1的原因是序列从0开始
        long num = start + (n-1)/digit;
        return Long.toString(num).charAt((n-1) % digit) - '0';
    }
}
```

