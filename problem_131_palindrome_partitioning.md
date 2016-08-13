# Problem 131: Palindrome Partitioning


> https://leetcode.com/problems/palindrome-partitioning/

----------------------------------------
##思路

这道题非常好！如果能把这道题彻底搞明白，对理解排列组合公式是非常有帮助的。
1. 用path记录待排序元素，用result记录最终的结果
2. 单独的function来判断是否为palindrome，这个应该很快写出来才行
3. 核心的排列组合模板


----------------------------------
```java
public class Solution {
    
    List<String> path = new ArrayList<String>();
    List<List<String>> result = new ArrayList(path);
    
    public List<List<String>> partition(String s) {
        if (s == null) {
            return result;
        }
        helper(s, path, 0, result);
        
        return result;
    }
    
    private void helper(String s, List<String> path, int pos, List<List<String>> result) {
        if (pos == s.length()) {
            result.add(new ArrayList(path));
            return;
        }
        
        for (int i = pos + 1; i <= s.length(); i++) {
            String prefix = s.substring(pos, i);
            
            if(!isPalindrome(prefix)) {
                continue;
            }
            
            path.add(prefix);
            helper(s, path, i, result);
            path.remove(path.size() - 1);
        }
    }
    
    private boolean isPalindrome(String s) {
        int start = 0;
        int end = s.length() - 1;
        
        while (start < end) {
            if (s.charAt(start) != s.charAt(end)) {
                return false;
            }
            
            start++;
            end--;
        }
        return true;
    }
}
```
##易错点
1. 初始化
```java
List<String> path = new ArrayList<String>();
List<List<String>> result = new ArrayList(path);
```
List是一个接口，他的实现类是ArrayList。所以对于一个两层的List来说，要从里到外一层一层初始化。

 通常我们可以把他们放在最外面，作为整个类的变量，方便后面调用。

2. 判断是否palindrome
```java
private boolean isPalindrome(String s) {
    int start = 0;
    int end = s.length() - 1;
        
    while (start < end) {
        if (s.charAt(start) != s.charAt(end)) {
                return false;
        }
            
        start++;
        end--;
    }
    return true;
}
```
3. 退出条件
```java
if (pos == s.length()) {
    result.add(new ArrayList(path));
    return;
}
```
分割位置走到最后，自然退出

4. 循环条件
```java
path.add(prefix);
helper(s, path, i, result);
path.remove(path.size() - 1);
```
其中helper的调用中，```helper(s, path, i, result);```，始终是s，而不是prefix























