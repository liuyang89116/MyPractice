# Problem151: Reverse Words in a String


> https://leetcode.com/problems/reverse-words-in-a-string/


---------------------------------------------------------------
这道题非常disgusting，有无数的corner cases要去考虑。但这种题目是准备的关键。

---------------------------------
##思路
这道题的思路有很多，第一种是考虑各种的corner cases，比如首尾有没有space啦，中间隔着很多space啦等等。但是实际上正面做的时候，还是感觉到很难把所有的情况都考虑到，容易出错。

第二种思路，类似于快慢指针的办法。先设置一个start指针，从末尾往前走，因为有可能有trailing spaces，所以真正当他遇到第一个不为空的character的时候，这时候，我们设置另一个指针end。接下来，让start指针继续向前走，直到start遇到下一个空格，这时，start和end之间的词就被定位了，它将是answer的第一个词。以此类推。

------------------------------------

```java
public class Solution {
    public String reverseWords(String s) {
        if (s.length() == 0 || s == null) {
            return s;
        }

        StringBuilder sb = new StringBuilder();
        for (int start = s.length() - 1; start >= 0; start--) {
            if (s.charAt(start) == ' ') {
                continue;
            }
            int end = start;
            while (start >= 0 && s.charAt(start) != ' ') {
                start--;
            }
            sb.append(s.substring(start + 1, end + 1) + " ");
        }
        
        return sb.toString().trim();
    }
}
```
---------------------
##易错点

1. 空指针查看是非常必要的
   ```java
   if (s.length() == 0 || s == null) {
       return s;
   }
   ```
2. substring 的index问题
   substring(beginIndex, endIndex);
   beginIndex-包含；endIndex-不包含      [a, b)
   
   ```java
   String s = "Hello World";
		
   System.out.println(s.substring(0));  // Hello World
   System.out.println(s.substring(1));  // ello World
   System.out.println(s.substring(0, 2)); // He
   System.out.println(s.substring(0, 4)); // Hell
   ```
   这道题里，
   ```java
   sb.append(s.substring(start + 1, end + 1) + " ");
   ```
   ```start + 1``` 是因为start已经挪到了空白处; ```end + 1```是因为右边是开区间
  
3. 去除空白的函数
   ```trim()```
4. StringBuider的用处
   ```java
   StringBuilder sb = new StringBuilder();
   ```
   创建一个StringBuilder
   ```java
   sb.append(s.substring(start+1, end+1) + " ");
   ```
   不断地append这个builder
   ```java
   sb.toString();
   ```
   再把StringBuilder变成字符串