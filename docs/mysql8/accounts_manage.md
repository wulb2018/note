# 账户管理

## 添加账户，分配权限和删除账户

### 添加账户

以下语句创建一个vroot账户名，可在任意主机上连接，因为使用了通配符% 
```
CREATE USER 'vroot'@'%' IDENTIFIED BY 'yourpassword';
```

### 分配权限
以下对vroot账户进行权限分配，表示分配所有权限和所有数据库和表。
```
GRANT ALL ON *.* TO 'vroot'@'%' WITH GRANT OPTION;
```

检查账户的特权和属性

使用SHOW GRANTS 查看账户的特权
```
SHOW GRANTS FOR 'vroot'@'%';
```
使用SHOW CREATE USER 查看账户非特权属性
```
SET print_identified_with_as_hex=ON;

SHOW CREATE USER 'vroot'@'%'\G;
```
启用 print_identified_with_as_hex 系统变量（自MySQL 8.0.17起可用）会导致 SHOW CREATE USER将包含不可打印字符的哈希值显示为十六进制字符串而不是常规字符串文字。

撤销账户特权

```
REVOKE ALL ON *.* FROM 'vroot'@'%';
```

### 删除账户

使用DROP USER 删除账户
```
DROP USER 'vroot'@'%';
```

