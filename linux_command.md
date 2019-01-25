[TOC]

### 1、用户和用户组

```shell
#查看当前登录用户的组内成员
groups 
#查看mysql用户所在的组,以及组内成员
groups mysql
#查看当前登录用户名
whoami 
```

```shell
#文件包含的所有组
cat /etc/group
cat /etc/gshadow
#系统存在的所有用户名
cat /etc/shadow
cat /etc/passwd
```

###### 1.1 与用户（user）和用户组（group）相关的配置文件； 

```
1）与用户（user）相关的配置文件；
/etc/passwd 注：用户（user）的配置文件；
/etc/shadow 注：用户（user）影子口令文件；
2）与用户组（group）相关的配置文件；
/etc/group 注：用户组（group）配置文件；
/etc/gshadow 注：用户组（group）的影子文件；
```

###### 1.2 管理用户（user）和用户组（group）的相关工具或命令； 

```shell
#1）管理用户（user）的工具或命令；
增加用户：useradd mysql
为用户增加密码：passwd mysql
#添加用户mysql 到用户组mysql
useradd -g mysql mysql
删除用户：userdel username
#2）管理用户组（group）的工具或命令；
新建工作组：groupadd mysql_group
将用户添加进工作组：usermod -G mysql_group mysql
                  usermod -a -G groupA mysql
删除用户组: groupdel mysql_group
查看用户所属的组使用命令：$ groups user
```

### 2、权限

######2.1 文件权限

```shell
drwxrwxrwx  2 root root  4096 Jan 25 10:07 bin
-rwxrwxrwx  1 root root 17987 Jan 25 10:08 COPYING
```

如图所示，一共是10位数字，除去第一位，剩下的9位数字从左到右开始，每三个字母代表一类。这样看来一共是三个组，而此时这里的三类对应到上面的用户组： 

```shell
除去第一位的字母：
    前三位代表的是：文件所拥有者对此文件的权限
    中间三位代表的是：当前用户所属的组对此文件的权限
    后三位代表的是：其他用户组对此文件的权限
而第一位代表的是文件的类型：
    d  目录文件。
    l  符号链接(指向另一个文件,类似于瘟下的快捷方式)。
    s  套接字文件。
    b  块设备文件,二进制文件。
    c  字符设备文件。
    p  命名管道文件。
```

```shell
r(Read，读取)：对文件而言，具有读取文件内容的权限；对目录来说，具有浏览目录的权限。
w(Write,写入)：对文件而言，具有新增,修改,删除文件内容的权限；对目录来说，具有新建，删除，修改，移动目录内文件的权限。
x(Execute，执行)：对文件而言，具有执行文件的权限；对目录了来说该用户具有进入目录的权限。
```

```shell
每个字母对应着数字
r,w,x --------------- 2^2,2^1,2^0
r:4
w:2
x:1
```

###### 2.2修改文件权限

```
1.修改权限方法一：
chmod 755 abc
其实就是在给abc赋予权限：rwx r-x r-x
rwx =7 ，r-x=5，r-x=5
就是样的一个对应关系

2.方法二：
u：用户权限
g：组权限
o：不同组其他用户权限
r，w，x上面已经介绍过了，再次不多解释。
+：加入
-：除去
=：设置
chmod u+x abc就是给abc的文件所有者可以执行的权限
```

2.3 改变文件属主和用户组

```shell
chown -R 所有者:所在的组 文件路径
chown -R mysql:mysql ./
```

