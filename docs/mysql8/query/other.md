# 其他内容

## 使用用户定义的变量

可以使用mysql用户变量来记住结果，而不必使用客户端的临时变量来储存。

```
SELECT @min_price:=MIN(price),@max_price:=MAX(price) FROM shop;
SELECT * FROM shop WHERE price=@min_price OR price=@max_price;
```
