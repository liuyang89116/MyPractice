# Problem 38: Count and Say


> https://leetcode.com/problems/count-and-say/

----------
##思路
* 理解题目：  
解释一下就是，输入n，那么我就打出第n行的字符串。  
怎么确定第n行字符串呢？他的这个是有规律的。  
n = 1时，打印一个1    
n = 2时，看n=1那一行，念：1个1，所以打印：11    
n = 3时，看n=2那一行，念：2个1，所以打印：21    
n = 4时，看n=3那一行，念：一个2一个1，所以打印：1211    
以此类推。(注意这里n是从1开始的）
* 每个 entry 的格式是： count + oldChar；所以我们对每个 char 遍历一遍就好

--------
```java
public class Solution {
    public String countAndSay(int n) {
        String oldString = "1";
        //n = n - 1;
        while (--n > 0) {
            StringBuilder sb = new StringBuilder();
            char[] oldChars = oldString.toCharArray();
            
            for (int i = 0; i < oldChars.length; i++) {
                int count = 1;
                while (i + 1 < oldChars.length && oldChars[i] == oldChars[i + 1]) {
                    count++;
                    i++;
                }
                sb.append(String.valueOf(count) + String.valueOf(oldChars[i]));
            }
            oldString = sb.toString();
            //n--;
        }
        return oldString;
    }
}
```
------
##易错点

1. oldString = "1" 初始时已经有了，所以在 n 内已经占用了一个了。所以我们从 n - 1 开始
2. String to char
```java
char[] oldChars = oldString.toCharArray();
```
3. int or Char to String
```java
String a = String.valueOf(count);
String b = String.valueOf(oldChars[i]);
```























