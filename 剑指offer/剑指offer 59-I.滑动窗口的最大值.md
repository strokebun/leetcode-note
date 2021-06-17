### 剑指offer 59-I.滑动窗口的最大值

给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

``` markdown
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**思路：** 单调队列

单调栈实现了 O(1) 时间获取最小值的操作，类比该思想，滑动窗口操作的是列表头部元素，对应双端队列。故使用双端队列实现单调队列，维护队列单调递减，队列头部元素即为滑动窗口的最大值。滑动窗口最左侧的元素等于单调队列头部时，再将该元素从队列中删除。

``` java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k == 0) {
            return new int[0];
        }
        Deque<Integer> dq = new LinkedList<>();
        int n = nums.length;
        int[] ans = new int[n - k + 1];
        for (int i = 0; i < k; i++) {
            while (!dq.isEmpty() && dq.peekLast() < nums[i]) {
                dq.removeLast();
            }
            dq.addLast(nums[i]);
        }
        ans[0] = dq.peekFirst();
        for (int i = k; i < n; i++) {
            if (!dq.isEmpty() && nums[i-k] == dq.peekFirst()) {
                dq.removeFirst();
            }
            while (!dq.isEmpty() && dq.peekLast() < nums[i]) {
                dq.removeLast();
            }
            dq.addLast(nums[i]);
            ans[i-k+1] = dq.peekFirst();
        }
        return ans;
    }
}
```

