# 函数

## 二进制函数
- BIT_COUNT() ： 用来计算二进制数中包含1的个数。如： 100101这个计算结果BIT_COUNT(100101)=3

- BIT_OR() ： 进行二进制数的或运算，在group by 时同组中每行的二进制数进行或运算，如： 10010 或 11000 等于 11010

> 上述两个函数可结合用于计算用户每月访问网页天数的案例，可以代替使用DISTINCT去重复的方案。