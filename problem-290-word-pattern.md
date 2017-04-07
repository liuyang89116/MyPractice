# Problem 290: Word Pattern

> https://leetcode.com/problems/word-pattern/\#/description

-------------

## 思路

* 通过一个 map 来建立 pattern 和 String 元素的对应关系，方便只有的对应比较。

-----

```java
public class Solution {
    public boolean wordPattern(String pattern, String str) {
        String[] words = str.split(" ");
        if (pattern.length() != words.length) return false;
        
        Map<Character, String> map = new HashMap<>();
        for (int i = 0; i < pattern.length(); i++) {
            char c = pattern.charAt(i);
            if (map.containsKey(c)) {
                if (!map.get(c).equals(words[i])) return false;
            } else {
                if (map.containsValue(words[i])) return false;
                
                map.put(c, words[i]);
            }
        }
        
        return true;
    }
}
```



