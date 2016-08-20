# Problem: Rotate String (LintCode)


> http://www.lintcode.com/en/problem/rotate-string/#

-----------
##思路
* 还是三步翻转法的原理，只要涉及到**翻转（rotate）**的东西，都应该首先想到三步翻转法
* 注意：有时候需要做一些转化，比如这里的，offset 和 str.length 的换算关系，把他们转化为“左边”和“右边”的 index

-----------
```java
public class Solution {
    /**
     * @param str: an array of char
     * @param offset: an integer
     * @return: nothing
     */
    public void rotateString(char[] str, int offset) {
        if (str == null || str.length == 0) {
            return;
        }
        offset = offset % str.length;
        reverse(str, 0, str.length - 1 - offset);
        reverse(str, str.length - offset, str.length - 1);
        reverse(str, 0, str.length - 1);
        return;
    }
    
    private void reverse(char[] str, int start, int end) {
        for (int i = start, j = end; i < j; i++, j--) {
            char temp = str[i];
            str[i] = str[j];
            str[j] = temp;
        }
    }
}
```

-----------
##易错点

1. offset转化
```java
offset = offset % str.length;
```
通过这样可以避免offset比数组数值大的情况
2. index之间的转化
```java
reverse(str, 0, str.length - 1 - offset);
reverse(str, str.length - offset, str.length - 1);
reverse(str, 0, str.length - 1);
```
**遇到搞不准的时候，只需要拿两个小例子试一下就可以得出他们的关系**




























