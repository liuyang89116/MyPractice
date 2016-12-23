# Problem 273: Integer to English Words

> https://leetcode.com/problems/integer-to-english-words/

--------
##思路
* 这道题首先把思路搞清楚：20 以下的数不规律，单独成组；各种 ty 数单独成组；最后就是大数
* 这里的 redix 和 dexWord 实际上是对应的。
* 这里最巧妙的一点是在大数的判断中间用了一次递归

------------


```java
public class Solution {
    public String numberToWords(int num) {
        if (num == 0) return "Zero";
        
        String[] lessThan20 = new String[] {"", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
        String[] tyWord = new String[] {"", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
        String[] dexWord = new String[] {"Billion", "Million", "Thousand", "Hundred"};
        int[] radix = new int[] {1000000000, 1000000, 1000, 100};
        
        StringBuffer sb = new StringBuffer();
        int count = 0;
        for (int i = 0; i < radix.length; i++) {
            count = num / radix[i];
            num %= radix[i];
            if (count == 0) continue;
            sb.append(numberToWords(count) + " ");
            sb.append(dexWord[i] + " ");
        }
        if (num < 20) {
            count = num % 20;
            sb.append(lessThan20[count]);
        } else {
            count = num / 10;
            sb.append(tyWord[count] + " ");
            count = num % 10;
            sb.append(lessThan20[count]);
        }
        
        return sb.toString().trim();
    }
}

```

--------
##易错点
1. 最后整体 trim
2. 判断大数的时候用递归，否则没有 "One"，"Two",……这些再最前面
```java
sb.append(numberToWords(count) + " ");
```
3. 用 StringBuffer 节省 space































