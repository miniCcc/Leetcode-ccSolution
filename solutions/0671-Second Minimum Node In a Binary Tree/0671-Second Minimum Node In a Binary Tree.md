### 0671-二叉树中第二小的节点

#### 题目地址：https://leetcode-cn.com/problems/second-minimum-node-in-a-binary-tree/

给定一个非空特殊的二叉树，每个节点都是正数，并且每个节点的子节点数量只能为 2 或 0。如果一个节点有两个子节点的话，那么该节点的值等于两个子节点中较小的一个。

更正式地说，root.val = min(root.left.val, root.right.val) 总成立。

给出这样的一个二叉树，你需要输出所有节点中的**第二小的值**。如果第二小的值不存在的话，输出 -1 。

**示例 1：**

![img](smbt1.jpg)

```
输入：root = [2,2,5,null,null,5,7]
输出：5
解释：最小的值是 2 ，第二小的值是 5 。
```

**示例 2：**

![img](smbt2.jpg)

```
输入：root = [2,2,2]
输出：-1
解释：最小的值是 2, 但是不存在第二小的值。
```

**提示：**

- 树中节点数目在范围 [1, 25] 内
- 1 <= Node.val <= 231 - 1
- 对于树中每个节点 root.val == min(root.left.val, root.right.val)

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
    long firval = Long.MAX_VALUE; // 最小的值
    long secval = Long.MAX_VALUE; // 第二小的值
    public int findSecondMinimumValue(TreeNode root) {
        dfs(root);
        System.out.println("firval : " + firval + ", secval : " + secval);
        return secval == Long.MAX_VALUE ? -1 : (int) secval;
    }

    public void dfs(TreeNode node){
        if(node == null) return;
        if(node.val < firval){
            secval = firval;
            firval = node.val;
        }
        if(node.val > firval && node.val < secval) secval = node.val;
        dfs(node.left);
        dfs(node.right);
    }
}
```

不得不说`[2,2,2147483647]`这个测试用例也太恶心了，还好没有添加`Long.MAX_VALUE`进去，一把辛酸泪,,,,,,