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
adduser&&useradd 注：添加用户
passwd 注：为用户设置密码
usermod 注：修改用户命令，可以通过usermod 来修改登录名、用户的家目录等等；
pwcov 注：同步用户从/etc/passwd 到/etc/shadow
pwck 注：pwck是校验用户配置文件/etc/passwd 和/etc/shadow 文件内容是否合法或完整；
pwunconv 注：是pwcov 的立逆向操作，是从/etc/shadow和 /etc/passwd 创建/etc/passwd ，然后会删除 /etc/shadow 文件；
finger 注：查看用户信息工具 id 注：查看用户的UID、GID及所归属的用户组 chfn 注：更改用户信息工具
su 注：用户切换工具 sudo 注：sudo 是通过另一个用户来执行命令（execute a command as another user），su 是用来切换用户，然后通过切换到的用户来完成相应的任务，
但sudo 能后面直接执行命令，比如sudo 不需要root 密码就可以执行root 赋与的执行只有root才能执行相应的命令；但得通过visudo 来编辑/etc/sudoers来实现；
visudo 注：visodo 是编辑 /etc/sudoers 的命令；也可以不用这个命令，直接用vi 来编辑 /etc/sudoers 的效果是一样的；
sudoedit 注：和sudo 功能差不多；
#2）管理用户组（group）的工具或命令；
groupadd 注：添加用户组；
groupdel 注：删除用户组；
groupmod 注：修改用户组信息
groups 注：显示用户所属的用户组
grpck grpconv 注：通过/etc/group和/etc/gshadow 的文件内容来同步或创建/etc/gshadow ，如果/etc/gshadow 不存在则创建；
grpunconv 注：通过/etc/group 和/etc/gshadow 文件内容来同步或创建/etc/group ，然后删除gshadow文件；
```

### 2、权限

```shell

```

