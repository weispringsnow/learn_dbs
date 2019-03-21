[TOC]

### 一、常用设置

######1、设置自动导包 

```xml
1. Settings→Editor→General→Auto Import
2. 选中Optimize imports on the fly和Add unambiguous imports on the fly
Optimize imports on the fly：自动去掉一些没有用到的包
Add unambiguous imports on the fly：自动帮我们优化导入的包
```

######2、修改主题和主编辑区字体大小

```
Files -> Settings Appearance Theme:Darcular Windows Intellij
                  Editor  Font Color 
```

###### 3、不知道的快捷键可以去查看idea的live templates,

```
具体：file->settings->editor->live templates 里面预定义了很多模板，sout就在output下面
```

###### 4、输入System.out.println()的快捷方法

```
输入 sout，然后按 tab 键，就可以快速生成 System.out.println();
```

###### 5、IntelliJ IDEA创建main函数快捷方法

```
在编写代码的时候直接输入psv就会看到一个psvm的提示，此时点击tab键一个main方法就写好了。
依次还有在方法体内键入for会有一个fori的提示，选中然后tab键，就会自动创建一个for循环。
更多的提示可以CTRL + j 可以查看，mac系统下是command＋j
```

######6、一键格式化代碼： **Ctrl+Alt+L**

######7、**ctrl+shift+R==搜索类   CTRL+N：按照类名搜索类**

###### 8、**强大的搜索功能，shift+shift (无论您想要搜啥都能找到)**

9、显示类中所有方法

View——Tool Windows——Structure  Alt + 7

### 二、导入maven项目

```
初始化1.import project -> 2.选择maven项目 -> 3.选择第二个external moudle,选择maven -> 4.next
4.1 Import Maven projects automatically 勾选 Automatically download 勾选 Sources Documentation
->environment setting -> 6.勾选快照 -7 改java环境变量
```

 ### 三、配置tomcat

```
配置Configurations 
菜单栏【run】-【Edit Configurations】或 右上角有个向下的小箭头 
或者File—>Setting—>Build,Execution,Deployment—->Application Servers—>”+”这里添加了之后Edit Configuration里面就可以看到Tomcat Server了 
```

### 四、侧边栏不见了,pom不起作用

```
view -> Tool Windows
最后发现在在setting-> Build Tools -> maven ->Ignored files 有一个pom文件被勾选，我也不知道是什么时候勾选，反正是勾选上了，去掉勾选就可以了；
```

### 五、Intellij导入子项目时，maven列表子项目灰色不可用---解决方法

```
第一步 
找到父项目，点击右键，选择Open Module Settings
第二步 
打开设置，点击绿色的+ 
第三步 
点击import module,找到显示为灰色的module模块，并导入，然后next,next,next… 
然后你就会发现，卧槽，竟然好了！！！ 
```

### 六、IDEA 中按住Alt+Enter根据提将代码改成lambda表达式

### 七、 Compilation failed: internal java compiler error

```
解决办法很简单：File-->Setting...-->Build,Execution,Deployment-->Compiler-->Java Compiler 设置相应Module的target bytecode version的合适版本（跟你jkd版本一致），这里我改成1.8版本的。
```

### 八、idea中鼠标放到类或方法上自动显示文档

```
setting - General - show quick documentation on mouse move
```

### 九、解决intellij idea控制台中文乱码(亲测有用)

```
第一步:修改intellij idea配置文件：
找到intellij idea安装目录，bin文件夹下面idea64.exe.vmoptions和idea.exe.vmoptions这两个文件，分别在这两个文件中添加：-Dfile.encoding=UTF-8
第二步：找到intellij idea的file---settings---Editor---FileEncodings的GlobalEncoding和ProjectEncoding和Default encoding for properties都配置成UTF-8
第三步：在部署Tomcat的VM options项中添加：-Dfile.encoding=UTF-8
第四步：重启Intellij idea即可解决乱码问题（一定要关闭idea重新打开）
```

