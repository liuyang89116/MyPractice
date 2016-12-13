# Problem 271: Encode and Decode Strings

> https://leetcode.com/problems/encode-and-decode-strings/

------
![](/assets/271_0.png)
![](/assets/271_1.png)

--------
##思路
* 我们可以维护一个 StringBuilder，读出每个 input string 的长度，append 一个特殊字符，例如 '/'，再 append string。
* decode 的时候我们就可以利用 java 的 String.indexOf(char，startIndex)来算出自 startIndex 其第一个 '/' 的位置，同时计算出接下来读取的 string 长度，用 String.substring() 读出字符串以后我们更新 index，来进行下一次读取。

-----------
##复杂度
* Time: `O(n)`
* Space: `O(1)`

--------

```java
public class Codec {

    // Encodes a list of strings to a single string.
    public String encode(List<String> strs) {
        if (strs == null || strs.size() == 0) {
            return "";
        }
        
        StringBuilder sb = new StringBuilder();
        for (String s : strs) {
            int len = s.length();
            sb.append(len);
            sb.append("/");
            sb.append(s);
        }
        
        return sb.toString();
    }

    // Decodes a single string to a list of strings.
    public List<String> decode(String s) {
        List<String> rst = new ArrayList<>();
        if (s == null || s.length() == 0) {
            return rst;
        }
        
        int index = 0;
        while (index < s.length()) {
            int slashIndex = s.indexOf("/", index);
            int len = Integer.parseInt(s.substring(index, slashIndex));
            rst.add(s.substring(slashIndex + 1, slashIndex + 1 + len));
            index = slashIndex + 1 + len;
        }
        
        return rst;
        
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(strs));
```
-------
##易错点
1. String.indexOf() 方法

```java
int slashIndex = s.indexOf("/", index);
```
这里 index，充当的是“起始位置”，也就是说，从这个位置开始以后看有没有 "/"































