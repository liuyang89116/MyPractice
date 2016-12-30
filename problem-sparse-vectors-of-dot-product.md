# Problem: Sparse vectors of dot product



##思路
* 如果都是 sparse vector,那思路就是把每个 vector 都表示成 (index, non-zero value) pairs:
```
A =[0,2,0,2,0,0,3,0,0,4] ==> A={(1,2), (3,2), (6,3), (9,4)}
```
```
B=[0,0,0,0,5,0,2,0,0,8]  ==> B={(4,5), (6,2), (9,8)} 
```
* for each index i, a = val of pair (i, v_in_A), b= val of pair (i, v_in_B).  
dot_product(A,B) = sum_of ( a * b )

* 复杂度： `O(m + n)`
-----------
## Follow Up
> what if the number of nonzero elements of one vector is 10^10 and the other is 10^2, how can you make it faster?

* 这里的区别就是，一个特别长一个特别短。那么我们就先扫短的，然后用二分法再长的里面找对应的 index。复杂度应该是 `O(m * log n)`