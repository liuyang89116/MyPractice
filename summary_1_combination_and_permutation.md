# Summary 1: Combination and Permutation

1. 组合 Vs. 排列：  
组合类的题目（eg.Problem 78: Subsets），就是不断往里面放元素，放进 path 的就立马可以 add 到 rst 里面。组合类题目，在选元素的时候，比较关注位置 pos。  
排列的问题，第一要考虑退出的条件-也就是什么情况下可以加元素。通常，当 path 的集合元素和原先集合的元素个数相等的时候，就可以加到 rst 里面了。第二个不同的地方是，要标记是否访问过当前元素。
