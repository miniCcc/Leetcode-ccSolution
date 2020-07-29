### 题目地址：https://leetcode-cn.com/problems/permutations/

解释：
1. 全排列问题还是可以用回溯来实现
2. 实质上还是遍历一颗决策树
<img src="1593478887.77555.jpg?raw=true" width="60%" height="60%">

### Java
``` java
class Solution {
    private List<List<Integer>> res = new ArrayList<>();

    public List<List<Integer>> permute(int[] nums) {
        List<Integer> list = new ArrayList<>();
        backtrack(nums, list);
        return res;
    }

    public void backtrack(int[] nums, List<Integer> list){
        if(list.size() == nums.length){
            // 注意
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i = 0; i < nums.length; i++){
            // 不考虑的情况
            if(list.contains(nums[i])) continue;
            // 做选择
            list.add(nums[i]);
            backtrack(nums, list);
            // 撤销选择
            list.remove(list.size() - 1);
        }
    }
}
```
