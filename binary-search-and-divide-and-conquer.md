# Binary search and Divide and Conquer

Binary search 非常 tricky，虽说道理简单，但是面试的时候却很容易出 bug，因此总结一下是必须的。

###终止条件不同

```
i <= j
```

```
i < j
```

###mid 的上下取向不同

```
i + (j - i) / 2
```

```
j - (j - i) / 2
```
###如何合理分半
分半的时候取 `mid`, `mid-1`, or `mid+1`

-----------
##举例

* **lc74: Search a 2D Matrix**： 这是一道普通的binary search。终止条件`i <= j`, mid 取向 `i + (j - i) / 2`, 分半的时候 = `mid - 1 or mid + 1`。

* **lc34: Search for a Range**：这道题需要终止条件`i < j`,
mid 取向两种都需要用到，分半的时候需要用到 = `mid`。我发现一般＝mid的时候，终止条件往往是`i < j`,不然会有死循环。

* 合理分半：下边这几道题都很tricky，分半的时候都有各自的特点，很不容易一次
写对。需要多多练习和体会。

```
lc33: Search in Rotated Sorted Array

lc81: Search in Rotated Sorted Array II

lc4: Median of Two Sorted Arrays
```
----------
##其他一些不容易看出来是 binary search 的题目

* lc29: Divide Two Integers：这题没做过面试也容易跪

* lc50: Pow(x, n)

* lc69: Sqrt(x)：其实算是一道典型的binary search题目，不过里边包括了几个tricky 的地方，很难一次写对

































