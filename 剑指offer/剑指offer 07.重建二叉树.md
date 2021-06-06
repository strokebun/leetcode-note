### 剑指offer 07.重建二叉树

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

``` markdown
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]

    3
   / \
  9  20
    /  \
   15   7
```

**思路：** 递归

前序遍历的第一个节点为根节点，再中序遍历序列找到该节点，在此之前的节点均位于根的左子树，之后的节点位于根的右子树。使用哈希表存储中序遍历序列以其下标降低复杂度。

``` java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    Map<Integer, Integer> map;
    int[] preorder;

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.preorder = preorder;
        map = new HashMap<>();
        int n = inorder.length;
        for (int i = 0; i < n; i++) {
            map.put(inorder[i], i);
        }
        return dfs(0, n-1, 0, n-1);
    }

    private TreeNode dfs(int pl, int pr, int il, int ir) {
        if (pl > pr) {
            return null;
        }
        TreeNode root = new TreeNode(preorder[pl]);
        int k = map.get(preorder[pl]);
        root.left = dfs(pl+1, pl+k-il, il, k-1);
        root.right = dfs(pl+k-il+1, pr, k+1, ir);
        return root;
    }


}
```

