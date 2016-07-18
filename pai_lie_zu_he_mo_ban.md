# summary1: subsets

这是一段经典的排列组合模板。

```java
void subsets(int[] num) {
	ArrayList<Integer> path = new ArrayList<Integer>();
	Arrays.sort(num);
	subsetsHelper(path, num, 0);
}

void subsetsHelper(ArrayList<Integer> path, int[] num, int pos) {
	outputToResult(path);

	for (int i = pos; i < num.length; i++) {
		path.add(num[i]);
		subsetsHelper(path, num, i + 1);
		path.remove(path.size() - 1);
	}
}
```



