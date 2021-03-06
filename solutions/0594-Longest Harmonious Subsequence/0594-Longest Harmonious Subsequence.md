### 题目地址：https://leetcode-cn.com/problems/longest-harmonious-subsequence/

### 题解1：
``` java
class Solution {
    public int findLHS(int[] nums) {
        Arrays.sort(nums);
        int res = 0;
        int index = 0;
        for(int i = 0; i < nums. length; i++){
            while(nums[i] - nums[index] > 1){
                index++;
            }
            if(nums[i] - nums[index] == 1) res = Math.max(res, i - index + 1);
        }
        return res;
    }
}
```
### 解释：
1、先对数组进行排序，从小到大进行排序

2、i其实是end，index其实是begin

3、看似i在index前面，其实执行完while之后，

![image](20200527112300.png)
---

### 题解2：

``` java
class Solution {
    public int findLHS(int[] nums) {
        int res = 0;
        Map<Integer, Integer> map = new HashMap<>();
        for(int num : nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        for(int i : map.keySet()){
            if(map.get(i + 1) != null){
                res = Math.max(res, map.get(i + 1) + map.get(i));
            }
        }
        return res;
    }
}
```

### 解释：
![image](20200527110533.png)

---
### python3
```python
class Solution:
    def findLHS(self, nums: List[int]) -> int:
        res = 0
        count = {} # 这是一个字典
        # 记录元素出现个数
        for i in nums:
            if i in count:
                count[i] += 1
            else: 
                count[i] = 1
    
        for i in count:
            if i+1 in count:
                res = max(res, count[i] + count[i + 1])

        return res
```
