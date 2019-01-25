[TOC]

### 1、下载

```shell
#下载地址：http://dev.mysql.com/downloads/mysql/5.6.html#downloads
#下载版本：我这里选择的5.6.33，通用版，linux下64位
#也可以直接复制64位的下载地址，通过命令下载：
wget http://dev.mysql.com/get/Downloads/MySQL-5.6/mysql-5.6.33-linux-glibc2.5-x86_64.tar.gz
```

### 2、解压

```shell
#解压
tar -zxvf mysql-5.6.33-linux-glibc2.5-x86_64.tar.gz
#复制解压后的mysql目录
cp -r mysql-5.6.33-linux-glibc2.5-x86_64 /usr/local/mysql
```

### 3、添加用户组和用户

```shell
#添加用户组
groupadd mysql
#添加用户mysql 到用户组mysql
useradd -g mysql mysql
```

### 4、安装

```shell
cd /usr/local/mysql/
mkdir ./data/mysql
chown -R mysql:mysql ./
./scripts/mysql_install_db --user=mysql --datadir=/usr/local/mysql/data/mysql
cp support-files/mysql.server /etc/init.d/mysqld
chmod 755 /etc/init.d/mysqld
cp support-files/my-default.cnf /etc/my.cnf
#修改启动脚本
vi /etc/init.d/mysqld
#修改项：
basedir=/usr/local/mysql/
datadir=/usr/local/mysql/data/mysql
 
#启动服务
service mysqld start
#测试连接
/usr/local/mysql/bin/mysql -u root
/usr/local/mysql/bin/mysql -u root -p
#加入环境变量，编辑 /etc/profile，这样可以在任何地方用mysql命令了
export PATH=$PATH:/usr/local/mysql//bin<br>source /etc/profile
 
#启动mysql
service mysqld start
#关闭mysql
service mysqld stop
#查看运行状态
service mysqld status
```

### 5、错误

######5.1 sqlyog连接时，报1130错误

```SHELL
#是由于没有给远程连接的用户权限问题
#解决：直接授权
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;
```

###### 5.2 安装时的一些错误 

```shell
#-bash: ./scripts/mysql_install_db: /usr/bin/perl: bad interpreter: 没有那个文件或目录
#解决： 
yum -y install perl perl-devel
#Installing MySQL system tables..../bin/mysqld: error while loading shared libraries: libaio.so.1: cannot open shared object file: No such file or directory
#解决：
yum -y install libaio-devel
#FATAL ERROR: please install the following Perl modules before executing ./scripts/mysql_install_db:
#解决：
yum -y install autoconf 
```

###### 5.3 MySQL修改root密码的多种方法

```mysql
方法1： 用SET PASSWORD命令
　　mysql -u root
　　mysql> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpass');
方法2：用mysqladmin
　　mysqladmin -u root password "newpass"
　　如果root已经设置过密码，采用如下方法
　　mysqladmin -u root password oldpass "newpass"
方法3： 用UPDATE直接编辑user表
　　mysql -u root
　　mysql> use mysql;
　　mysql> UPDATE user SET Password = PASSWORD('newpass') WHERE user = 'root';
　　mysql> FLUSH PRIVILEGES;
在丢失root密码的时候，可以这样
　　mysqld_safe --skip-grant-tables&
　　mysql -u root mysql
　　mysql> UPDATE user SET password=PASSWORD("new password") WHERE user='root';
　　mysql> FLUSH PRIVILEGES;
```



### 6、其他

###### #6.1 配置环境变量

```shell
vi /etc/profile
export PATH=....:/usr/local/mysql/bin
```

### 7、权限

```mysql
CREATE USER username IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' IDENTIFIED BY 'password';
REVOKE ALL PRIVILEGES ON *.* FROM 'username'@'localhost';
GRANT ALL PRIVILEGES ON wordpress.* TO 'username'@'localhost' IDENTIFIED BY 'password';
GRANT SELECT, UPDATE ON wordpress.* TO 'username'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
DROP USER username@localhost;
SELECT User, Host FROM user;
```

```mysql
WITH GRANT OPTION 这个选项表示该用户可以将自己拥有的权限授权给别人
```

### 8、**MySQL用户及权限管理** 

```myssql
MySQL服务器通过MySQL权限表来控制用户对数据库的访问，MySQL权限表存放在mysql数据库里，由mysql_install_db脚本初始化。这些MySQL权限表分别user，db，table_priv，columns_priv和host。下面分别介绍一下这些表的结构和内容：
user权限表：记录允许连接到服务器的用户帐号信息，里面的权限是全局级的。
db权限表：记录各个帐号在各个数据库上的操作权限。
table_priv权限表：记录数据表级的操作权限。
columns_priv权限表：记录数据列级的操作权限。
host权限表：配合db权限表对给定主机上数据库级操作权限作更细致的控制。这个权限表不受GRANT和REVOKE语句的影响。
```

```mysql
grant all on prod.* to 'tom'@'%' identified by 'tom' with grant option;
flush privileges;
select user,host from user where user='tom';
show grants for tom;
```

```mysql
GRANT 语法:
GRANT privileges (columns) ON what TO user IDENTIFIED BY "password" WITH GRANT OPTION
```

```mysql
权限列表：
ALTER: 修改表和索引。
CREATE: 创建数据库和表。
DELETE: 删除表中已有的记录。
DROP: 抛弃(删除)数据库和表。
INDEX: 创建或抛弃索引。
INSERT: 向表中插入新行。
REFERENCE: 未用。
SELECT: 检索表中的记录。
UPDATE: 修改现存表记录。
FILE: 读或写服务器上的文件。
PROCESS: 查看服务器中执行的线程信息或杀死线程。
RELOAD: 重载授权表或清空日志、主机缓存或表缓存。
SHUTDOWN: 关闭服务器。
ALL: 所有权限，ALL PRIVILEGES同义词。
USAGE: 特殊的 "无权限" 权限。
用 户账户包括 "username" 和 "host" 两部分，后者表示该用户被允许从何地接入。tom@'%' 表示任何地址，默认可以省略。还可以是 "tom@192.168.1.%"、"tom@%.abc.com" 等。数据库格式为 db@table，可以是 "test.*" 或 "*.*"，前者表示 test 数据库的所有表，后者表示所有数据库的所有表。
子句 "WITH GRANT OPTION" 表示该用户可以为其他用户分配权限。 
```

```mysql
创建用户:
GRANT insert, update ON testdb.* TO user1@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
CREATE USER user2 IDENTIFIED BY 'password';
分配权限:
GRANT select ON testdb.* TO user2;
查看权限:
SHOW GRANTS FOR user1;
修改密码:
SET PASSWORD FOR user1 = PASSWORD('newpwd');
SET PASSWORD = PASSWORD('newpwd');
移除权限:
REVOKE all ON *.* FROM user1;
删除用户:
DROP USER user1;
数据库列表:
SHOW DATABASES;
数据表列表:
SHOW TABLES;
当前数据库:
SELECT DATABASE();
当前用户:
SELECT USER();
数据表结构:
DESCRIBE table1;
刷新权限:
FLUSH PRIVILEGES;
```

### 9、参考网址

```html
https://www.cnblogs.com/SQL888/p/5748824.html
```

