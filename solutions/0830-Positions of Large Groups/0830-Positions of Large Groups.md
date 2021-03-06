### 题目地址：https://leetcode-cn.com/problems/positions-of-large-groups/

### Java题解：
``` java
class Solution {
    public List<List<Integer>> largeGroupPositions(String S) {
        List<List<Integer>> res = new ArrayList<>();
        int count = 1;
        for(int i = 0; i < S.length() - 1; i++){
            if(S.charAt(i) == S.charAt(i + 1)) count++;
            else{
                if(count >= 3){
                    List<Integer> temp = new ArrayList<>();
                    // 计算起始位置
                    temp.add(i - count + 1);
                    temp.add(i);
                    res.add(temp);
                }
                # 重新计数
                count = 1;
            }
        }
        // 处理最后连续特殊情况，可能最后是大于三个连续的，但是没有！=的条件去结束，需要重新判断
        if(count >= 3){
            List<Integer> temp = new ArrayList<>();
            temp.add(S.length() - count);
            temp.add(S.length() - 1);
            res.add(temp);
        }
        return res;
    }
}
```

**改进**：如果在S的最后追加一个大写字母，如'A'，那么就不用最后再判断一次了

---
### Python3题解：
``` pythoon
class Solution:
    def largeGroupPositions(self, S: str) -> List[List[int]]:
        res = []
        S += 'A'
        count = 1
        for index in range(len(S) - 1):
            if(S[index] == S[index + 1]):
                count += 1
            else:
                if count >= 3:
                    res.append([index - count + 1, index])
                count = 1
        return res
```
