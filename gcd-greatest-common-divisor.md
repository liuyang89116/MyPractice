# GCD Greatest Common Divisor



```java
package GCD;

import java.awt.*;

/**
 * Created by yang on 1/17/17.
 */
public class Solution {
    public static int gcd(int[] array) {
        if (array == null || array.length == 0) {
            return 0;
        }
        int gcd = array[0];
        for (int i = 1; i < array.length; i++) {
            gcd = helper(gcd, array[i]);
        }

        return gcd;
    }

    private static int helper(int num1, int num2) {
        if (num1 == 0 || num2 == 0) {
            return 0;
        }

        while (num1 != 0 && num2 != 0) {
            if (num2 > num1) {
                num1 ^= num2;
                num2 ^= num1;
                num1 ^= num2;
            }
            int tmp = num1 % num2;
            num1 = num2;
            num2 = tmp;
        }

        return num1 + num2;
    }

    public static void main(String[] args) {
        int[] arr = new int[]{64, 8, 16, 32, 128};
        System.out.println(gcd(arr));
    }
}

```



