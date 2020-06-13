### 题目地址：https://leetcode-cn.com/problems/buddy-strings/
### Java
``` java
class Solution {
    public boolean buddyStrings(String A, String B) {
        if(A.length() != B.length() || A.length() < 2) return false; // 首先比较长度，不等的话直接false
        if(A.equals(B)){ // 如果A,B相等，则需要判断是ab,ab还是aa,aa的情况，如果是aa,aa这种情况，那么一定有重复的元素
            for(int i = 0; i < A.length(); i++){
                if(A.indexOf(A.charAt(i)) != i) return true;
            }
        }
        int countdiff = 0; // 用于记录不同位置的个数
        int[] index = new int[2]; // 用于记录不同地方的下标
        for(int i = 0; i < A.length(); i++){
            if(A.charAt(i) != B.charAt(i)){
                countdiff++;
                if(countdiff > 2) return false; // 当大于2时直接false，因为只能交换一次
                index[countdiff - 1] = i; // countdiff = 1时代表找到第一个不同位置，记录在index[0]上，countdiff = 2也同样类推
            }
        }
        // 先判断countdiff == 2,因为是惰性判断，当不等于时直接就结束
        // index[]记录的是不同的两个位置的下标，现在只需要判断交换这两个位置后A,B是否还相等，因此直接判断交叉位置上的元素是否相等即可
        // 注意：countdiff == 1 时，没人与他交换，false
        // 注意: countdiff == 0时，也就是ab,ab或者aa,aa这种情况， 但是在最开始已经判断过aa,aa这类似情况，因此ab,ab是直接false的
        return countdiff == 2 && A.charAt(index[0]) == B.charAt(index[1]) && A.charAt(index[1]) == B.charAt(index[0]);
    }
}
```

---

### Python3
```python
class Solution:
    def buddyStrings(self, A: str, B: str) -> bool:
        if len(A) != len(B) or len(A) < 2: 
            return False
        if A == B:
            for i in range(len(A)):
                if A.find(A[i]) != i:
                    return True
        countdiff = 0
        index = [0, 0]
        for i in range(len(A)):
            if A[i] != B[i]:
                countdiff += 1
                if countdiff > 2:
                    return False
                index[countdiff - 1] = i
        return countdiff == 2 and A[index[0]] == B[index[1]] and A[index[1]] == B[index[0]]
```
