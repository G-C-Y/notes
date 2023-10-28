陈宇鹏分享
写在前面：本文章会详细介绍fabric最新版本（fabric2.2）的环境部署，以及在搭建过程中博主遇到一些坑，希望可以帮助到你们。

博主环境机器：VMware   Ubuntu20.4    写于2020/7/29

感谢博文以及参考文章：[https://www.cnblogs.com/cbkj-xd/p/11067790.html](https://www.cnblogs.com/cbkj-xd/p/11067790.html)

[https://blog.csdn.net/qq_43681877/article/details/107399250](https://blog.csdn.net/qq_43681877/article/details/107399250)

目录

一、必备软件安装

1.Go语言

2.Docker安装

3. Docker-Compose 安装

二、Fabric2.2 环境搭建

一、必备软件安装
如果你的Linux是新安装的，最好将源换成国内的，否则一些文件会下不下来，操作可以参考：[https://www.cnblogs.com/masbay/p/10887571.html](https://www.cnblogs.com/masbay/p/10887571.html)

推荐阿里云和163。阿里云是我看好像大家都用的，至于为啥推荐163我后面会提到。

1.Go语言
首先安装一些必要的依赖：

sudo apt install libtool libltdl-dev
去该网站 [https://studygolang.com/dl](https://studygolang.com/dl) 下载Go语言的安装包，我下的是目前最新版本: go1.14.6.linux-amd64.tar.gz

将压缩包复制到/usr/local路径下,然后进行解压：

cd /usr/local
tar zxvf go1.14.6.linux-amd64.tar.gz
配置GO的环境变量：

打开配置文件：

sudo vim ~/.profile
在文件中添加以下内容：

export PATH=![](https://g.yuque.com/gr/latex?PATH%3A%2Fusr%2Flocal%2Fgo%2Fbin%0Aexport%20GOROOT%3D%2Fusr%2Flocal%2Fgo%0Aexport%20GOPATH%3D#card=math&code=PATH%3A%2Fusr%2Flocal%2Fgo%2Fbin%0Aexport%20GOROOT%3D%2Fusr%2Flocal%2Fgo%0Aexport%20GOPATH%3D&id=I4Kvu)HOME/go
export PATH=![](https://g.yuque.com/gr/latex?PATH%3A#card=math&code=PATH%3A&id=OSAnR)GOPATH/bin
更新配置文件：

source ~/.profile
此时Go就安装完成，可以用以下命令查看是否安装成功：

go version
如果显示了版本号，就说明安装成功。我的版本号是这样的： go version go1.14.6 linux/amd64 。

2.Docker安装

如果Ubuntu系统中有旧版本的Docker，需要卸载后重新安装。操作如下：

sudo apt-get remove docker 
docker-engine 
docker.io



然后执行以下命令安装Docker：

# step 1: 安装必要的一些系统工具

sudo apt-get update
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common

# step 2:安装GPG证书：

curl -fsSL [http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg](http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg) | sudo apt-key add -

# step 3:写入软件源信息

sudo add-apt-repository "deb [arch=amd64] [http://mirrors.aliyun.com/docker-ce/linux/ubuntu](http://mirrors.aliyun.com/docker-ce/linux/ubuntu) $(lsb_release -cs) stable"

# step 4:更新并安装Docker-CE

sudo apt-get -y update
sudo apt-get -y install docker-ce
将当前用户添加到Docker用户组：

# step 1: 创建docker用户组

sudo groupadd docker

# step 2:将当前用户添加到docker用户组

sudo usermod -aG docker $USER
#退出当前终端
exit
编辑/etc/docker/daemon.json文件，如果没有则自行创建，添加以下内容：

{
"registry-mirrors": ["[http://f1361db2.m.daocloud.io](http://f1361db2.m.daocloud.io)","[https://hub-mirror.c.163.com](https://hub-mirror.c.163.com)","[https://xsoeja86.mirror.aliyuncs.com](https://xsoeja86.mirror.aliyuncs.com)"]
}
这个就是我遇到一个大坑 ，好多别的教程都会叫你写daocloud或者aliyun的镜像源，但是在下后面的二进制文件时候根本没有用！！后来好不容易看到有人用了163，我就试了试，163还是很好用的！！我上面虽然写了三个镜像源网址，但是其实管用只有163，你也可以只写163的。

最后重启服务：

sudo systemctl daemon-reload
sudo systemctl restart docker
docker在这就安装完成，你可以查看版本来检测是否安装成功：

docker -v
我的是：Docker version 19.03.12, build 48a66213fe 。

3. Docker-Compose 安装
下载docker-compose的二进制包：

curl -L [https://github.com/docker/compose/releases/download/1.25.0-rc1/docker-compose-](https://github.com/docker/compose/releases/download/1.25.0-rc1/docker-compose-)`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
#执行这一步时如果出现如下信息：

# Warning: Failed to create the file /usr/local/bin/docker-compose: Permission

# 则添加sudo 重新执行

#更改权限
sudo chmod +x /usr/local/bin/docker-compose
安装完成可以查看版本信息来检测是否安装成功：

docker-compose -v
我的是：docker-compose version 1.25.0-rc1, build 8552e8e2

二、Fabric2.2 环境搭建
首先创建文件夹

cd                  #cd 不加内容是默认返回Home文件夹
mkdir -p go/src/github.com/hyperledger/
#进入刚刚创建的文件夹内
cd go/src/github.com/hyperledger/
从github上拉取fabric的源码：

git clone "[https://github.com/hyperledger/fabric.git](https://github.com/hyperledger/fabric.git)"
cd fabric/
cd scripts/
#这一步会下载官方的例子以及所需要的Docker镜像
#下载是比较慢的，如果出现错误或者长时间没有速度只需要重新运行就可以了
sudo ./bootstrap.sh
注意：运行bootstrap.sh会下载很多东西，大约1~2个G，有点慢，国内把这个官网墙了，所以我们才需要之前设置镜像源，当时我就是在这里用daocloud或者aliyun怎么都下不下来，后来换了163的才好。可能有部分文件还是会下不下来，只要多运行几遍就好了。

到此fabric2.2环境就已经搭建好了。

全部下载完成后，会多出一个fabric-samples文件夹，这是个测试网络样例可以让你体验或者测试。

切换到fabric-samples文件夹:

cd fabric-samples
切换到test-network：

cd test-network/
启动测试网络：

sudo ./network.sh up
如果没出现错误，说明你的fabric已经搭建好了。


原文链接：[https://blog.csdn.net/shengsikandan/article/details/107656060](https://blog.csdn.net/shengsikandan/article/details/107656060)
