# Problem 291: Word Pattern II

> [https://leetcode.com/problems/word-pattern-ii/\#/description](https://leetcode.com/problems/word-pattern-ii/#/description)

---

![](/assets/291.png)

---

## 思路

* 这道题没有了之前天然的空格分隔，所以在识别的时候比之前更加困难。
* 我们可以用一个递归，同时用一个 map 来对应每个 pattern 的 character。这样在每次递归的时候，都可以同时切割 pattern 和 string，再往跟深的地方走。
* 当 map 中没有当前character的对应的时候，我们可以先添加这个 character和对应的 value，然后继续递归。这里要注意一点：记得递归完 remove 了这个键值对

-------

```java
public class Solution {
    Map<Character, String> map = new HashMap<>();
    public boolean wordPatternMatch(String pattern, String str) {
        if (pattern.length() == 0) return str.length() == pattern.length();
        
        if (map.containsKey(pattern.charAt(0))) {
            String value = map.get(pattern.charAt(0));
            if (value.length() > str.length() || !str.substring(0, value.length()).equals(value)) return false;
            if (wordPatternMatch(pattern.substring(1), str.substring(value.length()))) return true;
        } else {
            for (int i = 1; i <= str.length(); i++) {
                if (map.containsValue(str.substring(0, i))) continue;
                map.put(pattern.charAt(0), str.substring(0, i));
                if (wordPatternMatch(pattern.substring(1), str.substring(i))) return true;
                map.remove(pattern.charAt(0));
            }
        }
        
        return false;
    }
}
```



