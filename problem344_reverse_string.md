# Problem344: Reverse String


> https://leetcode.com/problems/reverse-string/

基础题， 这道题的关键在于，学会数组和字符串之间的互相转换

```java
public class Solution {
	public String reverseString(String s) {
		char[] arr = s.toCharArray();
		for (int i = 0; i < arr.length; i++) {
			arr[i] = s.charAt(s.length() - 1 - i);
		}
		return String.valueOf(arr);
	}
}
```