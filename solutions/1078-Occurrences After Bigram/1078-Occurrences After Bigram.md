题目地址：https://leetcode-cn.com/problems/occurrences-after-bigram/
``` java
class Solution {
    public String[] findOcurrences(String text, String first, String second) {
        String[] temp = text.split(" ");
        if(temp.length < 3) return new String[0];
        List<String> res = new ArrayList<>();
        for(int i = 0; i < temp.length - 2; i++){
            if(temp[i].equals(first) && temp[i + 1].equals(second)){
                res.add(temp[i + 2]);
            }
        }
        return (String []) res.toArray(new String[res.size()]);
    }
}
```
IPAD上记录：
![image](20200525165702.png)
