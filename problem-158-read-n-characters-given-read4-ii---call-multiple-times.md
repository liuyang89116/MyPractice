# Problem 158: Read N Characters Given Read4 II - Call multiple times

> https://leetcode.com/problems/read-n-characters-given-read4-ii-call-multiple-times/

---------
![](/assets/158.png)

--------
##思路
* 这道题比上一道题难度增大，上一题说 read 函数只能调用一次，而这道题说read函数可以调用多次，为了更简单直观的说明问题，我们举个简单的例子吧。  
比如：buf = "ab", [read(1),read(2)]，返回 ["a","b"]，那么第一次调用read(1) 后，从 buf 中读出一个字符，那么就是第一个字符 a，然后又调用了一个read(2)，想取出两个字符，但是 buf 中只剩一个b了，所以就把取出的结果就是 b。   
再来看一个例子：buf = "a", [read(0),read(1),read(2)]，返回 ["","a",""]，第一次调用 read(0)，不取任何字符，返回空，第二次调用 read(1)，取一个字符，buf 中只有一个字符，取出为a，然后再调用 read(2)，想取出两个字符，但是 buf 中没有字符了，所以取出为空。
* 这里我们需要记录上一次 buff 的使用情况： buffPtr 代表 buff 的 pointer，看他指到了哪儿； buffCnt 代表的是 buff 的index，看读完了没有。

---------


```java
/* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
    
    private int buffPtr = 0;
    private int buffCnt = 0;
    private char[] buff = new char[4];
    
    public int read(char[] buf, int n) {
        int ptr = 0;
        while (ptr < n) {
            if (buffPtr == 0) {
                buffCnt = read4(buff);
            }
            while (ptr < n && buffPtr < buffCnt) {
                buf[ptr++] = buff[buffPtr++];
            }
            // all chars in buff used up, set pointer to 0
            if (buffPtr == buffCnt) {
                buffPtr = 0;
            }
            // read4 returns less than 4, end of file
            if (buffCnt < 4) {
                break;
            }
            
        }
        
        return ptr;
    }
}
```

