### 题目地址：https://leetcode-cn.com/problems/subsets/
### Java
``` java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        // 加入空集
        res.add(new ArrayList<>());
        
        for(int i = 0; i < nums.length; i++){
            // 记得每次重新获取len
            int len = res.size();
            // 将该数加入之前的所有所有子集
            for(int j = 0; j < len; j++){
                // 实现浅拷贝,只复制数据
                List<Integer> temp = new ArrayList<>(res.get(j));
                temp.add(nums[i]);
                res.add(temp);
            }
        }
        return res;
    }
}
```
解释：
1. 顺序遍历，每次将该数，也就是nums[i]加入以前的子集A，生成一个新的子集B
2. 合并A与B作为新的子集

![image](1592883571.257847.jpg?raw=true)
