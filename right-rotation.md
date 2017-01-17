# Right Rotation

> 判断 string1 和 string2 是否互为 right rotation。比如：abcd 和 cdab.CC150原题.



```java
package RightRotation;

/**
 * Created by yang on 1/17/17.
 */
public class Solution {
    public static int rightRotate(String word1, String word2) {
        if (word1 == null || word1.length() == 0 || word2 == null || word2.length() == 0) {
            return -1;
        }
        if (word1.length() != word2.length()) {
            return -1;
        }

        String s = word1 + word1;
        return s.indexOf(word2) != -1 ? 1 : -1;
    }

    public static void main(String[] args) {
        String word1 = "abcd";
        String word2 = "cdab";
        System.out.println(rightRotate(word1, word2));
    }
}

```

