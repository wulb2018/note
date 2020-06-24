# 日期计算

## TIMESTAMPDIFF()

该函数可以计算两个日期的差值

> TIMESTAMPDIFF(YEAR,start_date,end_date)第一个参数是计算结果的单位，第二个参数是起始日期，第三个参数是终止日期
> ```
> SELECT `name` ,birth,CURDATE(),TIMESTAMPDIFF(YEAR,birth,CURDATE())  AS age FROM pet;
> ```

## 年月日

YEAR() 计算年份

MONTH() 计算月份

DAY() 计算日

DAYOFMONTH() 计算某月的第几天

CURDATE() 获取当前日期

## DATE_ADD() 增加日期

对当前日期的月份加一

```
SELECT `name` ,birth FROM pet WHERE MONTH(birth) = MONTH(DATE_ADD(CURDATE(),INTERVAL 1 MONTH));
```

另一种办法,是将月份对12取模再加1。需要先取模的原因是MONTH()返回1到12之间的数字，MOD(MONTH(CURDATE()),12)返回0到11的数字，例如当前月份为12就返回0，当前月份11时返回11。所以需要再取模后加1.

```
SELECT `name`,birth FROM pet WHERE MONTH(birth)=MOD(MONTH(CURDATE()),12)+1;
```

对日期加一

```
SELECT '2020-06-30' + INTERVAR 1 DAY;
```
结果是2020-07-01

```
SELECT '2020-06-31' + INTERVAL 1 DAY;
```

以上将产生警告，因为日期无效