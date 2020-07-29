### 题目地址：https://leetcode-cn.com/problems/combinations/

解释：
1. 其实也就是一个全排列问题，但是存在一个去重的问题，例如[1, 3]和[3, 1]是不能重复算的
2. 利用一个`index`来去重，`int i = index`，每次只找比自己大的，则不会存在[3, 1]这种情况
3. 只能挑选k个数，也就是回溯那个决策树的深度只能为k，则用`list`的大小来判断是不是已经有k个数了
<div align=center>
<img src="1593743211.301769.jpg?raw=true">
</div>


### Java
``` java
class Solution {
    private List<List<Integer>> res = new ArrayList<>();

    public List<List<Integer>> combine(int n, int k) {
        List<Integer> list = new ArrayList<>();
        backtrack(n, k, list, 1);
        return res;
    }
    public void backtrack(int n, int k, List<Integer> list, int index){
        // 已经有k个数了，return
        if(list.size() == k){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i = index; i <= n; i++){
            // 不能包含已经有过的数
            if(list.contains(i)) continue;
            // 做选择
            list.add(i);
            // 进入下一层决策
            backtrack(n, k, list, i + 1);
            // 撤销选择
            list.remove(list.size() - 1);
        }
    }
}
```

