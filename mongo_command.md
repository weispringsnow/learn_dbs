[TOC]

#### 一、安装方式

######windows下：

```shell
命令行下运行 MongoDB 服务器
  mongod --dbpath D:\mongodb\data
安装 MongoDB服务
  mongod --config "D:\mongodb\mongod.cfg" --instal  
    需要时加 --serviceName --serviceDisplayName
启动MongoDB服务 
  net start MongoDB
关闭MongoDB服务
  net stop MongoDB
移除 MongoDB 服务
  mongod --remove
db 命令用于查看当前操作的文档（数据库）
```
D:\mongodb\mongod.cfg
```yaml
systemLog:
    destination: file
    path: c:\data\log\mongod.log
storage:
    dbPath: c:\data\db
security:
    authorization: disabled/enabled #开启权限验证
```

###### linux下:

```shell
tar -zxvf mongodb-linux-x86_64-rhel70-2.6.6.tgz  #解压
mv mongodb-linux-x86_64-rhel70-2.6.6 /usr/local/mongodb   #拷贝到指定目录
vi /etc/profile #环境变量
  PATH=$PATH:/usr/local/mongodb/bin
  export PATH
#创建数据库目录
mkdir -p /data/db
#命令行中运行 MongoDB 服务
mongod或mongod --dbpath /data/db
 db.runoob.insert({x:10})
 db.runoob.find()
#命令可以显示所有数据的列表
 show dbs
 db
 use local
#数据库名可以是满足以下条件的任意UTF-8字符串。
不能是空字符串（"")。
不得含有' '（空格)、.、$、/、\和\0 (空字符)。
应全部小写。
最多64字节。
```
####二、用户权限控制

###### 	开启权限验证：

windows下
```yaml
security:
    authorization: disabled/enabled #开启权限验证
```

linux下

```shell
mongod --auth
```

#### 添加用户和角色


```shell
use admin
db.createUser(
  {
    user: "myUserAdmin",
    pwd: "abc123",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
#结果
show users
db.system.users.find()
```

#### 验证权限是否生效

```shell
use admin
db.auth('myUserAdmin', 'abc123')
show dbs
```

#### 添加普通用户

```
1、一旦经过认证的用户管理员，可以使用db.createUser()去创建额外的用户。 
你可以分配mongodb内置的角色或用户自定义的角色给用户。
2、这个myUserAdmin用户仅仅只有特权去管理用户和角色，myUserAdmin，如果你试图执行其他任何操作，例如在test数据库中的foo集合中去读数据，mongodb将返回错误。
3、注意：
你创建用户的数据库（这里就是test数据库）是该用户认证数据库。尽管用户认证是这个数据库，用户依然可以有其他数据库的角色。即用户认证数据库不限制用户权限。
```

###### 创建普通用户： 

```shell
use test
db.createUser(
    {
    user:"test1",
    pwd: "test1",
    roles: [{ role: "readWrite", db: "test"}]
    }
  )
```

#### 创建超极用户root

```shell
use admin
db.createUser(
  {
    user: "root",
    pwd: "root",
    roles: [ { role: "root", db: "admin" } ]
  }
);
```

#### MongoDB数据库角色

**内建的角色** 
  **数据库用户角色：**read、readWrite; 
  **数据库管理角色：**dbAdmin、dbOwner、userAdmin； 
  **集群管理角色：**clusterAdmin、clusterManager、clusterMonitor、hostManager； 
  **备份恢复角色：**backup、restore； 
  **所有数据库角色：**readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、dbAdminAnyDatabase 
  **超级用户角色：**root // 这里还有几个角色间接或直接提供了系统超级用户的访问（dbOwner 、userAdmin、userAdminAnyDatabase） 
  **内部角色：**__system 
**角色说明：** 
  **Read：**允许用户读取指定数据库 
  **readWrite：**允许用户读写指定数据库 
  **dbAdmin：**允许用户在指定数据库中执行管理函数，如索引创建、删除，查看统计或访问    system.profile 
  **userAdmin：**允许用户向system.users集合写入，可以找指定数据库里创建、删除和管理用户 
  **clusterAdmin：**只在admin数据库中可用，赋予用户所有分片和复制集相关函数的管理权限。 
  **readAnyDatabase：**只在admin数据库中可用，赋予用户所有数据库的读权限 
  **readWriteAnyDatabase：**只在admin数据库中可用，赋予用户所有数据库的读写权限 
  **userAdminAnyDatabase：**只在admin数据库中可用，赋予用户所有数据库的userAdmin权限 
  **dbAdminAnyDatabase：**只在admin数据库中可用，赋予用户所有数据库的dbAdmin权限。 
  **root：**只在admin数据库中可用。超级账号，超级权限





