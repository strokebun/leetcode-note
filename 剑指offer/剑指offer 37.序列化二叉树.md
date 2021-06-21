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
        StringBuilder sb = new StringBuilder();
        serialize(root, sb);
        return sb.toString();
    }

    private void serialize(TreeNode root, StringBuilder sb) {
        if (root == null) {
            sb.append("null,");
        } else {
            sb.append(String.valueOf(root.val) + ",");
            serialize(root.left, sb);
            serialize(root.right, sb);
        }
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] arr = data.split(",");
        List<String> list = new LinkedList<>(Arrays.asList(arr));
        return deserialize(list);
    }

    private TreeNode deserialize(List<String> list) {
        String str = list.get(0);
        if (str.equals("null")) {
            list.remove(0);
            return null;
        }
        TreeNode node = new TreeNode(Integer.valueOf(str));
        list.remove(0);
        node.left = deserialize(list);
        node.right = deserialize(list);
        return node;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// TreeNode ans = deser.deserialize(ser.serialize(root));

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

