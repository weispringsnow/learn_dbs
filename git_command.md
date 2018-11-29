[TOC]
### git命令
####1、init
`git init`命令创建一个空的Git仓库或重新初始化一个现有仓库。 
####2、add
`git add`命令将文件内容添加到索引(将修改添加到暂存区)。也就是将要提交的文件的信息添加到索引库中。 

```
用法： git add <path>
```
####3、commit

`git commit`命令将索引的当前内容与描述更改的用户和日志消息一起存储在新的提交中。 

```
用法： git commit -m "the commit message" 
```

#### 4、remote

`git remote`命令管理一组跟踪的存储库。 

```
用法：
 1.查看当前的远程库
 	git remote -v  列出详细信息，在每一个名字后面列出其远程url
 2.添加一个新的远程仓库
 	git remote add origin https://github.com/weispringsnow/learn_dbs.git
 	git remote add staging https://github.com/weispringsnow/learn_dbs.git
```

#### 5、fetch

`git fetch`命令用于从另一个存储库下载对象和引用。 

```
用法：
 1.更新远程跟踪分支
 	git fetch origin
    git fetch staging
   上述命令从远程refs/heads/命名空间复制所有分支，并将它们存储到本地的refs/remotes/    origin/命名空间中，除非使用分支.<name>.fetch选项来指定非默认的refspec。
 2.将某个远程主机的更新 
 	git fetch https://github.com/weispringsnow/learn_dbs.git master
 	git fetch origin master
```

#### 6、checkout

`git checkout`命令用于切换分支或恢复工作树文件。`git checkout`是git最常用的命令之一，同时也是一个很危险的命令，因为这条命令会重写工作区。 

```
用法：
 1.切换分支
 	git checkout master  #//取出master版本的head。
 2. 从另一个提交中取出文件
    git checkout master_dev Makefile
 3.从索引中恢复file_name 放弃当前对文件file_name的修改
    git checkout file_name
 4.从远程dev/1.5.4分支取得到本地分支/dev/1.5.4
    git checkout -b dev/1.5.4 origin/dev/1.5.4
 5.取文件file_name的 在commit_id是的版本
    git checkout commit_id file_name  
 6.这条命令把hello.rb从HEAD中签出.
    git checkout -- hello.rb
 7.这条命令把 当前目录所有修改的文件从HEAD中签出并且把它恢复成未修改时的样子.
     git checkout .
     #注意：在使用 git checkout 时，如果其对应的文件被修改过，那么该修改会被覆盖掉
 8.假设你现在基于远程分支”origin“，创建一个叫”mywork“的分支。
     git checkout -b mywork origin
```

#### 7、pull

`git pull`命令用于从另一个存储库或本地分支获取并集成(整合)。`git pull`命令的作用是：取回远程主机某个分支的更新，再与本地的指定分支合并，它的完整格式稍稍有点复杂。

```
用法：
 1.要取回origin主机的next分支，与本地的master分支合并
  git pull origin next:master #与本地的master分支合并
  git pull origin next        #与当前分支合并 
  	相等于git fetch origin + git merge origin/next
```

#### 8、clone

`git clone`命令将存储库克隆到新目录中。 

```
用法：
 git clone <版本库的网址> <本地目录名>
 git remote add origin https://github.com/weispringsnow/learn_dbs.git
```

#### 9、**git fetch和git pull的区别**
+ *git fetch*：相当于是从远程获取最新版本到本地，不会自动合并。
  

#### 10、merge

`git merge`命令用于将两个或两个以上的开发历史加入(合并)一起。 

````
1.合并分支fixes和enhancements在当前分支的顶部，使它们合并：
  git merge fixes enhancements
2.合并obsolete分支到当前分支，使用ours合并策略：
  git merge -s ours obsolete
3.将分支maint合并到当前分支中，但不要自动进行新的提交：
  git merge --no-commit maint
4.将分支dev合并到当前分支中，自动进行新的提交：
  git merge dev
````

#### 11、rebase

`git rebase`命令在另一个分支基础之上重新应用，用于把一个分支的修改合并到当前分支。

```
git rebase origin 
git rebase --continue
git rebase --abort
```

#### 12、branch

`git branch`命令用于列出，创建或删除分支。 

```
1. 查看当前有哪些分支、查看本地和远程分支
   git branch
   git branch -a
   git branch -r
2. 新建一个分支、切换到指定分支
   git branch dev2
   git checkout dev2
3. 将更改添加到新建分支上
   git status
   git add git_command.md


4. 查看当前有哪些分支
5. 查看当前有哪些分支
6. 查看当前有哪些分支
7. 查看当前有哪些分支
8. 查看当前有哪些分支

```

