### 题目地址：https://leetcode-cn.com/problems/combination-sum/

给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target ··的组合。

candidates 中的数字可以无限制重复被选取。

**说明**：

所有数字（包括 target）都是正整数。
解集不能包含重复的组合。 <br>

**示例 1**:<br>
输入: candidates = [2,3,6,7], target = 7,
<br>所求解集为:
[
  [7],
  [2,2,3]
]

---

### Java
``` java
class Solution {
    private List<List<Integer>> res = new ArrayList<>();
    private int sum = 0;

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<Integer> list = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(candidates, target, list, 0);
        return res;
    }

    public void backtrack(int[] candidates, int target, List<Integer> list, int index){
        if(sum == target){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i = index; i < candidates.length; i++){
            if(sum + candidates[i] > target) continue;
            list.add(candidates[i]);
            sum += candidates[i];
            // 因为可以重复选自己，则还是i,而不是 i + 1
            backtrack(candidates, target, list, i);
            list.remove(list.size() - 1);
            sum -= candidates[i];
        }
    }
}
```
