### 题目地址：https://leetcode-cn.com/problems/subsets-ii/

解释：
1. 换个思考方式，加入利用一个map，记录每个数据出现的次数
2. 根据map里面的数据，不断组成不同的组合，看起来有点像排列组合问题
3. 而在解决这类问题的时候一般使用**回溯**
4. 参考链接：<br>
    4.1 [链接1](https://github.com/labuladong/fucking-algorithm/blob/master/%E7%AE%97%E6%B3%95%E6%80%9D%E7%BB%B4%E7%B3%BB%E5%88%97/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95%E8%AF%A6%E8%A7%A3%E4%BF%AE%E8%AE%A2%E7%89%88.md)<br>
    4.2 [链接2](https://github.com/labuladong/fucking-algorithm/blob/master/%E9%AB%98%E9%A2%91%E9%9D%A2%E8%AF%95%E7%B3%BB%E5%88%97/%E5%AD%90%E9%9B%86%E6%8E%92%E5%88%97%E7%BB%84%E5%90%88.md)
    

<img src="1593394317.983626.jpg?raw=true" width="60%" height="60%">

### Java
``` java
class Solution {
    private List<List<Integer>> res = new ArrayList<>();

    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<Integer> list = new ArrayList<>();
        // 一定要排序
        Arrays.sort(nums);
        helper(nums, list, 0);
        return res;
    }

    public void helper(int[] nums, List<Integer> list, int index){
        // 记录上一层的数据
        res.add(new ArrayList<>(list));
        for(int i = index; i < nums.length; i++){
            if(i - 1 >= index && nums[i - 1] == nums[i]) continue;
            // 加入路径
            list.add(nums[i]);
            // 回溯，进入下一层
            helper(nums, list, i + 1);
            // 撤销操作
            list.remove(list.size() - 1);
        }
    }
}
```
