### 剑指offer 66.构建乘积数组

给定一个数组 `A[0,1,…,n-1]`，请构建一个数组 `B[0,1,…,n-1]`，其中 `B[i]` 的值是数组 `A` 中除了下标 `i` 以外的元素的积, 即 `B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]`。不能使用除法。

``` markdown
输入: [1,2,3,4,5]
输出: [120,60,40,30,24]
```

**提示：**

- 所有元素乘积之和不会溢出 32 位整数
- `a.length <= 100000`



**思路：** 前缀积 + 后缀积

分别记录前缀积和后缀积，再构建乘积数组。

``` java
class Solution {
    public int[] constructArr(int[] a) {
        int n = a.length;
        int[] prefix = new int[n+1];
        prefix[0] = 1;
        for (int i = 1; i < n; i++) {
            prefix[i] = prefix[i-1] * a[i-1];
        }

        int[] suffix = new int[n+1];
        suffix[n] = 1;
        for (int i = n-1; i >= 0; i--) {
            suffix[i] = suffix[i+1] * a[i];
        }

        int[] ans = new int[n];
        for (int i = 0; i < n; i++) {
            ans[i] = prefix[i] * suffix[i+1];
        }
        return ans;
    }
}
```

