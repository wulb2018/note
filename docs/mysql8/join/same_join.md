# 各种连接

- 内部非等额连接

```
SELECT * FROM t1 JOIN t2 ON t1.c1<t2.c1;
```

- 半连接

```
SELECT * FROM t1 WHERE t1.c1 IN(SELECT t2.c2 FROM t2);
```

- 反连接

```
SELECT * FROM t2 WHERE NOT EXISTS(SELECT * FROM t1 WHERE t1.col1=t2.col1);
```

- 左外连接

```
SELECT * FROM t1 LEFT JOIN t2 ON t1.c1=t2.c1;
```

- 右外连接

```
SELECT * FROM t1 RIGHT JOIN t2 ON t1.c1=t2.c1;
```

>注意
>以上连接在mysql 8.0.20及更高版本中都使用哈希连接
>