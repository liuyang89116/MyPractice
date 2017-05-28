# Problem 482: License Key Formatting

> https://leetcode.com/problems/license-key-formatting/\#/description

------

## 思路

* 这道题的要求是第一个 group 可以不满足 k 的长度，但后面的都要满足。所以如果我们能从后往前排，最后剩下几个就是几个会特别方便。
* 这里的几个对 String 的处理需要熟练：`reverse()`，`toString()`，`toUpperCase()`.
* 每隔 k 位插一个 dash，用 `%`来判断。

-----

```java
public class Solution {
    public String licenseKeyFormatting(String S, int K) {
        StringBuilder sb = new StringBuilder();
        for (int i = S.length() - 1; i >= 0; i--) {
            char c = S.charAt(i);
            if (c == '-') continue;
            sb.append(sb.length() % (K + 1) == K ? "-" : "").append(c);
        }
        return sb.reverse().toString().toUpperCase();
    }
}
```



