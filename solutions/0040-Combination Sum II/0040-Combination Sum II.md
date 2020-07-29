### 题目地址：https://leetcode-cn.com/problems/combination-sum-ii/

给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的每个数字在每个组合中只能使用一次。

**说明**：

所有数字（包括目标数）都是正整数。
解集不能包含重复的组合。 

**示例 1**:

输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]

---

### Java
``` java
class Solution {
    // 因为每个数只能用一次，那么当一个数出现多次的时候，可能会产生重复的解，比如[1, 1, 2]则可能有[1, 2](第一个1),[1, 2](第二个1)
    // 采用set + int i = index 的方法去重
    private Set<List<Integer>> res = new HashSet<>();
    private int sum = 0;

    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        List<Integer> list = new ArrayList<>();
        backtrack(candidates, target, list, 0);
        return new ArrayList<>(res);
    }
    public void backtrack(int[] candidates, int target, List<Integer> list, int index){
        if(sum == target){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i = index; i < candidates.length; i++){
            if(sum > target) continue;
            list.add(candidates[i]);
            sum += candidates[i];
            backtrack(candidates, target, list, i + 1);
            list.remove(list.size() - 1);
            sum -= candidates[i];
        }
    }
}
```

### 优化
1. 因为set底层是红黑树，因此效率不太行，有更好的去重方案
2. [参考链接](https://leetcode-cn.com/problems/combination-sum-ii/solution/hui-su-suan-fa-jian-zhi-python-dai-ma-java-dai-m-3/)
3. 解释一下：他是采用减法的方式，我是采用的加法的方式，本质上其实差不多；但是重点在于黄色框起来的部分（剪枝），判断同一层是否有相等的节点（i > index && can[i] == can[i - 1]）：i > index是用来判断同层是否是首次出现还是第二次第三次出现，can[i] == can[i - 1]是用来判断是否值相等
