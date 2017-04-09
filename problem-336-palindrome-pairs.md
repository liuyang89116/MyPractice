# Problem 336: Palindrome Pairs

> https://leetcode.com/problems/palindrome-pairs/\#/description

-------

![](/assets/336_1.png)

------

## 思路

* 总体的思路就是遍历每个 word， 然后把它拆分成 `str1` 和 `str2` 两个字符串。
* 如果 str1 已经是回文，那么我们只需要给 str2 找个伴儿即可 ！

----------

```java
public class Solution {
    public List<List<Integer>> palindromePairs(String[] words) {
        Set<List<Integer>> set = new HashSet<>();
        List<List<Integer>> rst = new ArrayList<>();
        if (words == null || words.length == 0) return rst;
        
        Map<String, Integer> map = new HashMap<>();
        for (int i = 0; i < words.length; i++) {
            map.put(words[i], i);
        }
        for (int i = 0; i < words.length; i++) {
            for (int j = 0; j <= words[i].length(); j++) {
                String str1 = words[i].substring(0, j);
                String str2 = words[i].substring(j);
                if (isPalindrome(str1)) {
                    String str2rvs = new StringBuilder(str2).reverse().toString();
                    if (map.containsKey(str2rvs) && map.get(str2rvs) != i) {
                        List<Integer> list = new ArrayList<>();
                        list.add(map.get(str2rvs));
                        list.add(i);
                        set.add(list);
                    }
                }
                if (isPalindrome(str2)) {
                    String str1rvs = new StringBuilder(str1).reverse().toString();
                    if (map.containsKey(str1rvs) && map.get(str1rvs) != i) {
                        List<Integer> list = new ArrayList<>();
                        list.add(i);
                        list.add(map.get(str1rvs));
                        set.add(list);
                    }
                }
            }
        }
        rst = new ArrayList(set);
        
        return rst;
    }
    
    private boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        while (left <= right) {
            if (s.charAt(left) != s.charAt(right)) return false;
            left++;
            right--;
        }
        
        return true;
    }
}



```





























