### 题目地址：https://leetcode-cn.com/problems/combination-sum-iii/submissions/

### Java
``` java
class Solution {
    private List<List<Integer>> res = new ArrayList<>();
    private int sum = 0;

    public List<List<Integer>> combinationSum3(int k, int n) {
        List<Integer> list = new ArrayList<>();
        backtrack(k, n, list, 1);
        return res;
    }
    
    public void backtrack(int k, int n, List<Integer> list, int index){
        // 累加为n的k个数，也就是说加入结果集有两个条件
        if(sum == n && list.size() == k){
            res.add(new ArrayList<>(list));
            return;
        }
        // index用于防止重复的集合，每次都只找比自己大的
        for(int i = index; i <= 9; i++){
            if(list.contains(i)) continue;
            list.add(i);
            // 做选择，记录当前累加值
            sum += i;
            backtrack(k, n, list, i + 1);
            list.remove(list.size() - 1);
            // 撤销选择后sum也需要回到原来的状态
            sum -= i;
        }
    }
}
```
