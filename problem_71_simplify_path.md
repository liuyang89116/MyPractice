# Problem 71: Simplify Path


> https://leetcode.com/problems/simplify-path/

------------
##思路
* 这道题就是把原来的 String split 开，然后再拼接成新的字符串
* 需要注意的几个 corner cases: (1) Did you consider the case where path = "/../"? In this case, you should return "/". (2) Another corner case is the path might contain multiple slashes '/' together, such as "/home//foo/". In this case, you should ignore redundant slashes and return "/home/foo".

------
```java
public class Solution {
    public String simplifyPath(String path) {
        String result = "/";
        String[] arr = path.split("/");
        ArrayList<String> buildPath = new ArrayList<String>();
        for (String s : arr) {
            if (s.equals("..")) {
                if (buildPath.size() > 0) {
                    buildPath.remove(buildPath.size() - 1);
                }
            } else if (!s.equals(".") && !s.equals("")) {
                buildPath.add(s);
            }
        }
        
        for (String str : buildPath) {
            result += str + "/";
        }
        
        if (result.length() > 1) {
            result = result.substring(0, result.length() - 1);
        }
        
        return result;
    }
}
```
-------
##易错点

1. equals() 和 ==
```java
if (s.equals("..")) {
         if (buildPath.size() > 0) {
               buildPath.remove(buildPath.size() - 1);
         }
} else if (!s.equals(".") && !s.equals("")) {
         buildPath.add(s);
}
```
equals() 方法比较的是 String 的内容是否相同；而 “==” 比较的是两个 Object 是否是同一个，比的是地址值。
2. 最后去掉末尾的 “/”
```java
if (result.length() > 1) {
         result = result.substring(0, result.length() - 1);
}
```




























