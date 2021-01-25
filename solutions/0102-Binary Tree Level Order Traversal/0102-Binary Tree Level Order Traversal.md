### 题目地址：https://leetcode-cn.com/problems/binary-tree-level-order-traversal/

给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

**示例：**
二叉树：[3,9,20,null,null,15,7],

      3
     / \
      9  20
        /  \
       15   7
返回其层序遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        Queue<TreeNode> queue = new LinkedList<>();
        // 加入根节点
        queue.offer(root);
        while(!queue.isEmpty()){
            List<Integer> list = new ArrayList<>();
            int count = queue.size();
            while(count != 0){
                TreeNode temp = queue.poll();
                list.add(temp.val);
                if(temp.left != null) queue.offer(temp.left);
                if(temp.right != null) queue.offer(temp.right);
                count--;
            }
            res.add(list);
        }
        return res;
    }
}
```

