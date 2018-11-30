[TOC]

#### һ����װ��ʽ

######windows�£�

```shell
������������ MongoDB ������
  mongod --dbpath D:\mongodb\data
��װ MongoDB����
  mongod --config "D:\mongodb\mongod.cfg" --instal  
    ��Ҫʱ�� --serviceName --serviceDisplayName
����MongoDB���� 
  net start MongoDB
�ر�MongoDB����
  net stop MongoDB
�Ƴ� MongoDB ����
  mongod --remove
db �������ڲ鿴��ǰ�������ĵ������ݿ⣩
```
D:\mongodb\mongod.cfg
```yaml
systemLog:
    destination: file
    path: c:\data\log\mongod.log
storage:
    dbPath: c:\data\db
security:
    authorization: disabled/enabled #����Ȩ����֤
```

###### linux��:

```shell
tar -zxvf mongodb-linux-x86_64-rhel70-2.6.6.tgz  #��ѹ
mv mongodb-linux-x86_64-rhel70-2.6.6 /usr/local/mongodb   #������ָ��Ŀ¼
vi /etc/profile #��������
  PATH=$PATH:/usr/local/mongodb/bin
  export PATH
#�������ݿ�Ŀ¼
mkdir -p /data/db
#������������ MongoDB ����
mongod��mongod --dbpath /data/db
 db.runoob.insert({x:10})
 db.runoob.find()
#���������ʾ�������ݵ��б�
 show dbs
 db
 use local
#���ݿ���������������������������UTF-8�ַ�����
�����ǿ��ַ�����"")��
���ú���' '���ո�)��.��$��/��\��\0 (���ַ�)��
Ӧȫ��Сд��
���64�ֽڡ�
```
####�����û�Ȩ�޿���

###### 	����Ȩ����֤��

windows��
```yaml
security:
    authorization: disabled/enabled #����Ȩ����֤
```

linux��

```shell
mongod --auth
```

#### ����û��ͽ�ɫ


```shell
use admin
db.createUser(
  {
    user: "myUserAdmin",
    pwd: "abc123",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
#���
show users
db.system.users.find()
```

#### ��֤Ȩ���Ƿ���Ч

```shell
use admin
db.auth('myUserAdmin', 'abc123')
show dbs
```

#### �����ͨ�û�

```
1��һ��������֤���û�����Ա������ʹ��db.createUser()ȥ����������û��� 
����Է���mongodb���õĽ�ɫ���û��Զ���Ľ�ɫ���û���
2�����myUserAdmin�û�����ֻ����Ȩȥ�����û��ͽ�ɫ��myUserAdmin���������ͼִ�������κβ�����������test���ݿ��е�foo������ȥ�����ݣ�mongodb�����ش���
3��ע�⣺
�㴴���û������ݿ⣨�������test���ݿ⣩�Ǹ��û���֤���ݿ⡣�����û���֤��������ݿ⣬�û���Ȼ�������������ݿ�Ľ�ɫ�����û���֤���ݿⲻ�����û�Ȩ�ޡ�
```

###### ������ͨ�û��� 

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

#### ���������û�root

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

#### MongoDB���ݿ��ɫ

**�ڽ��Ľ�ɫ** 
  **���ݿ��û���ɫ��**read��readWrite; 
  **���ݿ�����ɫ��**dbAdmin��dbOwner��userAdmin�� 
  **��Ⱥ�����ɫ��**clusterAdmin��clusterManager��clusterMonitor��hostManager�� 
  **���ݻָ���ɫ��**backup��restore�� 
  **�������ݿ��ɫ��**readAnyDatabase��readWriteAnyDatabase��userAdminAnyDatabase��dbAdminAnyDatabase 
  **�����û���ɫ��**root // ���ﻹ�м�����ɫ��ӻ�ֱ���ṩ��ϵͳ�����û��ķ��ʣ�dbOwner ��userAdmin��userAdminAnyDatabase�� 
  **�ڲ���ɫ��**__system 
**��ɫ˵����** 
  **Read��**�����û���ȡָ�����ݿ� 
  **readWrite��**�����û���дָ�����ݿ� 
  **dbAdmin��**�����û���ָ�����ݿ���ִ�й�������������������ɾ�����鿴ͳ�ƻ����    system.profile 
  **userAdmin��**�����û���system.users����д�룬������ָ�����ݿ��ﴴ����ɾ���͹����û� 
  **clusterAdmin��**ֻ��admin���ݿ��п��ã������û����з�Ƭ�͸��Ƽ���غ����Ĺ���Ȩ�ޡ� 
  **readAnyDatabase��**ֻ��admin���ݿ��п��ã������û��������ݿ�Ķ�Ȩ�� 
  **readWriteAnyDatabase��**ֻ��admin���ݿ��п��ã������û��������ݿ�Ķ�дȨ�� 
  **userAdminAnyDatabase��**ֻ��admin���ݿ��п��ã������û��������ݿ��userAdminȨ�� 
  **dbAdminAnyDatabase��**ֻ��admin���ݿ��п��ã������û��������ݿ��dbAdminȨ�ޡ� 
  **root��**ֻ��admin���ݿ��п��á������˺ţ�����Ȩ��





