# Problem 383: Ransom Note


> https://leetcode.com/problems/ransom-note/

------
##思路
* 就是一个变相的哈希表的计数
* 这道题虽然简单，但是涉及到的东西还挺多的

-----------
```java
public class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
       int[] cnt = new int[26];
       for (int i = 0; i < magazine.length(); i++) {
           cnt[magazine.charAt(i) - 97]++;
       }
       for (int i = 0; i < ransomNote.length(); i++) {
           if(--cnt[ransomNote.charAt(i) - 97] < 0) {
               return false;
           }
       }
        
       return true;    
    }
}
```
----
##易错点

1. 字母的 ASCII 码
a - z: 97 - 122
A - Z: 65 - 90
0 - 9: 48 - 57
2. 几个非常容易错的知识点
```java
String s  = "abc";
System.out.println(s.charAt(0));          // a   
System.out.println(s.charAt(0) - '0');    // 49
System.out.println(s.charAt(0) - 0);      // 97
```





























