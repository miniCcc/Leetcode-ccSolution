### 0508. 出现次数最多的子树元素和

#### 题目地址：https://leetcode-cn.com/problems/most-frequent-subtree-sum/

给你一个二叉树的根结点，请你找出出现次数最多的子树元素和。一个结点的「子树元素和」定义为以该结点为根的二叉树上所有结点的元素之和（包括结点本身）。

你需要返回出现次数最多的子树元素和。如果有多个元素出现的次数相同，返回所有出现次数最多的子树元素和（不限顺序）。



**示例 1：**
输入:

```
   5
 /  \
2   -3
```

返回 [2, -3, 4]，所有的值均只出现一次，以任意顺序返回所有值。

**示例 2：**
输入：

```
   5
 /  \
2   -5
```

返回 [2]，只有 2 出现两次，-5 只出现 1 次。

**提示：** 假设任意子树元素和均可以用 32 位有符号整数表示。

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
    Map<Integer, Integer> map = new HashMap<>();
    int maxcount = -1;
    public int[] findFrequentTreeSum(TreeNode root) {
        dfs(root);
        // 寻找map中最大的（即出现次数最多的）
        int max = -1;
        List<Integer> list = new ArrayList<>();
        for(int i : map.keySet()){
            if(map.get(i) == maxcount) list.add(i);
        }
        // list转普通数组
        int[] res = new int[list.size()];
        for(int i = 0; i < res.length; i++){
            res[i] = list.get(i);
        }
        return res;
    }
    // 后序遍历
    public void dfs(TreeNode node){
        if(node == null) return;
        dfs(node.left);
        dfs(node.right);
        // !!! 核心代码
        if(node.left != null || node.right != null){
            node.val = (node.left == null ? 0 : node.left.val) + (node.right == null ? 0 : node.right.val) + node.val;
        }
        // 放入map中，同时不断更新最大的出现次数
        int count = map.getOrDefault(node.val, 0) + 1;
        map.put(node.val, count);
        if(maxcount < count) maxcount = count;
    }
}
```

解释：

- 使用后序遍历，不断去更改结点的值，左右根，当到根的时候，将当前节点的值设置为左右结点的和，不断下去，这个树的每个结点的值都是左右孩子值的和了
- 设置一个map来记录每个结点的出现次数，在遍历的过程中，如果在map中找到，则值+1，如果没有找到则设置为1,
- 同时设置一个变量去保存最大的出现次数，不断更新这个变量，当遍历完成后，那么这个变量的值就是最大的次数，而不再需要重新去遍历map得到这个最大值
- 最后去map 中根据`maxcount`找结果加入结果集即可