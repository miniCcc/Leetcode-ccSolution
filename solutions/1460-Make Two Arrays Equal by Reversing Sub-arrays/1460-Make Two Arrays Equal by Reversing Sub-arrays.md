### 题目地址：https://leetcode-cn.com/problems/make-two-arrays-equal-by-reversing-sub-arrays/
### Java
``` java
class Solution {
    public boolean canBeEqual(int[] target, int[] arr) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int num : target){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        for(int i = 0; i < arr.length; i++){
            if(map.get(arr[i]) != null){
                int count = map.get(arr[i]);
                map.put(arr[i], --count);
            }else if(map.get(arr[i]) == null || map.get(arr[i]) == 0) return false;
        }
        return true;
    }
}
```

**分析：**
其实就是比较两个数组是否相等，可以直接排序，然后遍历判断对应位置

---
### Python
``` python
class Solution:
    def canBeEqual(self, target: List[int], arr: List[int]) -> bool:
        target.sort()
        arr.sort()
        for i in range(len(target)) :
            if target[i] != arr[i] :
                return False
        return True

```
