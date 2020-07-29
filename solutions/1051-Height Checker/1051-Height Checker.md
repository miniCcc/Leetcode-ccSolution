### 题目地址：https://leetcode-cn.com/problems/height-checker/

**解释：也就是求排序后，相同位置（下标）值不一样的个数**
### Java
``` java
class Solution {
    public int heightChecker(int[] heights) {
        int temp[] = heights.clone();
        Arrays.sort(heights);
        int count = 0;
        for(int i = 0; i < heights.length; i++){
            if(heights[i] != temp[i]) count++;
        }
        return count;
    }
}
```
---
### Python3
``` python
class Solution:
    def heightChecker(self, heights: List[int]) -> int:
        temp = heights[:]
        heights.sort()
        count = 0
        for i in range(len(heights)):
            if heights[i] != temp[i]:
                count += 1
        return count
```
