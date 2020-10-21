### 二叉树的序列化与反序列化

题目地址：https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/

序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

**示例:** 

你可以将以下二叉树：

        1
       / \
      2   3
         / \
        4   5

序列化为 "[1,2,3,null,null,4,5]"

---

**Java**

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
    String SEP = ",";
    String NULL =  "null";  

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        // 使用StringBuilder是因为速度更快
        StringBuilder sb = new StringBuilder();
        serialize(root, sb);
        return sb.toString();
    }

    void serialize(TreeNode root, StringBuilder sb){     
        if(root == null){
            sb.append(NULL).append(SEP);
            return;
        }
        // 先序遍历
        sb.append(root.val).append(SEP);
        
        serialize(root.left, sb);
        serialize(root.right, sb);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        LinkedList<String> list = new LinkedList<>();
        for(String str : data.split(SEP)){
            list.addLast(str);
        }
        return deserializeHelper(list);
    }

    TreeNode deserializeHelper(LinkedList<String> list){
        // 判断序列是否为空
        if(list.isEmpty()) return null;
        // 子序列第一个即为当前的根节点,并从list序列中移除
        String firstnode = list.removeFirst();
        if(firstnode.equals("null")) return null;
        // 先序遍历
        // 创建该结点
        TreeNode node = new TreeNode(Integer.parseInt(firstnode));

        node.left = deserializeHelper(list);
        node.right = deserializeHelper(list);

        return node;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// TreeNode ans = deser.deserialize(ser.serialize(root));
```





