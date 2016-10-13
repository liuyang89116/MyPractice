# Problem 387: First Unique Character in a String


> https://leetcode.com/problems/first-unique-character-in-a-string/

----------
##思路
* 记录一遍每个元素出现的次数，然后回溯的时候查找

-----------
```java
public class Solution {
    public int firstUniqChar(String s) {
        int[] arr = new int[26];
        for (int i = 0; i < s.length(); i++) {
            arr[s.charAt(i) - 'a'] += 1;
        }
        
        for (int i = 0; i < s.length(); i++) {
            if (arr[s.charAt(i) - 'a'] == 1) {
                return i;
            } 
        }
        
        return -1;
    }
}
```
-------
##易错点
1.记录元素个数的方法
```java
for (int i = 0; i < s.length(); i++) {
       arr[s.charAt(i) - 'a'] += 1;
}
```
