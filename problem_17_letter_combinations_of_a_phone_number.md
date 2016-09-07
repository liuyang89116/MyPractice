# Problem 17: Letter Combinations of a Phone Number


> https://leetcode.com/problems/letter-combinations-of-a-phone-number/

--------
##思路
* 排列模板
* 先把每个数字对应的字母存到 HashMap 里，然后不停地罗列不同的排列

---------
```java
public class Solution {
    List<String> result = new ArrayList<String>();
    public List<String> letterCombinations(String digits) {
        if (digits == null || digits.length() == 0) {
            return result;
        }
        
        Map<Character, char[]> map = new HashMap<Character, char[]>();
        map.put('0', new char[] {});
        map.put('1', new char[] {});
        map.put('2', new char[] {'a', 'b', 'c'});
        map.put('3', new char[] {'d', 'e', 'f'});
        map.put('4', new char[] {'g', 'h', 'i'});
        map.put('5', new char[] {'j', 'k', 'l'});
        map.put('6', new char[] {'m', 'n', 'o'});
        map.put('7', new char[] {'p', 'q', 'r', 's'});
        map.put('8', new char[] {'t', 'u', 'v'});
        map.put('9', new char[] {'w', 'x', 'y', 'z'});
        
        StringBuilder sb = new StringBuilder();
        helper(map, sb, digits, result);
        
        return result;
    }
    
    private void helper(Map<Character, char[]> map, StringBuilder sb, String digits, List<String> result) {
        if (sb.length() == digits.length()) {
            result.add(sb.toString());
            return;
        }
        
        for (char c : map.get(digits.charAt(sb.length()))) {
            sb.append(c);
            helper(map, sb, digits, result);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```
---------
##易错点

1. 初始化数组
```java
char[] arr = new char[] {'a', 'b', 'c'};
```
注意右边不要把 “[]” 丢了
2. helper 退出条件
```java
if (sb.length() == digits.length()) {
         result.add(sb.toString());
         return;
}
```
3. 核心的遍历部分
```java
for (char c : map.get(digits.charAt(sb.length()))) {
          sb.append(c);
          helper(map, sb, digits, result);
          sb.deleteCharAt(sb.length() - 1);
}
```
4. StringBuilder 的方法
```java
StringBuilder sb = new StringBuilder();
sb.append('a');
sb.deleteCharAt(sb.length() - 1);
```
























