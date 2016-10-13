# Problem 388: Longest Absolute File Path


> https://leetcode.com/problems/longest-absolute-file-path/

--------
##思路
* 解法参考自这里  
> http://www.cnblogs.com/grandyang/p/5806493.html
* 这道题给了我们一个字符串，里面包含\n和\t这种表示回车和空格的特殊字符，让我们找到某一个最长的绝对文件路径，要注意的是，最长绝对文件路径不一定是要最深的路径
* 我们可以用哈希表来建立深度和当前深度的绝对路径长度之间的映射，那么当前深度下的文件的绝对路径就是文件名长度加上哈希表中当前深度对应的长度，我们的思路是遍历整个字符串
* 遇到\n或者\t就停下来，然后我们判断，如果遇到的是回车，我们把这段文件名提取出来，如果里面包含'.'，说明是文件，我们更新res长度，如果不包含点，说明是文件夹，我们深度 level 自增1，然后建立当前深度和总长度之间的映射，然后我们将深度 level 重置为0
* 之前如果遇到的是空格\t，那么我们深度加一，通过累加\t的个数，我们可以得知当前文件或文件夹的深度，然后做对应的处理

-----------
```java
public class Solution {
    public int lengthLongestPath(String input) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        map.put(0, 0);
        int rst = 0;
        for (String s : input.split("\n")) {
            int level = s.lastIndexOf("\t") + 1;
            int len = s.substring(level).length();
            if (s.contains(".")) {
                rst = Math.max(rst, map.get(level) + len);
            } else {
                map.put(level + 1, map.get(level) + len + 1);
            }
        }
        
        return rst;
    }
}
```
---------
##易错点
1. 为什么用 lastIndexOf()
```java
int level = s.lastIndexOf("\t") + 1;
```
因为有时候会有好几个```\t```，我们要定位的是最后一个，然后接下来就是后面的文件夹或者文件
2. 最开始 map 里要先放东西
```java
map.put(0, 0);
```

























