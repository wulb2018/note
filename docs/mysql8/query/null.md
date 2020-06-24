# 有关于NULL

NULL值只能使用<u>IS NULL</u>和<u>IS NOT NULL</u>运算符
```
mysql> SELECT 1 IS NULL ,1 IS NOT NULL;
```

不能使用 = ,<, >或者<>

 NULL与任何算术比较的结果都是NULL,所以此类比较没有意义

 在mysql中，1或NULL表示false,其他的表示true.布尔运算的默认真值是1

 在ORDER BY中对含有NULL的列进行排序时,按ASC排序时NULL将排在前面，按DESC排序时将排在后面