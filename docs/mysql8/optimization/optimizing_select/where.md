# where优化（子句优化）

- 在表储存引擎为MyISAM或者MEMORY时使用COUNT(*) 函数且不加where子句时可快速查询到缓存信息，或者仅使用NOT NULL
- 如果索引列是数字，MYSQL仅使用索引树来解析