# Problem 242: Valid Anagram

>https://leetcode.com/problems/valid-anagram/

-------------
##思路
* 这道题至少有两种思路：第一种就是先拆分成数组，然后再转化为 String，比较两个 String 是否相同；第二种就是遍历的方法。
* 第一种方法速度很快，但是可能并不是面试官想要看的
* 最优解放在最上面

-----------------------
```java
/*
  最优解
*/
public class Solution {
    public boolean isAnagram(String s, String t) {
        int[] arr = new int[26];
        
        for (int i = 0; i < s.length(); i++) {
            arr[s.charAt(i) - 'a']++;
        }
        for (int i = 0; i < t.length(); i++) {
            arr[t.charAt(i) - 'a']--;
        }
        
        for (Integer count : arr) {
            if (count != 0) {
                return false;
            }
        }
        
        return true;
    }
}
```
```java
/*
  First version
*/
public class Solution {
    public boolean isAnagram(String s, String t) {
        char[] sArr = s.toCharArray();
        char[] tArr = t.toCharArray();
        Arrays.sort(sArr);
        Arrays.sort(tArr);
        
        return String.valueOf(sArr).equals(String.valueOf(tArr)); 
    }
}
```

```java
/*
  Second version
*/
public class Solution {
    public boolean isAnagram(String s, String t) {
        HashMap<Character, Integer> hm = new HashMap<Character, Integer>();
        char[] sArr = s.toCharArray();
        char[] tArr = t.toCharArray();
        
        for (Character c : sArr) {
            if (hm.containsKey(c)) {
                hm.put(c, hm.get(c) + 1);
            } else {
                hm.put(c, 1);
            } 
        }
        
        for (Character c : tArr) {
            if (hm.containsKey(c)) {
                hm.put(c, hm.get(c) - 1);
            } else {
                return false;
            }
        }
        
        for (Integer value : hm.values()) {
            if (value != 0) {
                return false;
            } 
        }
        
        return true;
    }
}
```
-----
##易错点
1.注意如果 map 里面没有该元素的时候，put 的个数是 1
```java
hm.put(c, 1);
```










