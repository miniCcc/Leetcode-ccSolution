### 437. 路径总和

#### 题目地址：https://leetcode-cn.com/problems/path-sum-iii/

给定一个二叉树，它的每个结点都存放着一个整数值。

找出路径和等于给定数值的路径总数。

路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。

**示例：**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

返回 3。和等于 8 的路径有:

1.  5 -> 3
2.  5 -> 2 -> 1
3.  -3 -> 11
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
    Map<Integer, Integer> map = new HashMap<>();
    int target = 0;
    public int pathSum(TreeNode root, int sum) {
        target = sum;
        map.put(0, 1);
        return recur(root, 0);
    }
    public int recur(TreeNode node, int curSum){
        if(node == null) return 0;
        int res = 0;
        curSum += node.val;
        res += map.getOrDefault(curSum - target, 0);
        map.put(curSum, map.getOrDefault(curSum, 0) + 1);

        int left = recur(node.left, curSum);
        int right = recur(node.right, curSum);

        // 撤销选择
        map.put(curSum, map.get(curSum) - 1);

        res += left + right;
        return res;
    }
}
```

直接看leetcode题解：

- https://leetcode-cn.com/problems/path-sum-iii/solution/qian-zhui-he-di-gui-hui-su-by-shi-huo-de-xia-tian/
- https://leetcode-cn.com/problems/path-sum-iii/solution/dui-qian-zhui-he-jie-fa-de-yi-dian-jie-s-dey6/

两个结合在一起看，至此特地说明一下困扰我的一个问题，这种解法如何避免重复的问题？

```
    5
   /
  3
 / \
2   -2
```

对于路径 [5, 3, 2] 和 [5, 3, -2]，sum=8的情况下，应该只有1条路径，而不应该是2条

在这种解法当中，用了一个变量`curSum`，`curSum`代表从根节点到当前这个节点，有没有符合条件的路径，但是需要注意的是，**一定得包含当前这个节点**，比如：

对于 [5, 3, 2] 这个路径，我们一定是要去找：

- 2
- 2 -> 3
- 2 -> 3- > 5

这样的话一定是没有重复的，而不是去找：

- 5
- 5 -> 3
- 5 -> 3 -> 2

如果是这样的话，那么则会重复计算

