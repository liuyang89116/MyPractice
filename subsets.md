# Subsets Summary
* 求子集主要是通过 pos 来记录当前的进程，永远都是取后面的没有取过的元素。他和 permutation 不同的是，permutation 是通过 `visited[]` 数组来记录。因为 permutation 每次都要把所有元素取一遍，for 循环的时候实际上都要经历一遍。
* 没有重复元素的时候，Array 不需要 sort，取谁不取谁只和他们的位置有关系。而如果数组里有重复元素的话，就要 sort，去重的时候需要。
