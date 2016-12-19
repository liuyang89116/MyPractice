# Problem 299: Bulls and Cows

> https://leetcode.com/problems/bulls-and-cows/

--------
##思路
* 我们的目标就是扫一遍数组，然后在对应位置上吻合的，`bull++`
* 然后判断`cow`。如果在原来的 secret 里出现，对应的数组加 1；如果在 guess 里面出现，对应的数组就减 1；
* 所以我们可以看到，如果数组小于 0，说明之前有 guess 来过，这时正好是 secret 来访问的话，他俩正好凑成一对儿，`cow++`；数组大于 0，说明有 secret 来过，这是 guess 来访问的话，`cow--`。

------------
