### 题目地址：https://leetcode-cn.com/problems/smallest-range-i/

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;解释：每个A[i]可以加不同的数，不是都有的A[i]加的值都一样

### Java
``` java
class Solution {
    public int smallestRangeI(int[] A, int K) {
        if(A.length == 1) return 0;
        Arrays.sort(A);
        int min = A[0], max = A[A.length - 1];
        if(max - min > 2 * K) return max - min - 2 * K;
        return 0;
    }
}
```
---

### Python3
``` python
class Solution:
    def smallestRangeI(self, A: List[int], K: int) -> int:
        if len(A) == 1:
            return 0
        A.sort()
        mymin = A[0]
        mymax = A[len(A) - 1]
        if mymax - mymin > 2 * K:
            return mymax - mymin - 2 * K
        return 0
```&nbsp;
