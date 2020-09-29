---
tags: [Linux]
comments: true
toc: true
---



### 命令

```
	sudo apt-get update 更新软件源
	cd 进入某文件夹 cd - 快速回到上传路径
	ls 显示目录下所有文件
	mkdir 创建文件夹 mkdir a/b/c/d -p 创建文件夹
	touch 创建文件
	pwd 显示当前目录地址
	q 退出当前（man ls ）
	clear 清除终端显示信息
	tab键 自动补全文件名
	cat 查看文件内容 小文件适用
	history 显示历史命令
	! + 历史命令行号 执行对应命令
	rm 删除文件或文件夹 rm -r 递归地删除目录下的内容 删除文件夹
	rmdir 只能删非空文件夹

	* 是通配符（ls 2* 显示以2开头文件或目录)
	？是通配符（ls 2? 显示以2开头的两位名文件或目录）
	[] 通配符 （ls 1[1-5]3.txt 显示指定范围的文件和文件夹）
	> 重定向 （ls > xxx.txt 如果有xxx.txt文件，先删除xxx.txt内容删掉，再把显示在终端的信息放到文件里面。如果没有就直接生成文件再添加内容）
	>> 重定向追加 （ls >> xxx.txt 把内容放到文件里面的末尾）
	more 查看文件内容 （f往下翻， b往回撤 ） 大文件适用
	| 管道 （ls -alh /bin | more）将显示的内容分页显示 通过 | 进行分流
	ctrl + c 终止
	mv 源文件名 新文件名 (重命名文件或文件夹)
	mv 源文件 文件夹路径 剪切并粘贴到文件路径
	cp 文件 文件路径 复制粘贴， cp -r 复制粘贴文件夹
	ln -s 对谁创建快捷方式 创建后的文件名 （软链接）
	ln 对谁创建快捷方式 创建后的文件名 （硬链接） 删除原文件不影响创建后的文件
	ls -lh 查看文件的链接数
	grep -n "ntfs" xxx.txt 在xxx.txt文件中查找ntfs， -n是显示行号，-v 显示不包含ntfs的内容

	:wq 保存退出 :q! 不保存退出
	
	tar -cvf test.tar *py 打包所有py文件倒test.tar
	tar -xvf test.tar 解包
	tar -zcvf xxx.tar.gz *py 压缩 -C /dongge 指定路径
	tar -zxvf xxx.tar.gz 解压
	tar -jcvf yyy.tar.bz2 *py 压缩
	zip zzz.zip *py
	unzip zzz.zip, unzip -d /test4 zzz.zip 解压到指定路径
	
	wich ls 查看命令所在的文件路径
	
	cal 打印日历 -y 2018 打印2018年日历
	date "+%Y-%m-%d" 打印时间
	
	ps -aux 显示进程
	top 动态显示进程
	top 显示进程
	ps -ef|grep tomcat 查找相应进程
	kill -9 9909 杀死进程， -9 强制杀死进程
	
	reboot 重启
	shutdown -h （now或10或 20:20） 关机 指定时间
	
	df -h 查看硬盘使用情况
	du -h 显示当前路径使用情况
	ifconfig 显示网络信息
	ping 检查是否能网络连通
	
	sudo useradd shuaige -m 创建用户
	cat /etc/passwd 查看有多少账户
	su shuaige 切换shuaige用户
	sudo passwd shuaige 更新密码
	ssh python@172.16.7.139 远程登录电脑
	whoami 显示当前登录用户
	exit 退出当前用户
	
	文件权限
	rwx 可读 可写 可执行 
	r-- 只能读
	r-x 可读 可执行 但是不能写
	
	chmod u=rwx 2.py 修改权限 拥有者u
	chmod g=rwx 2.py 修改权限 同组者g
	chmod o=rwx 2.py 修改权限 其他o
	777 

```

***


### vim操作

------------------------vim-------------------------------------
```
i 光标前插入
a 光标后插入
esc 退出编辑模式
:wq 保存并退出
o 下一行插入
I 行首
A 行尾
O 上一行插入
yy 复制光标所在一行
4yy 复制光标所在的行开始向下4行
p 粘贴
dd 剪切 删除光标所在的行
2dd 剪切 删除光标所在的行往下2行
D 剪切当前行光标后的所有内容
d0 剪切当前行光标前的所有内容
x 删除光标后的内容
X 删除光标前的内容
h 左 j下 k上 l右
H 当前屏幕的上方
M 当前屏幕中间
L 当前屏幕的下方

Ctrl + f 向下翻一页
Ctrl + b 向上翻一页
Ctrl + d 向下翻半屏
Ctrl + u 向上翻半屏

2G 快速定位到第二行
G 快速调到整个代码的最后一行
gg 快速回到整个代码的第一行

w 向后跳一个单词的长度， 即跳到下一个单词的开始处
b 向前跳一个单词的长度， 即跳到上一个单词的开始处

u 撤销刚刚的操作
Ctrl + r 反撤销

v 选择
V 选择光标经过的行

>> 向右移动代码
<< 向左移动代码

. 重复执行上一次的命令

/hello 查找hello
n 下一个hello
N 上一个hello

r 替换一个字符
R 替换光标以及后边的字符
:%s/abc/123/g abc全部替换为123
:1, 10s/abc/123/g 第一行到第10行的abc全部替换为123

shift + zz 相当于wq

末行模式
w 保存
q 退出
wq 保存并退出

```
***

======================================================
### centos安装ss
1、安装应用
```
yum install python-setuptools
easy_install pip
pip install shadowsocks
```

2、配置文件
```
mkdir /etc/shadowsocks
vim /etc/shadowsocks/ss.json
// 单用户
{
    "server":"0.0.0.0",
    "server_port":9000,           //服务端口
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"123456",          //服务密码
    "timeout":300,
    "method":"aes-256-cfb",      //加密方式
    "fast_open":false,
    "workers": 1
}
// 多用户一定要开启防火墙端口号
{
    "server":"0.0.0.0",
    "server_port":9000,           //服务端口
    "port_passowrd": {
    	"9000":"123456",
    	"9001":"12345678"
    },
    "local_address":"127.0.0.1",
    "local_port":1080,
    "timeout":300,
    "method":"aes-256-cfb",      //加密方式
    "fast_open":false,
}
```

3、运行
此方法可能无效
```
ssserver -c /etc/shadowsocks/ss.json -d start 
ssserver -c /etc/shadowsocks/ss.json -d stop       //停止
ssserver -c /etc/shadowsocks/ss.json -d restart    //重启
```

推荐使用以下方式运行
```
vim /usr/lib/systemd/system/ss.service
[Unit]
Description=Shadowsocks Server
After=network.target
[Service]
PermissionsStartOnly=true
ExecStartPre=/bin/mkdir -p /run/shadowsocks
ExecStartPre=/bin/chown nobody:nobody /run/shadowsocks
ExecStart=/usr/bin/ssserver -c /etc/shadowsocks/ss.json #之前的配置地址
Restart=on-abort
User=nobody
Group=nobody
UMask=0027
[Install]
WantedBy=multi-user.target

运行服务并设置开机自启：
systemctl start ss
systemctl enable ss
```

4、注意
防火墙需要开启端口号9000，修改过后重启防火墙才能生效
systemctl start firewalld.service（开启防火墙）
systemctl stop firewalld.service（停用防火墙）
service firewalld restart（重启防火墙）
firewall-cmd --zone=public --add-port=9000/udp --permanen(指定端口范围为9000通过防火墙)
firewall-cmd --zone=public --add-port=9000/tcp --permanen(指定端口范围为9000通过防火墙)
firewall-cmd --reload

window使用shadowsocks
1、安装shadowsocks，地址在github上搜sadowsocks-window
2、配置一下服务器地址，服务器端口，密码以及加密方式（与服务器对应）
3、启动系统代理，PAC模式和全局模式都可以，PAC模式一般是被代理被墙了的

// https://kiwivm.64clouds.com/main-exec.php?mode=extras_shadowsocks
***

======================================================
### mysql 

  安装
  ```
	sudo apt-get install mysql-server
	sudo apt isntall mysql-client
	sudo apt install libmysqlclient-dev
  ```
  启动service mysql start

  关闭service mysql stop

  重启service mysql restart

  mysql -uroot -p syqroot

  现在设置mysql允许远程访问，首先编辑文件/etc/mysql/mysql.conf.d/mysqld.cnf：
	sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
	注释掉bind-address = 127.0.0.1：
***

======================================================
### 在 Ubuntu 系统安装 Redis 可以使用以下命令:

$sudo apt-get update
$sudo apt-get install redis-server
启动 Redis
$ redis-server
查看 redis 是否启动？
$ redis-cli
以上命令将打开以下终端：

redis 127.0.0.1:6379>
127.0.0.1 是本机 IP ，6379 是 redis 服务端口。现在我们输入 PING 命令。


flushall ——> 清空整个 Redis 服务器的数据(删除所有数据库的所有 key )

flushdb ——> 清空当前数据库中的所有 key

redis 127.0.0.1:6379> ping
PONG
以上说明我们已经成功安装了redis。

如果是用apt-get或者yum install安装的redis，可以直接通过下面的命令停止/启动/重启redis

/etc/init.d/redis-server stop
/etc/init.d/redis-server start
/etc/init.d/redis-server restart
如果是通过源码安装的redis，则可以通过redis的客户端程序redis-cli的shutdown命令来重启redis

redis-cli -h 127.0.0.1 -p 6379 shutdown
如果上述方式都没有成功停止redis，则可以使用终极武器 kill -9

/usr/local/redis/bin/redis-cli 

***

=====================================================
### tomcat
查看输出logs
tail -f catalina.out
查看tomcat进程
ps -ef | grep tomcat

***

==================================================
腾讯云服务器
+----------------------------------------------------------------------
| YJCOM [ EASY CLOUD EASY WEBSITE]" >> $README
+----------------------------------------------------------------------
| Copyright (c) 2015 http://yjcom.com All rights reserved.
+----------------------------------------------------------------------

nginx 		/usr/local/nginx
tomcat6		/var/tomcat/tomcat-6
tomcat7		/var/tomcat/tomcat-7
tomcat8		/var/tomcat/tomcat-8
mysql5.6	/var/lib/mysql

./tomcat.sh stop|start

mysql:		service mysql (start|stop|restart)
vsftpd:		service vsftpfd (start|stop|restart)
nginx:		service nginx (start|stop|restart)

www ftp directory	/yjdata/www/www/

change tomcat version for the default site
/yjdata/www/www/change_tomcat_version.sh 6|7|8

change jdk version for the default site
/yjdata/www/www/change_jdk_version.sh 1.6|1.7|1.8

======================================================================
***
netstat -ntlp //查看当前所有tcp端口·

netstat -ntulp |grep 80 //查看所有80端口使用情况·

netstat -an | grep 3306 //查看所有3306端口使用情况·

### sftp
登录
```
sftp -P [port] [user]@[ip]
```
get 取得远程服务器上的指定文件

put 上传本地指定的文件到远程服务器上

示例:

get -r ./* /Users/voidcc.com/本地项目目录/

从远程下载所有文件及文件夹到本地项目目录

 