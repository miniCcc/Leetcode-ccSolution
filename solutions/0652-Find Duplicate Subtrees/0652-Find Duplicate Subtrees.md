### 652. 寻找重复的子树

#### 题目地址：https://leetcode-cn.com/problems/find-duplicate-subtrees/

给定一棵二叉树，返回所有重复的子树。对于同一类的重复子树，你只需要返回其中任意一棵的根结点即可。

两棵树重复是指它们具有相同的结构以及相同的结点值。

**示例 1：**

```
        1
       / \
      2   3
     /   / \
    4   2   4
       /
      4
```

下面是两个重复的子树：

```
      2
     /
    4
```

和

```
    4
```

因此，你需要以列表的形式返回上述重复子树的根结点。

---

**Java**

``` java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    List<TreeNode> res = new ArrayList<>();
    Map<String, Integer> map = new HashMap<>();
    public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
        if(root == null) return res;
        helper(root);
        return res;
    }

    public StringBuilder helper(TreeNode node){
        // 以#代表结束
        if(node == null) return new StringBuilder("#");
        StringBuilder left = helper(node.left);
        StringBuilder right = helper(node.right);

        StringBuilder sb = new StringBuilder();
        sb.append(node.val).append(",").append(left).append(",").append(right);
        int num = map.getOrDefault(sb.toString(), 0);
        if(num == 1) res.add(node);
        map.put(sb.toString(), num + 1);
        return sb;
    }
}
```

以序列化的方式去表示一个二叉树

