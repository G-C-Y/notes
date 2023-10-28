# Git生成密钥(ssh)
1.首先用如下命令（如未特别说明，所有命令均默认在Git Bash工具下执行）检查一下用户名和邮箱是否配置（gitlab支持我们用用户名或邮箱登录）：
git config --global  --list
如下，则说明已经配置
![image.png](https://images.cherryfloris.eu.org/2022/1648887436526-38b60485-7f94-4c43-a4d3-75b8eae3ac23.png)
如未配置，则执行以下命令进行配置：
git config --global  user.name "这里换上你的用户名"
git config --global user.email "这里换上你的邮箱"
![image.png](https://images.cherryfloris.eu.org/2022/1648887493872-950a39da-9777-4b5a-a535-3abb74843036.png)
2.执行，~/.ssh检查是否生成ssh文件夹,执行命令后切换到.ssh文件夹下。如果没有则创建.ssh，如图：
![image.png](https://images.cherryfloris.eu.org/2022/1648887513567-e6f98aab-594b-4588-be49-5e2052563d02.png)
3.执行，[ssh](https://so.csdn.net/so/search?q=ssh&spm=1001.2101.3001.7020)-keygen -t rsa -C "这是你的邮箱"
4,接着点击，enter，输入密码
4，接着点击，enter，确认密码
5，如图，则创建成功
![image.png](https://images.cherryfloris.eu.org/2022/1648887552137-52110bfc-28fc-4304-9c82-babcf39567b1.png)
在这里可以看到id_rsa和id_rsa.pub文件已经生成。并且生成的路径也已显示。

6，进入文件夹可以看到

id_rsa文件是私钥，要保存好，放在本地，私钥可以生产公钥，反之不行。
id_rsa.pub文件是公钥，可以用于发送到其他服务器，或者git上
7，用记事本之类的软件打开id_rsa.pub文件，并且复制全部内容。

8，进入gitlab，找到setting,再找到 SSHKeys，将复制的的内容放到 key立即可，Title随便起，如图：
![image.png](https://images.cherryfloris.eu.org/2022/1648887654611-ada0b511-60d5-48f7-9530-1bb4298a087b.png)
9，点击 add key，看到如下图，则[gitlab](https://so.csdn.net/so/search?q=gitlab&spm=1001.2101.3001.7020)添加密钥成功：
![image.png](https://images.cherryfloris.eu.org/2022/1648887679207-f1fac3ea-585b-4dac-9655-a96f93a29408.png)

# Git基础命令
cd /d 切换目录
git clone -b jiuku1.0 [http://git.gzxijiu.com:8022/jiukugroup/jiuku.git](http://git.gzxijiu.com:8022/jiukugroup/jiuku.git)   #直接拉取某一分支代码
git init                              # 初始化本地代码仓
git add .                             # 添加本地代码
git commit -m "add local source"      # 提交本地代码
git pull origin master                # 下载远程代码
git checkout -b cherry           # 新建一个开发分支cherry
git merge master                      # 合并master分支
git push -u origin master             # 上传代码
git  push origin 本地分支名：远程仓库的分支名 ；将项目从本地仓库推送到远程仓库中
git branch //查看本地分支
git branch -D master//删除目标分支
IntelliJ IDEA操作git——合并
将远程orgin/master合并到自己的远程分支orgin/cherry
1.本地切换到master分支
$ git checkout master        若cherry有更新合并一下 git merge
# 获取主干最新代码
$ git pull
2.本地切换到cherry分支
$ git checkout cherry    或点右下角
将master分支代码合并到本地cherry分支
$ git merge
3.将本地改动推送到orgin/cherry
$git push


从系统入手开始了解功能，熟悉功能之后再了解业务，反过来去印证学习过的功能，知道了为什么要这些功能。
