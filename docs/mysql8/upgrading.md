# mysql8与之前版本的差异


* [caching_sha2_password作为首选身份验证插件]()
* [配置变更]()
* [服务器变更]()
* [InnoDB的变化]()
* [SQL变更]()

<a name="caching_sha2_password作为首选身份验证插件">caching_sha2_password作为首选身份验证插件</a>

caching_sha2_password和sha256_password认证插件与原本的mysql_native_password认证插件比价，提供了更加安全的密码加密。并且caching_sha2_password的加密性能比sha256_password更好。因此caching_sha2_password是mysql8的默认的身份验证插件，此更改会影响服务器和libmysqlclient客户端库：
- 对于mysql服务器default_authentication_plugin系统变量的默认值从mysql_native_password改为caching_sha2_password。
此更改仅适用于对mysql服务器升级到mysql8.0及更高版本后新创建的账户，对于升级前就已经存在的账户还是保持原来的mysql_native_password插件。如果希望将旧的账户也切换成caching_sha2_password的话可以使用一下ALTER USER语句：
```
ALTER USER user IDENTIFIED WITH caching_sha2_password BY 'password';
```
- caching_sha2_password的兼容性问题临时性解决方案
> ### 重要
> 如果mysql客户端与mysql8不兼容可以使用一下方案：
> ```
> [mysqld]
> default_authentication_plugin=mysql_native_password
> ```
> 该设置使之前版本的客户端可以连接到mysql8，但是应该是临时的方案而不是长期永久方案
> 另外还有一种临时性方案是只将某个账户的验证方式改为mysql_native_password
> ```
> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
> ```

## caching_sha2_password和复制
主/从复制和从/副本连接也都是使用caching_sha2_password验证身份

主/从账户要连接到caching_sha2_password：
- 使用一下CHANGE MASTER TO 选项：
```
MASTER_SSL=1
GET_MASTER_PUBLIC_KEY=1
MASTER_PUBLIC_KEY_PATH='path to RSA publi key file'
```
- 或者是在启动mysql服务器时提供密钥，则可以使用与RSA公钥相关的选项

要连接到caching_sha2_password组复制账户：

- 对于使用OpenSSL构建的mysql请设置一下系统变量：
```
SET GLOBAL group_relication_recovery_use_ssl=ON;
SET GLOBAL group_replication_recovery_get_public_key=1;
SET GLOBAL group_replication_recovery_public_key_path ='path to RSA public key path'
```
启动服务器是如果提供密钥则可以使用与RSA公钥相关的选项