# Problem 125: Valid Palindrome


> https://leetcode.com/problems/valid-palindrome/

题目不难，但是要注意的东西还是有很多的

-----------------------------
##思路
这道题的思路就是首尾各一个指针，遇到不是字母或者数字的字符跳过，最后汇合，判定是否为palindrome

```java
public class Solution {
    public boolean isPalindrome(String s) {
        int start = 0;
        int end = s.length() - 1;
        char c1, c2;
        while (start <= end) {
            c1 = s.charAt(start);
            c2 = s.charAt(end);
            if (!Character.isLetterOrDigit(c1)) {
                start++;
            } else if (!Character.isLetterOrDigit(c2)) {
                end--;
            } else {
                if (Character.toLowerCase(c1) != Character.toLowerCase(c2)) {
                    return false;
                }
                start++;
                end--;
            }
        }
        return true;
    }
}
```
----------------------------------
##易错点
1. 逻辑结构一定要想清楚：几个条件要同时满足（start得是字母，end也得是字母），缺一不可，那么得用 if...else...这个结构
2. start 和 end 变化的位置 
```java
start++;
end--;
```
应该放在else的block下面，因为是在他们都是字母的情况下进行的操作
3. 判断是否为字母
```java
Character.isLetterOrDigit(c1);
```
4. 转换大小写
```java
Character.toLowerCase(c1);
```