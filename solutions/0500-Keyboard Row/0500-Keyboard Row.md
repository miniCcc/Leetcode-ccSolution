题目地址：https://leetcode-cn.com/problems/keyboard-row/

``` java
class Solution {
    public static Map<Character, Integer> map = new HashMap<>();
    public String[] findWords(String[] words) {
        List<String> res = new ArrayList<>();
        char[] first = {'q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p'}; //第一排的
        char[] second = {'a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l'}; //第二排的
        char[] third = {'z', 'x', 'c', 'v', 'b', 'n', 'm'}; //第三排的
        helper(first, 1);
        helper(second, 2);
        helper(third, 3);
        //正片开始
        for(int i = 0; i < words.length; i++){
            String str = words[i];
            int sign = map.get(str.charAt(0));
            int j = 1;
            for(; j < str.length(); j++){
                char c = str.charAt(j);
                if(map.get(c) != sign) break;
            }
            if(j == str.length()) res.add(str);
        }
        return (String[]) res.toArray(new String[res.size()]);
    }
    public static void helper(char[] num, int n){
        for(char temp : num){
            map.put(temp, n);
            map.put((char) ((int )temp - 32), n); //存大写
        }
    }
}
```

IPAD上的记录
![image](20200524105005.png)