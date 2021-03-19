### 0429. N 叉树的层序遍历

#### 题目地址：https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/

给定一个 N 叉树，返回其节点值的层序遍历。（即从左到右，逐层遍历）。

树的序列化输入是用层序遍历，每组子节点都由 null 值分隔（参见示例）。

 

**示例 1：**

<img src="narytreeexample.png" alt="img" style="zoom: 50%;" />

```
输入：root = [1,null,3,2,4,null,5,6]
输出：[[1],[3,2,4],[5,6]]
```

**示例 2：**

<img src="sample_4_964.png" alt="img" style="zoom:60%;" />

```
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：[[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
```

**提示：**

- 树的高度不会超过 `1000`
- 树的节点总数在 `[0, 10^4]` 之间

---

**Java**

``` java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    Queue<Node> queue = new LinkedList<>();
    List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> levelOrder(Node root) {
        if(root == null) return res;
        queue.offer(root);
        helper(new ArrayList<>());
        return res;
    }
    // 层次遍历
    public void helper(List<Integer> list){
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i = 0; i < size; i++){
                Node temp = queue.poll();
                // 找到当前结点的所有孩子
                List<Node> child = temp.children;
                // 将所有孩子入队
                for(Node n : child){
                    queue.offer(n);
                }
                list.add(temp.val);
            }
            res.add(new ArrayList<>(list));
            // 清空list，记录下一层
            list.clear();
        }
    }
}
```

