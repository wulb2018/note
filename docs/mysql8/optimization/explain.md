# explain输出说明

提供两种输出方式，一种是表格一种是json,FORMAT=JSON

## 输出的列

| 列名 | json名称 | 含义 |
| ---- |  ----   |----  |
| id   |select_id|该SELECT的标识符|
| select_type | 没有 | 该SELECT的类型|
| table | table_name| 查询的表名|
| partitions|partitions|匹配的分区|
| type | access_type | join类型|
| possible_keys | possible_keys| 可能选择的索引|
| key | key | 实际选择的索引|
| key_len | key_len | 所选择的索引的长度|
| ref | ref| 与索引比较的列|
| rows | rows | 估计要检查的行数|
| filtered | filtered | 按条件过滤的行数的百分比|
| Extra | 没有| 附加信息|

## 列的详细解释

- id(JSON名：select_id)

SELECT的标识符。这是SELECT查询中的序号。如果该行引用其他的行的并集结果，则该值为NULL（例如：使用union连接两个表）。在这种情况下，该table的值以< union M , N > 格式显示（其中MN为引用的行的id）表明该行引用的行的并集

- select_type (JSON名称：无)

SELECT的类型，所有类型如下表。JSON格式的explain除了SIMPLE和PRIMARY外都将其显示为属性query_block ，具体见表格

| select_type值 | JSON名称 | 含义 |
| ------------- | -------- | --- |
| SIMPLE        | 没有    | 简单SELECT|
| PRIMARY       | 没有    | 最外层的SELECT|
| UNION         | 没有    | SELECT 使用union时会出现，一般是在第二个表|
| DEPENDENT UNION | dependent(true)| 在第二个或者后面一个的SELECT语句出现，从属于于外部的查询|
| UNION RESULT | union_result | UNION的结果，id=null|
| SUBQUERY     | 没有       | 第一个SELECT子查询|
| DEPENDENT SUBQUERY | dependent(true) | 在第一个SELECT子查询中，从属于外部查询|
| DERIVED      | 没有       | 派生表|
| DEPENDENT DERIVED | dependent(true)| 派生表依赖于另一个表|
| MATERIALIZED | materialized_from_subquery | 物化子查询|
| UNCACHEABLE SUBQUERY | cacheable(false)| 子查询，其结果无法缓存，必须针对外部查询的每一行重新进行评估|
| UNCACHEABLE UNION | cacheable(false) | 在UNION的无缓存子查询中的第二个或后面的SELECT查询|

- table (JSON名：table_name)
输出行所引用的表的名称。也可以是一下值之一：
 - <union M , N> : 该行是指具有id值的行M和N的并集。
 - <derived N>: 该行的N是指涉及的派生表的id的值，派生表可能来自于from子句中的子查询。
 - <subquery N>: 该行的N 是指物化子查询的结果id的值

- partitions(JSON名：partitions)

该值为非NULL时是查询匹配的分区，未分区的表该值未NULL

- type (JSON名：access_type)

join类型

- possible_keys(JSON名：possible_keys)
该列显示在表中可以选择的索引。此列完全独立于输出中显示的表顺序。此列为NULL 则没有相关的索引

- key (JSON名：key)
该列指示MySQL实际使用的索引。key 的索引有可能不在possible_keys中。

- key_len(JSON名：key_length)
该列指示MySQL决定使用的key的长度。key_len能够确定MySQL实际使用多少部分的键，如果key为NULL则key_len也为NULL。

- ref (JSON名：ref)
该列显示将哪些列或者常量与该key列中的索引进行比较进行查询。

如果值为func，则使用的值是某函数的结果。要查看是哪个函数，在EXPLAIN之后可以使用SHOW WARNINGS 查看。

- rows (JSON 名：rows)
该列指示MySQL认为执行查询必须检查的行数。

对于InnoDB表。此数字是估计值可能并不总是准确的。

- filtered (JSON 名：filtered)
该列表示将被条件过滤的表行的估计百分比。最大值是100，这表示未过滤行。值从100减少表示过滤量在增加。rows*filtered显示了将与后面的表连接的行数。例如，如果rows为1000且filtered为50（50%），则与后面表连接的行数为1000*50%=500.

Extra(JSON名：无)

此列包含有关于MySQL如何解析查询的其他信息。没有对应的JSON属性。但是可能出现其他属性。