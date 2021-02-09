### 0637-二叉树的层平均值

#### 题目地址：https://leetcode-cn.com/problems/average-of-levels-in-binary-tree/

给定一个非空二叉树, 返回一个由每层节点平均值组成的数组。

 

**示例 1：**

```
输入：
    3
   / \
  9  20
    /  \
   15   7
输出：[3, 14.5, 11]
解释：
第 0 层的平均值是 3 ,  第1层是 14.5 , 第2层是 11 。因此返回 [3, 14.5, 11] 。
```

**提示：**

- 节点值的范围在32位有符号整数范围内。

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
    List<Double> res = new ArrayList<>();
    Queue<TreeNode> queue = new LinkedList<>();
    public List<Double> averageOfLevels(TreeNode root) {
        if(root == null) return res;
        queue.offer(root);
        helper(0, 0);
        return res;
    }
    public void helper(long sum, int count){
        while(!queue.isEmpty()){
            int size = queue.size();
            sum = 0;
            for(int i = 0; i < size; i++){
                TreeNode temp = queue.poll();
                sum += temp.val;
                if(temp.left != null) queue.offer(temp.left);
                if(temp.right != null) queue.offer(temp.right);
            }
            res.add((double) sum / size);
        }
    }
}
```

- 其实这个题也就是层次遍历的改版，建议先去做二叉树的层次遍历再来做这个题

- 在层次遍历中我们使用到的是队列，而不是栈，那问题就在怎么判断本层是否结束了？可以通过下面这种方式：

  ``` java
  while(!queue.isEmpty()){
      // 去获取当前队列里有多少个，出完了就算本层结束
      int size = queue.size();
      sum = 0;
      for(int i = 0; i < size; i++){
          .....
      }
      // 到这里就结束了
  }
  ```

- 但是在不断出队列的过程中，我们需要把他们的孩子放进去，所以在......这个位置添加上自己孩子入队的操作，则成了这样：

  ``` java
  while(!queue.isEmpty()){
      int size = queue.size();
      sum = 0;
      for(int i = 0; i < size; i++){
          TreeNode temp = queue.poll();
          sum += temp.val;
          if(temp.left != null) queue.offer(temp.left);
          if(temp.right != null) queue.offer(temp.right);
      }
      res.add((double) sum / size);
  }
  ```

- ==总结一下做这种题，就是外面一层while，里面一层for==

  ``` java
  // 最外层的总控开关
  while(!queue.isEmpty()){
      // 去获取当前队列里有多少个，出完了就算本层结束
      int size = queue.size();
      for(int i = 0; i < size; i++){
  		// 做自己的操作
      }
      // 到这里就结束了，做结束操作
  }
  ```

  