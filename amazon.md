# Consecutive Gray Code

> 给两个byte，判断它们是否为连续 greycode. Given two hexadecimal numbers find if they can be consecutive in gray code.

```
For example: 10001000, 10001001
              return 1
since they are successive in gray code
 
Example2: 10001000, 10011001
              return -1
since they are not successive in gray code.
```

--------
##思路
* 主要就是 check 是否有一个 bit 被翻转

---------


```java
package GreyCode;

/**
 * Created by yang on 1/17/17.
 */

/**
 * 给两个byte，判断它们是否为连续 greycode
 *
 * Given two hexadecimal numbers find if they can be consecutive in gray code
 *   For example: 10001000, 10001001
 *   return 1
 *  since they are successive in gray code
 *
 *   Example2: 10001000, 10011001
 *   return -1
 *   since they are not successive in gray code.
 */
public class Solution {
    public static int greyCode(byte term1, byte term2) {
        byte x = (byte) (term1 ^ term2);
        int count = 0;
        while (x != 0) {
            x = (byte) (x & (x - 1));
            count++;
        }

        return count == 1 ? 1 : 0;
    }
}

```

