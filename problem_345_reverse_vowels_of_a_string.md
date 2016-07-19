# Problem 345: Reverse Vowels of a String


> https://leetcode.com/problems/reverse-vowels-of-a-string/

-------------------------------------------------------
```java
public class Solution {
    public String reverseVowels(String s) {
        HashSet<Character> hs = new HashSet<Character>();
        hs.add('a');
        hs.add('e');
        hs.add('i');
        hs.add('o');
        hs.add('u');
        hs.add('A');
        hs.add('E');
        hs.add('I');
        hs.add('O');
        hs.add('U');

        int[] pos = new int[s.length()];   //record vowel character position
        int count = 0;                   //record vowel number
        for (int i = 0; i < s.length(); i++) {
            if (hs.contains(s.charAt(i))) {
                pos[count] = i;
                count++;
            }
        }

        char[] ans = s.toCharArray();
        for (int i = 0; i < count; i++) {
            ans[pos[i]] = s.charAt(pos[count - 1 - i]);
        }

        return String.valueOf(ans);
    }
}
```
---------------------------

## 易错点
1. HashSet是去重复的有利手段；HashMap则是用来储存键值对的;
2. 思路：
   用count来记录元音元素；用一个数组pos来记录他们的位置
   ```java
   if (hs.contains(s.charAt(i))) {
          pos[count] = i;
          count++;
   }
   ```
3. length方法

|data structure|方法|描述|
| --| -- | -- |
|Array| s.length | 没括号 |
| String |s.length() |有括号 |
|List|s.size()|有括号|



4.**String转Array**
```char[] ans = s.toCharArray();```

5.**Array转String**
```
String.valueOf(ans);
```

6.互换元素的index关系
 ```ans[pos[i]] = s.charAt(pos[count - 1 - i]);```

