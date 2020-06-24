# ORDER

排序时如果需要区分字母大小写可以使用BINARY
```
SELECT `name`,birth FROM pet ORDER BY BINARY `name`;
```

多列排序

```
SELECT `name`,species,birth FROM pet ORDER BY apecies ASC,birth DESC;
```
apecies ASC 按apecies 进行升序，birth DESC按birth进行降序。