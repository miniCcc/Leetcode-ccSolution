### 题目地址：https://leetcode-cn.com/problems/compare-strings-by-frequency-of-the-smallest-character/
### Java
``` java
class Solution {
    public int[] numSmallerByFrequency(String[] queries, String[] words) {
        int[] res = new int[queries.length];
        for(int i = 0; i < queries.length; i++){
            int count = 0;
            for(int j = 0; j < words.length; j++){
                if(f(queries[i]) < f(words[j])) count++;
            }
            res[i] = count;
        }
        return res;
    }
    public int f(String s){
        char[] str = s.toCharArray();
        Arrays.sort(str);
        int count = 1;
        for(int i = 0; i < str.length - 1; i++){
            if(str[i] == str[i + 1]) count++;
            else break;
        }
        return count;
    }
}
```
**Java思路：**
1. 写出函数f统计最小字母频次，直接sort后找第一个的个数即可
2. 暴力双重for循环统计

### 改进版本
---
**先说思路：**
1. 使用数组统计最小频次，直接遍历数组即可，最多26个
2. 使用一个辅助数组，统计words中对应字符串最小字母频次，进行存储，然后sort排序
3. 外循环遍历queries数组，计算当前queries[i]的最小字母频次，然后需要找到大于他频次的个数，就去辅助数组里用二分查找（注意是二分）

``` java
class Solution {
    public int[] numSmallerByFrequency(String[] queries, String[] words) {
        int[] res = new int[queries.length];
        int[] target = new int[words.length];
        // 使用辅助数组
        for(int i = 0; i < target.length; i++){
            target[i] = f(words[i]);
        }
        Arrays.sort(target);
        for(int i = 0; i < queries.length; i++){
            res[i] = BinarySearch(f(queries[i]), target);
        }
        return res;
    }
    // 改动版本的二分
    public int BinarySearch(int target, int[] nums){
        int left = 0, right = nums.length - 1;
        while(left < right){
            int mid = (left + right) / 2;
            //注意这里不是 right = mid - 1
            //是因为我们要找的数是第一个大于target的值，可能这个数正好是，不能舍去
            if(nums[mid] > target) right = mid;
            else left = mid + 1;
        }
        //跳出while后 left == right，可能是找到了跳出，也可能是没找到跳出，进行判断
        return nums[left] <= target ? 0 : nums.length - left;
    }
    // 计算最小字母频次
    public int f(String s){
        int[] countNum = new int[26];
        if(s == null || s.length() == 0) return 0;
        char[] Schar = s.toCharArray();
        for(char c : Schar){
            countNum[c - 'a']++;
        }
        for(int num : countNum){
            if(num > 0) return num;
        }
        return 0;
    }
}
```
