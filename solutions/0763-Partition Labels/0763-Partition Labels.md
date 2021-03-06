### 题目地址：https://leetcode-cn.com/problems/partition-labels/

字符串 S 由小写字母组成。我们要把这个字符串划分为尽可能多的片段，同一个字母只会出现在其中的一个片段。返回一个表示每个字符串片段的长度的列表。

**示例 1：**

输入：S = "ababcbacadefegdehijhklij"<br>
输出：[9,7,8]<br>

**解释：**

划分结果为 "ababcbaca", "defegde", "hijhklij"。<br>
每个字母最多出现在一个片段中。<br>
像 "ababcbacadefegde", "hijhklij" 的划分是错误的，因为划分的片段数较少。

---

分析：
1. 先记录每个字母的最后出现位置（下标）
2. 遍历字符串，用max记录当前这个串里字母最后出现位置，也就是维护一个max
3. 如果遇到一个新的字符，判断这个字符是否在max的下标之内
4. 如果是：则加入当前这个串
5. 如果不是，则代表当前这个串到此结束，后面的又是一个新的结果了，所有的max，count标志回归初始

---

### Java
``` java
class Solution {
    public List<Integer> partitionLabels(String S) {
        List<Integer> list = new ArrayList<>();
        Map<Character, Integer> map = new HashMap<>();
        // 记录每个单词最后一次出现的位置
        for(int i = 0; i < S.length(); i++){
            char c = S.charAt(i);
            map.put(c, i);
        }
        int max = map.get(S.charAt(0)), count = 1;
        for(int i = 1; i < S.length(); i++){
            char c = S.charAt(i);
            if(i > max){
                list.add(count);
                count = 1;
                max = map.get(c);
            }else{
                // 维护max
                if(map.get(c) >= max) max = map.get(c);
                count++;
            }
        }
        if(count != 0) list.add(count);
        return list;
    }
}
```
