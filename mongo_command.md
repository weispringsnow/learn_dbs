windows下：
命令行下运行 MongoDB 服务器
mongod --dbpath D:\mongodb\data
安装 MongoDB服务
mongod --config "D:\mongodb\mongod.cfg" --install
 --serviceName 和 --serviceDisplayName
启动MongoDB服务 
net start MongoDB
关闭MongoDB服务
net stop MongoDB
移除 MongoDB 服务
mongod --remove


db 命令用于查看当前操作的文档（数据库）

linux:
tar -zxvf mongodb-linux-x86_64-rhel70-2.6.6.tgz  
mv  mongodb-linux-x86_64-rhel70-2.6.6 /usr/local/mongodb       # 将解压包拷贝到指定目录
vi /etc/profile
PATH=$PATH:/usr/local/mongodb/bin
export PATH
创建数据库目录
mkdir -p /data/db
命令行中运行 MongoDB 服务
mongod或mongod --dbpath /data/db
db.runoob.insert({x:10})
db.runoob.find()
命令可以显示所有数据的列表
show dbs
db
use local
数据库也通过名字来标识。数据库名可以是满足以下条件的任意UTF-8字符串。
不能是空字符串（"")。
不得含有' '（空格)、.、$、/、\和\0 (空字符)。
应全部小写。
最多64字节。

