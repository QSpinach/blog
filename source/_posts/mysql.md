---
tags: [Mysql]
comments: true
toc: true
---



### -----设置默认值

若本身存在默认值，则先删除
alter table表名alter column字段名drop default; 
然后设置默认值（若本身不存在则可以直接设定）
alter table表名 alter column字段名 set default默认值;



### ------设置数据库导入文件最大容量
set global max_allowed_packet = 2*1024*1024*10;
show VARIABLES like '%max_allowed_packet%';

### ------查看编码 修改编码
show VARIABLES like '%char%'

[mysqld]
character_set_server=utf8

### ------MySql “Row size too large (> 8126)”解决办法在my.ini中加入
[mysqld]
innodb_log_file_size = 512M
innodb_strict_mode = 0

### ---------------------Redis
redis-cli.exe
127.0.0.1:6379>shutdown
not connected>exit

启动命令
redis-server redis.windows.conf
设置服务命令
redis-server --service-install redis.windows-service.conf --loglevel verbose

卸载服务：
redis-server --service-uninstall
启动服务
redis-server --service-start
停止服务
redis-server --service-stop

--------------------------------------------------------------

### mysql更改root密码
#1.停止mysql数据库
/etc/init.d/mysqld stop

#2.执行如下命令
mysqld_safe --user=mysql --skip-grant-tables --skip-networking &

#3.使用root登录mysql数据库
mysql -u root mysql

#4.更新root密码
mysql> UPDATE user SET Password=PASSWORD('xxx123') where USER='root';
#最新版MySQL请采用如下SQL：
mysql> UPDATE user SET authentication_string=PASSWORD('xxx123') where USER='root';

#5.刷新权限 
mysql> FLUSH PRIVILEGES;

#6.退出mysql
mysql> quit

#7.重启mysql
/etc/init.d/mysqld restart

#8.使用root用户重新登录mysql
mysql -uroot -p 
Enter password: <输入新设的密码newpassword>