# Problem 318: Maximum Product of Word Lengths

> [https://leetcode.com/problems/maximum-product-of-word-lengths/?tab=Description](https://leetcode.com/problems/maximum-product-of-word-lengths/?tab=Description)

---

## 思路

* 这道题很有意思。解法里用 `count[i]` 来表明对应的 `word[i]`的每一位上的字母的情况。这里的 `word[i]`是用二进制表示的，从右向左代表 `abcde...xyz`这几个数
* 最后循环一遍以后，判断最大值是多少。这里 check 的时候用 `&`来判断两个数是否是“没有 share 的元素”

---------

```java
public class Solution {
    public int maxProduct(String[] words) {
        if (words == null || words.length == 0) return 0;
        
        int len = words.length;
        int[] count = new int[len];
        for (int i = 0; i < len; i++) {
            String word = words[i];
            count[i] = 0;
            for (int j = 0; j < word.length(); j++) {
                count[i] |= 1 << (word.charAt(j) - 'a');
            }
        }
        
        int product = 0;
        for (int i = 0; i < len; i++) {
            for (int j = i + 1; j < len; j++) {
                if ((count[i] & count[j]) == 0 && words[i].length() * words[j].length() > product) {
                    product = words[i].length() * words[j].length();
                }
            }
        }
        
        return product;
    }
}
```



