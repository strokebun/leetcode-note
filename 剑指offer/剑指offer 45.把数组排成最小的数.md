### 剑指offer 45.把数组排成最小的数

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

``` markdown
输入: [10,2]
输出: "102"

输入: [3,30,34,5,9]
输出: "3033459"
```

提示:

- 0 < nums.length <= 100

说明：

- 输出结果可能非常大，所以你需要返回一个字符串而不是整数
- 拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0



**思路：** 自定义排序

将数组中的整数转换为字符串之后，对该数组进行排序，排序规则：要使最后的数字最小，那么对于字符串 `x`  和 `y`，

如果 `x + y < y + x`，则 `x` 应该排在 `y` 的前面。数组排序之后进行拼接即可。

``` java 
class Solution {
    public String minNumber(int[] nums) {
        int n = nums.length;
        String[] strs = new String[n];
        for (int i = 0; i < n; i++) {
            strs[i] = String.valueOf(nums[i]);
        }
        Arrays.sort(strs, (String a, String b) -> {
            return (a + b).compareTo(b+a);
        });
        StringBuilder sb = new StringBuilder();
        for (String str : strs) {
            sb.append(str);
        }
        return sb.toString();
    }
}
```