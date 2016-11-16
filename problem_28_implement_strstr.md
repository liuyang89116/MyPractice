# Problem 28: Implement strStr()


> https://leetcode.com/problems/implement-strstr/

-----
##思路
* 这道题很多解法，官方解法虽然嗯简单，但是用了很多 java 的函数在里面。这里用的双指针法应该是从根本上解决问题

------
```java
public class Solution {
    public int strStr(String haystack, String needle) {
        if (haystack == null || needle == null || haystack.length() < needle.length()) {
            return -1;
        }
        
        for (int i = 0; i <= haystack.length() - needle.length(); i++) {
            int j = 0;
            for (j = 0; j < needle.length(); j++) {
                if (haystack.charAt(i + j) != needle.charAt(j)) {
                    break;
                }
            }
            
            if (j == needle.length()) {
                return i;
            }
        }
        
        return -1;
    }
}
```
##易错点
1. 判断是否有子串
```java
if (j == needle.length()) {
          return i;
}
```
循环完之后，j 是length() - 1 的，但是跳出循环之前还得再判断一次！这次的时候，j == length() - 1。
2. 循环 haystack 的时候，是在 i 的基础上，i + j
3. 第一次出现是说第一次出现的“开头”，所以返回的是 i
4. corner cases
```java
for (int i = 0; i <= haystack.length() - needle.length(); i++)
```
按理说 i 循环到 ```i < haystack.length()```就可以了，但是，如果两个字符串都是空集的时候，就会报错了。因为没有循环到空字符串，直接跳出，返回 -1

