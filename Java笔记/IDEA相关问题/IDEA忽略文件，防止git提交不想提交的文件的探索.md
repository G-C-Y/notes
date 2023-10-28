使用IDEA开发有 一段时间了，从陌生到熟悉的过程算是很平稳的度过，感谢导师与同事对我提供的帮助。这篇文章是探索git忽略文件提交的一些方面的研究，分为2个部分，内容如下
1.在项目中隐藏掉你不想看到的文件夹或者文件，
2.使用.ignore插件在IDEA中忽略你要提交的文件。

一个标准的IDEA项目，以maven项目为例子：
```java
+ project
  |
  + pom.xml
  |
  + src /
     + main /
     | + java    java源代码文件,最终会打包编译到WEB/INF下的classes目录
     | + resources 资源库，会自动复制到classes目录里
     | + filters  资源过滤文件
     | + webapp web应用程序资源文件
     + test /
     | + java  测试java源文件内容
     | + resources 测试的资源文件
     | + filters  测试的资源过滤文件
     + it /
     + assembly /
     + site / |
  + .idea /
  +  project.iml
+ LICENSE.txt   工程许可说明
+ NOTICE.txt   项目所需要的依赖的说明文件
+ README.txt 项目工程说明文档
```
多出.idea目录和project.iml（名称是和你项目名称一致的），这个是IDEA工具自己生成的，但是我们不想看到，也不会把该文件提交到我们版本控制仓库中。
方式一、在项目中隐藏掉你不想看到的文件夹或者文件
进入IDE Settings section, go to File Types如图：
![](https://images.cherryfloris.eu.org/2021/1632377429133-cc821180-0728-4421-af53-2dd9be502725.png)
看红色方框的内容，此时project中已经已经看不到这个idea文件夹和*.iml文件了。

ps：有的时候maven项目编译后会看到target目录，但是我们也不需要看到他的时候，按如下操作隐藏掉它：
1.Mark Directory As   -> Excluded,此时target目录下的所有内容会变成红色。
![](https://images.cherryfloris.eu.org/2021/1632377465197-a5dd0843-dc37-4a66-874a-875a6f359912.png)
2.点击红框标记的1处，取消Show Excluded Files文件，此时的target就会从项目中隐藏掉了。
![](https://images.cherryfloris.eu.org/2021/1632377480349-49a43738-dc1c-41dc-a979-af50e7476399.png)
**方式二、使用.ignore插件在IDEA中忽略你要提交的文件**

有的时间创建的文件，不想被提交到版本控制的的选项中。在IDEA中安装.ignore插件。创建好了之后：

1.添加.gitignore
![](https://images.cherryfloris.eu.org/2021/1632377497747-fa126c15-a06b-4651-a613-84c5e3cc94b0.png)
![](https://images.cherryfloris.eu.org/2021/1632377506715-7b8c0b71-7950-43fa-9024-54547cc725fc.png)
 2.将不需要提交到版本控制add ignore中
例如你创建了一个MyTest文件，首先不要git add，使用工具：
![](https://images.cherryfloris.eu.org/2021/1632377538426-0ec87af9-47f4-4f27-8856-03e23cfcbbc5.png)
此时刚被你选中的被忽略的文件名变成了灰色，此时该文件你想git add也add不进去，当然也就不能提交了。
ps：万一你不小心git add file(add File文件了，哪怕文件置灰，也是能提交的)了，怎么办，不用急
使用git 命令如下：
git rm --cached file_path
git commit -m '移除测试文件'
删除本地缓存，但是不删除文件。测试的文件在处于置灰状态就不能提交了！
插件下载地址：[https://plugins.jetbrains.com/plugin/7495--ignore](https://plugins.jetbrains.com/plugin/7495--ignore)
转载：[http://blog.csdn.net/qq_34590097/article/details/56284935](http://blog.csdn.net/qq_34590097/article/details/56284935)
方式三：IDEA的changelist方式
![image.png](https://images.cherryfloris.eu.org/2021/1632377581434-762e1058-42c6-4964-88c5-ebe24f15f968.png)
步骤1：创建changelist
步骤2：将不想提交的文件移动到你所创建的changelist里面，如下图所示：
![image.png](https://images.cherryfloris.eu.org/2021/1632377612008-07641515-d040-4059-ade3-a8609737e35b.png)
备注：方式三在IDEA2020中找不到，官网说2020.1版本以后这个标签页默认在git commit时才会看到。解决方案如下图所示：
**取消掉User non-modal commit interface即可！**
![image.png](https://images.cherryfloris.eu.org/2021/1632377631065-7a68a12c-22df-4807-88bd-b357631a3616.png)
![image.png](https://images.cherryfloris.eu.org/2021/1632377640366-0f2beac2-5e0a-40d8-bd2b-61ff1a42cd91.png)

# [Git忽略规则(.gitignore配置）不生效原因和解决](https://www.cnblogs.com/rainbowk/p/10932322.html)
[https://www.cnblogs.com/rainbowk/p/10932322.html](https://www.cnblogs.com/rainbowk/p/10932322.html)
