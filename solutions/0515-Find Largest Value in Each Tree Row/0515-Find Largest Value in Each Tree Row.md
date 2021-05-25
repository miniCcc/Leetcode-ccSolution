### 0515. 在每个树行中找最大值

#### 题目地址：https://leetcode-cn.com/problems/find-largest-value-in-each-tree-row/

您需要在二叉树的每一行中找到最大的值。

**示例：**

```
输入: 

          1
         / \
        3   2
       / \   \  
      5   3   9 

输出: [1, 3, 9]
```

---

**Java**

```java
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
    Queue<TreeNode> queue = new LinkedList<>();
    List<Integer> res = new ArrayList<>();
    public List<Integer> largestValues(TreeNode root) {
        if(root == null) return res;
        queue.offer(root);
        helper();
        return res;
    }
    // 层次遍历
    public void helper(){
        while(!queue.isEmpty()){
            int size = queue.size();
            int max = Integer.MIN_VALUE;
            for(int i = 0; i < size; i++){
                TreeNode temp = queue.poll();
                if(max < temp.val) max = temp.val;
                if(temp.left != null) queue.offer(temp.left);
                if(temp.right != null) queue.offer(temp.right);
            }
            res.add(max);
        }
    }
}
```

