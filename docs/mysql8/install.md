# 安装

mysql手册原地址 https://dev.mysql.com/doc/refman/8.0/en/linux-installation-yum-repo.html

下载rpm包
wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
安装下载好的包
```
yum install mysql80-community-release-el7-3.noarch.rpm
```
开始安装mysql8
```
sudo yum install mysql-community-server
```
启动服务器（在sentos7以上linux的命令）
```
systemctl start mysqld
```
设置随系统启动
```
systemctl enable mysqld
```
关闭随系统启动
```
systemctl disable mysqld
```
查看mysql的状态
```
systemctl status mysqld
```
安装后查看初始密码
```
sudo grep 'temporary password' /var/log/mysqld.log
```
```
2020-06-23T03:44:06.266653Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: nRqa9si-oyP2
```
通过使用生成的临时密码登录并尽快更改root密码，并为超级用户帐户设置自定义密码
```
mysql -uroot -p
```
修改默认密码
```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';
```
>注意
validate_password 默认情况下已安装。通过实施的默认密码策略validate_password要求密码至少包含一个大写字母，一个小写字母，一位数字和一个特殊字符，并且密码总长度至少为8个字符。

创建用户用于windows连接
```
create user 'vroot'@'%' identified by 'MyNewPass4!';
```
赋权
grant all on *.* to 'vroot'@'%';
```
刷新权限
```
flush privileges;
```