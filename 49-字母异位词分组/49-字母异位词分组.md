### 题目地址：https://leetcode-cn.com/problems/group-anagrams/

给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

**示例:**

输入: <br>
["eat", "tea", "tan", "ate", "nat", "bat"]<br>
输出:<br>
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]<br>

**说明：**

所有输入均为小写字母。
不考虑答案输出的顺序。

---

解释：
1. 本题利用HashMap来解决，但是Map使用更加灵活 `Map<String, List<String>> map = new HashMap<>();`
2. 可以看到Map的值是一个list，而且这个list是动态变化的
3. 异位词：只要按照字母顺序排序后一致的词，那么就是异位词
4. 在不断遍历的过程中，查看map中是否有这个词（排序后的），如果有，那么本原单词加入后更改list，如果没有，那么新建一个list
5. 也就是说，map中的键是排序后的词，相对应的值（也就是list）就是键所对应的结果集

### Java
``` java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();
        for(String str : strs){
            char[] c = str.toCharArray();
            Arrays.sort(c);
            String temp = String.valueOf(c);
            // getOrDefault方法注意
            List<String> list = map.getOrDefault(temp, new ArrayList<>());
            // 动态更改list
            list.add(str);
            // 保存更改后的
            map.put(temp, list);
        }
        // 只返回了map的value，键不管
        return new ArrayList<>(map.values());
    }
}
```
