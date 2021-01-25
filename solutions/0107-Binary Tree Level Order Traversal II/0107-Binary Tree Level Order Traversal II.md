### 题目地址：https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/

给定一个二叉树，返回其节点值自底向上的层序遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

**例如：**
给定二叉树 [3,9,20,null,null,15,7],

        3
       / \
      9  20
        /  \
       15   7
返回其自底向上的层序遍历为：

```
[
  [15,7],
  [9,20],
  [3]
]
```

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
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        if (root == null) return res;
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            List<Integer> list = new ArrayList<Integer>();
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                list.add(node.val);
                if(node.left != null) queue.offer(node.left);
                if(node.right != null) queue.offer(node.right);
            }
            // 头插法
            res.add(0, list);
        }
        return res;
    }
    
}
```

这个题和102很类似，也就是最终结果顺序不同而已，可以在102的基础上反转一下，也可以像上面这样使用头插法，如果像上面这个写法，最后在`res.add(0, list)`才可以通过，而不能写`res.addFirst(list)`，但是可以这样用：

```java
LinkedList<List<Integer>> res = new LinkedList<List<Integer>>();
.....
res.addFirst(list);
```

