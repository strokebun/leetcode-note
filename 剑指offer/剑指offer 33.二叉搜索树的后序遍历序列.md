### 剑指offer 33.二叉搜索树的后序遍历序列

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

``` markdown
     5
    / \
   2   6
  / \
 1   3
 
输入: [1,6,3,2,5]
输出: false

输入: [1,3,2,6,5]
输出: true
```

**思路：** 递归

后序遍历序列的最后一个元素即为树的根 `root` ，要满足二叉搜索树的性质，则将该序列分为两部分，前半部分元素都小于 `root`，后半部分元素都大于 `root`，递归判断每棵子树。

``` java
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        return dfs(postorder, 0, postorder.length-1);
    }

    private boolean dfs(int[] postorder, int left, int right) {
        if (left >= right) {
            return true;
        }
        int root = postorder[right];
        int index = left;
        while (index < right && postorder[index] < root) {
            index++;
        }
        for (int i = index; i < right; i++) {
            if (postorder[i] < root) {
                return false;
            }
        }
        return dfs(postorder, left, index-1) && dfs(postorder, index, right-1);
    }
}s
```

