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
cd /usr/local/mysql/<br>mkdir ./data/mysql
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
./mysql/bin/mysql -uroot
 
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
#解决1:更改 ‘mysql’数据库‘user’表‘host’项，从‘localhost’改成‘%’。
use mysql;
select 'host' from user where user='root'; 
update user set host = '%' where user ='root';
flush privileges; 
#解决2：直接授权
GRANT ALL PRIVILEGES ON *.* TO ‘root’@'%’ IDENTIFIED BY ‘youpassword’ WITH GRANT OPTION;
```

###### 5.2 安装时的一些错误 

```shell
#-bash: ./scripts/mysql_install_db: /usr/bin/perl: bad interpreter: 没有那个文件或目录
#解决： 
yum -y install perl perl-devel
#Installing MySQL system tables..../bin/mysqld: error while loading shared libraries: libaio.so.1: cannot open shared object file: No such file or directory
#解决：
yum -y install libaio-devel
```

### 6、其他

###### #6.1 配置环境变量

```shell
vi /etc/profile
export PATH=....:/usr/local/mysql/bin
```

