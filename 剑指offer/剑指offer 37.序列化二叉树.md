### 剑指offer 37.序列化二叉树

请实现两个函数，分别用来序列化和反序列化二叉树。



**思路：** dfs

根据先序遍历的顺序进行序列化，反序列化时先解析左子树，再解析右子树即可。

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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        return serialize(root, "");
    }

    private String serialize(TreeNode root, String str) {
        if (root == null) {
            str += "null,";
        } else {
            str = str + String.valueOf(root.val) + ",";
            str = serialize(root.left, str);
            str = serialize(root.right, str); 
        }
        return str;
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String str) {
        String[] arr = str.split(",");
        List<String> data = new LinkedList<>(Arrays.asList(arr));
        return deserialize(data);
    }

    private TreeNode deserialize(List<String> data) {
        if (data.get(0).equals("null")) {
            data.remove(0);
            return null;
        }
        TreeNode node = new TreeNode(Integer.valueOf(data.get(0)));
        data.remove(0);
        node.left = deserialize(data);
        node.right = deserialize(data);
        return node;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

