### 题目地址：https://leetcode-cn.com/problems/letter-tile-possibilities/

解释：
  1. 其实也就是全排列问题
  2. 记录每个字母出现的次数，如果使用了就--，如果最后都使用完了则可以return

<img src="QQ%E6%88%AA%E5%9B%BE20200701120135.png?raw=true" width="80%" height="80%">
图片来自于：https://leetcode-cn.com/problems/letter-tile-possibilities/solution/hui-su-suan-fa-python-dai-ma-by-liweiwei1419/

### Java
``` java
class Solution {
    int[] count;
    public int numTilePossibilities(String tiles) {
        count = new int[26];
        for (char c : tiles.toCharArray()) {
            count[c - 'A']++;
        }
        return helper();
    }

    public int helper() {
        int res = 0;
        for (int i = 0; i < count.length; i++) {
            // 如果用完了，或者没有，直接跳过
            if (count[i] == 0) continue;
            // 代表我当前是一个分支
            res ++;
            // 做选择
            count[i]--;
            // 进入下一层，把下一层的有效分支+上
            res += helper();
            // 撤销选择
            count[i]++;
        }
        return res;
    }
}
```
---
根据之前总结的模板瞎改的
``` java
class Solution {
    List<List<Character>> res = new ArrayList<>();
    public int numTilePossibilities(String tiles) {
        int[] count = new int[26];
        List<Character> list = new ArrayList<>();  
        for (char c : tiles.toCharArray()) {
            count[c - 'A']++;
        }
        helper(count, list);
        // 减去[]空集
        return res.size() - 1;
    }

    public void helper(int[] count, List<Character> list) {
        res.add(list);
        for (int i = 0; i < count.length; i++) {
            if (count[i] == 0) continue;
            list.add((char) count[i]);
            count[i]--;
            helper(count, list);
            count[i]++;
            list.remove(list.size() - 1);
        }
    }
}

```
