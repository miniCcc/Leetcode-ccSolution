### 113. 路径总和 II

#### 题目地址：https://leetcode-cn.com/problems/path-sum-ii/

给你二叉树的根节点 root 和一个整数目标和 targetSum ，找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径。

叶子节点 是指没有子节点的节点。

 

**示例 1：**

![img](pathsumii1.jpg)

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
```

**示例 2：**

![img](pathsum2.jpg)

```
输入：root = [1,2,3], targetSum = 5
输出：[]
```

**示例 3：**

```
输入：root = [1,2], targetSum = 0
输出：[]
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
    List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<Integer> list = new ArrayList<>();
        backtrace(list, root, targetSum);
        return res;
    }
    public void backtrace(List<Integer> list, TreeNode node, int sum){
        if(node == null) return;
        list.add(node.val);
        if(sum == node.val && node.left == null && node.right == null){
            res.add(new ArrayList<>(list));
            // return;   不能加return，否则会多一个节点，假若现在在第四层，return后回到了第三层，但是此时第四层的结点需要舍去，没有经历remove,则会多出来
        }
        // 这里用的是减法，但是用加法也一样
        backtrace(list, node.left, sum - node.val);
        backtrace(list, node.right, sum - node.val);
        list.remove(list.size() - 1);
    }
}
```

- 注意，不能加剪枝操作，因为结点值可能为负数