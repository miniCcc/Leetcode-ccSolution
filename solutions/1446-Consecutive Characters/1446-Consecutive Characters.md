### 题目地址：https://leetcode-cn.com/problems/consecutive-characters/
### Java
``` java
class Solution {
    // 采用的是计数的方法，双指针法思想差不多
    public int maxPower(String s) {
        int max = 1;
        int count = 1;
        for(int i = 0; i < s.length() - 1; i++){
            if(s.charAt(i) == s.charAt(i + 1)) count++;
            else{
                if(max <= count) max = count;
                count = 1;
            }
        }
        return Math.max(count, max);
    }
}
```
---
### Python3
``` python
class Solution:
    def maxPower(self, s: str) -> int:
        mymax = 1
        count = 1
        for i in range(len(s) - 1):
            if s[i] == s[i + 1]: count += 1
            else:
                mymax = max(mymax, count)
                count = 1
        return max(mymax, count)
```
