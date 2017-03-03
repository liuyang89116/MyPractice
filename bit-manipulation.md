# Bit Manipulation

> [https://discuss.leetcode.com/topic/50315/a-summary-how-to-use-bit-manipulation-to-solve-problems-easily-and-efficiently](https://discuss.leetcode.com/topic/50315/a-summary-how-to-use-bit-manipulation-to-solve-problems-easily-and-efficiently)

* 这个帖子讲得非常好！

## XOR \(^\) tricks

* XOR 主要用来剔除掉**偶数个的相同元素**，而生下来单独存在的元素
* 特性： 

\(1\) 恒等律：`A ^ 0 = A`

\(2\) 归零律:  `A ^ A = 0`

相同的元素互相抵消；任何元素与 0 异或得到本身。

### eg1: 不使用其他空间，交换两个值

```
a = a ^ b;    
b = a ^ b;   // b = a ^ b = a ^ b ^ b = a ^ 0 = a
a = a ^ b;   // a = a ^ a ^ b = b
```

### eg2: Missing Number

> Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array. For example, Given nums = \[0, 1, 3\] return 2. \(Of course, you can do this by math.\)




