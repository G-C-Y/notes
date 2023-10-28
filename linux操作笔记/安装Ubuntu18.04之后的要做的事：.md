[https://blog.csdn.net/haeasringnar/article/details/81809040](https://blog.csdn.net/haeasringnar/article/details/81809040)
1、更新源，使用软件更新器选择中国的服务器aliyun即可自动更新缓存，以及各种软件
之后每天更新,
shell更新：
```
sudo apt update
sudo apt upgrade
```
2、安装vim、wget、curl、net-tools
```
sudo apt install -y vim curl wget net-tools
```
配置十字光标：用户目录下
```
vim .vimrc
```
然后输入一下内容：
```
set nu
set tabstop=4
set cuc
set cul
```
如果出现依赖错误，那么就输入sudo apt install -f 解决依赖错误问题即可
3、安装搜狗输入法
[搜狗输入法Linux64位下载地址](http://cdn2.ime.sogou.com/dl/index/1524572264/sogoupinyin_2.2.0.0108_amd64.deb?st=3lH-P_6gAW4OrLs2tsrG8w&e=1534577837&fn=sogoupinyin_2.2.0.0108_amd64.deb)
```
sudo apt install fcitx-bin      #安装fcitx-bin
sudo apt update --fix-missing   #修复fcitx-bin安装失败的情况
sudo apt install fcitx-bin      #重新安装fcitx-bin
sudo apt install fcitx-table    #安装fcitx-table
```
然后去搜狗官网下载好给予linux的搜狗输入法deb安装包
```
sudo dpkg -i sogoupinyin*.deb       #安装搜狗拼音
sudo apt install -f             #修复搜狗拼音安装的错误
sudo dpkg -i sogoupinyin*.deb       #重新安装搜狗拼音
```
输入法安装成功后要重新进入系统生效，重新登录或重启。
4、安装wps
[wps-linux下载地址](http://community.wps.cn/download/)
事先下载好wps deb包，必要的libpng12-0依赖，以及wps 必要的字体文件


sudo dpkg -i wps*.deb   # 安装wps
sudo apt install -f             # 发生错误时
sudo dpkg -i wps*.deb   # 重新安装wps
1
2
3
4
5
然后处理字体问题
字体文件
字体文件下载解压之后放到系统的字体库里面，新建一个用来放wps的字体

sudo mkdir /usr/share/fonts/WPS-Fonts       #新建wps字体存储文件夹
1
将字体文件夹放到 WPS-Fonts
然后：

sudo mkfontscale    #生成字体索引

sudo mkfontdir      #生成字体索引

sudo fc-cache       #更新字体缓存
1
2
3
4
5
然后重启wps，就可以发现字体问题解决啦！
顺便卸载掉系统自带的office

sudo apt remove libreoffice-common
1
5、Python开发者直接安装Anaconda即可
具体安装步骤请移步
Anaconda安装及使用

6、安装chrome浏览器
chrome-linux下载地址
然后

sudo dpkg -i google-chrome-stable_current_amd64.deb
1
如果出现依赖问题没有安装成功：

sudo apt install -f
1
然后：

sudo dpkg -i google-chrome-stable_current_amd64.deb
1
7、安装Opera浏览器
Opera-linux下载地址

到官网网站下载deb包，然后安装，安装方式和chrome一致

8、安装node.js 以及 npm 和cnpm的配置
node.js下载地址

先下载好node.js的官方资源，推荐使用后缀为LTS(长期支持)
然后解压缩到你自己的目录下，
将压缩包名改为node方便后续操作

mv node-v8.11.4-linux-x64.tar.gz node
1
然后修改.profile 或者 .bashrc 文件

vim ~/.bashrc
1
然后在最后面加上自己的配置

export NODE_HOME=/home/node  #你的node目录的路径

export PATH=![](https://g.yuque.com/gr/latex?PATH%3A#card=math&code=PATH%3A&id=BPkxf)NODE_HOME/bin

export NODE_PATH=$NODE_HOME/lib/node_modules
1
2
3
4
5
然后重启.profile或者.bashrc

source ~/.bashrc
1
验证是否配置成功：
在终端中输入

npm -V
1
题外话：cnpm的配置
方法一：

npm install -g cnpm --registry=https://registry.npm.taobao.org
1
方法二：
在.bashrc 或者.profile 内部添加一下代码

alias cnpm="npm --registry=https://registry.npm.taobao.org 
--cache=![](https://g.yuque.com/gr/latex?HOME%2F.npm%2F.cache%2Fcnpm%20%5C%0A--disturl%3Dhttps%3A%2F%2Fnpm.taobao.org%2Fdist%20%5C%0A--userconfig%3D#card=math&code=HOME%2F.npm%2F.cache%2Fcnpm%20%5C%0A--disturl%3Dhttps%3A%2F%2Fnpm.taobao.org%2Fdist%20%5C%0A--userconfig%3D&id=QBB0o)HOME/.cnpmrc"
1
2
3
4
然后重启.profile或者.bashrc

source ~/.bashrc
1
验证是否配置成功：
在终端中输入

cnpm -V
1
9、安装链接服务器的ssh服务器
首先在服务器上安装SSH的服务器端。

sudo apt install openssh-server
1
启动ssh-server。

/etc/init.d/ssh restart
1
确认ssh-server是否正常工作

netstat -tlp
tcp6 0 0 :ssh :* LISTEN -
1
2
上面这一行就说明ssh-server已经在运行了。

在Ubuntu客户端通过SSH登录服务器。假设服务器的IP地址是113.112.23.124，登录的用户名是name。

ssh -l name 113.112.23.124
1
最后提示你输入密码，就说明连上远程服务器了。

题外话：使用ssh-key登录服务器

仅需通过3个步骤的简单设置而无需输入密码就能登录远程Linux主机。
ssh-keygen 创建公钥和密钥。
ssh-copy-id 把本地主机的公钥复制到远程主机的authorized_keys文件上。
1: 用 ssh-key-gen 在本地主机上创建公钥和密钥

ssh-keygen -t rsa -C "[youremail@example.com](mailto:youremail@example.com)"
1
在你的用户目录下就会有一个.ssh的目录，里面的id_rsa是你的秘钥 id_rsa.pub是你的公钥
2: 用 ssh-copy-id 把公钥复制到远程主机上

ssh-copy-id -i ~/.ssh/id_rsa.pub  [root@111.111.111.111](mailto:root@111.111.111.111) #用的ip替换
1
注意：这一步需要输入服务器密码
注意：ssh-copy-id 把密钥追加到远程主机的 .ssh/authorized_key 上
3: 直接登录远程主机

ssh [root@111.111.111.111](mailto:root@111.111.111.111)
1
安装网络工具

sudo apt install net-tools
1
安装之后就可以使用ifconfig ping等命令

10、安装各种IDE
jetbrains

根据自己的需求下载成功后
由于具体安装方法也是大同小异
无非是deb安装包或tar包解压后直接允许脚本使用
这里建议大家使用社区版或购买激活码使用

11、安装git并配置git
第一步：
安装git。打开终端输入命令

sudo apt install git
1
第二步：

配置本机git的两个重要信息，user.name和user.email,中终端输入如下命令即可设置

git config --global user.name "Your Name"

git config --global user.email "[email@example.com](mailto:email@example.com)"
1
2
3
然后我们可通过命令 git config --list,查看是否设置成功。

第三步：

查看home目录下是否有.ssh目录，一般情况是没有的，需要我们敲命令生成这个目录，在终端输入

ssh-keygen -t rsa -C "[youremail@example.com](mailto:youremail@example.com)"
1
邮箱就是刚刚第二步设置的。然后一路按回车，其实就是不设置密码。然后你就会看到home目录下
多了.ssh目录。

第四步：
进入.ssh目录你会看到两个文件id_rsa和id_rsa.pub,id_rsa是私钥，id_rsa.pub自然就是
公钥啦。然后我们需要做的就是把id_rsa.pub文件中的内容拷贝一下。
第五步：
进入你自己的github，进入Settings->SSH and GPG keys->New SSH key,然后在Key那
栏下面将第四步拷贝的东西粘贴进去就可以了，最后点击 Add SSH key按钮添加。

大功告成，这样你在git push的时候就不需要每次输入用户名和密码了，github作为现在最流行的代码管理
工具，对于程序员来说学会使用它还是很有必要的。

注意：：：如果出现你使用了key，但还是报没有权限的情况下，就要执行下面的操作：
ssh-add ~/.ssh/id_rsa 然后再次链接git会有如下提示
…Are you sure you want to continue connecting (yes/no)? yes
输入yes，发现就可以正常链接到远程仓库了

12、安装截图软件shutter
sudo apt install shutter    #安装shutter
1
然后配置快捷键，快捷键的命令 shutter -s 是新建一个截图

在Ubuntu 18.04中安装了我最喜欢的截图工具Shutter后，我发现编辑按钮变编程灰色。这个快速提示将向您展示如何重新启用Shutter中的编辑功能。
libgoocanvas-common：[https://launchpad.net/ubuntu/+archive/primary/+files/libgoocanvas-common_1.0.0-1_all.deb](https://launchpad.net/ubuntu/+archive/primary/+files/libgoocanvas-common_1.0.0-1_all.deb)
libgoocanvas3：[https://launchpad.net/ubuntu/+archive/primary/+files/libgoocanvas3_1.0.0-1_amd64.deb](https://launchpad.net/ubuntu/+archive/primary/+files/libgoocanvas3_1.0.0-1_amd64.deb)
libgoo-canvas-perl：[https://launchpad.net/ubuntu/+archive/primary/+files/libgoo-canvas-perl_0.06-2ubuntu3_amd64.deb](https://launchpad.net/ubuntu/+archive/primary/+files/libgoo-canvas-perl_0.06-2ubuntu3_amd64.deb)

sudo dpkg -i libgoocanvas-common*.deb
sudo dpkg -i libgoocanvas3*.deb
sudo dpkg -i libgoo-canvas-perl*deb
1
2
3
将上述三个包给安装上，若安装失败，执行下面代码:

sudo apt install -f
1
然后再安装这几个包。
重启！重启！重启！重要的事情说三遍！

13、视频和音频
安装解码器：

sudo apt install ubuntu-restricted-extras
1
安装VLC视频播放器

sudo apt install vlc browser-plugin-vlc
1
另一款比较好的播放器SMPlayer也不错

sudo apt-add-repository ppa:rvm/smplayer
sudo apt update
sudo apt install smplayer smplayer-skins smplayer-themes
1
2
3
安装FFmpeg

sudo add-apt-repository ppa:djcj/hybrid

sudo apt update

sudo apt install ffmpeg
1
2
3
4
5
14安装网易云音乐
网易云下载地址

进入网易云音乐Linux版，下载Ubuntu16.04（64位）。

sudo dpkg -i netease-cloud-music*.deb
1
此时，直接点击网易云音乐，大部分可能是打不开的。解决方案如下：
(1).直接使用命令行打开,但是后台一直有一个终端。

sudo netease-cloud-music
1
可是使用在后台运行：

sudo nohup netease-cloud-music &
1
(2).修改网易云的快捷方式(不推荐，可能会遇到问题)

sudo gedit /usr/share/applications/netease-cloud-music.desktop

找到

Exec=netease-cloud-music %U

这一行，改为：

Exec=netease-cloud-music --no-sandbox %U

重启！重启！重启！重要的事情说三遍！

15、安装franz
franz下载地址

下载deb之后，安装使用即可。

sudo dpkg -i 对应的安装包名
1
如果出现依赖问题，执行：

sudo apt install -f
1
然后再次安装vscode

sudo dpkg -i 对应的安装包名
1
16、安装gimp 类似ps的软件
sudo apt install gimp
1
安装相关插件

sudo apt install gimp-plugin-registry gimp-data-extras
1
插件 描述
gimp-data-extras 刷子/调色板/渐变色的GIMP插件集
gimp-gmic 用于《GREYC魔术图像转换软件》的GIMP插件
gimp-gutenprint GIMP的打印插件
gimp-plugin-registry GIMP的可选扩展库
gvfs-backends 用户空间虚拟文件系统-后端
xcftools 命令行工具，用于XCF文件的额外数据
gimp-gap gif动态图制作插件
mathmap 制作德罗斯特效应插件

17、安装mysql5.7
安装mysql服务：

sudo apt install mysql-server-5.7
1
安装客户端：

sudo apt install mysql-client-5.7
1
安装依赖：

sudo apt install libmysqlclient-dev
1
检查状态：

sudo netstat -tap | grep mysql
1
注意查看mysql版本使用：mysql -V 命令
查看MySQL5.7默认账号和密码：

sudo cat /etc/mysql/debian.cnf
1
查看用户已经修改重置root密码
mysql> select user, plugin from mysql.user;
±-----------------±----------------------+
| user | plugin |
±-----------------±----------------------+
| root | auth_socket |
| mysql.session | mysql_native_password |
| mysql.sys | mysql_native_password |
| debian-sys-maint | mysql_native_password |
±-----------------±----------------------+
4 rows in set (0.00 sec)
mysql> update mysql.user set authentication_string=PASSWORD('123456'), plugin='mysql_native_password' where user='root';
mysql>flush privileges;
mysql> exit
Bye
配置远程访问mysql:
修改配置文件，注释掉bind-address = 127.0.0.1

sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
1
保存退出，然后进入mysql服务，执行授权命令：

mysql -uroot -p
1
mysql> grant all on . to root@’%’ identified by ‘123456’ with grant option;
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)

mysql> exit
Bye

sudo /etc/init.d/mysql restart
1
但有些时候你装错了，想删了重新安装：那么
彻底删除MySQL
此教程是你想安装MySQL 8.0或者重装MySQL 5.7的前提条件，如果你没有这两个需求，此教程可以忽略！

1.删除 mysql:

sudo apt autoremove --purge mysql-server-*

sudo apt remove mysql-server

sudo apt autoremove mysql-server

sudo apt remove mysql-common
1
2
3
4
5
6
7
2.清理残留数据

dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
1
18、安装g++ gcc 开发必备编译库
讲开发没有编译器，那么一切都是浮云。
Ubuntu默认是不安装g++的

sudo apt install build-essential
1
下面这些看自己爱好:
安装词法和语法分析器

sudo apt install flex

sudo apt install bison
1
2
3
19、安装sublime3
sublime下载地址

然后直接解压出来，双击里面的sublime_text就可以使用了

20、安装靠谱又简介的markdown编辑器typora
依次执行：

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA300B7755AFCFAE

sudo add-apt-repository 'deb [https://typora.io/linux](https://typora.io/linux) ./'

sudo apt update

sudo apt install typora
1
2
3
4
5
6
7
21、安装mysql可视化，Linux上比较好的一款mysql-workbench
sudo apt install mysql-workbench
1
出现依赖包无法下载错误时

sudo apt update --fix-missing
1
然后再次执行

sudo apt install mysql-workbench
1
22、安装vscode
vscode下载地址

然后

sudo dpkg -i 对应的安装包名
1
如果出现依赖问题，执行：

sudo apt install -f
1
然后再次安装vscode

sudo dpkg -i 对应的安装包名
1
23、安装nginx
使用apt安装

sudo apt install nginx
1
安装好的位置：
/usr/sbin/nginx：主程序

/etc/nginx：存放配置文件

/usr/share/nginx：存放静态文件

/var/log/nginx：存放日志

service nginx start  #启动nginx
service nginx reload  #重新加载nginx
1
2
在浏览器输入你的ip地址，如果出现Wellcome to nginx 那么就是配置成功。

23、安装postman
postman下载地址

然后解压到自己的目录，然后双击postman就可以使用了。
###24、安装FileZilla客户端
FileZilla是用来方便的向你的服务器上传文件的工具，在源里面已经存在了直接安装使用即可

sudo apt install filezilla
1
24、安装优化工具 gnome-tweak-tool
sudo apt install gnome-tweak-tool
1
安装成功后，去软件中心安装 dash to dock
它是gnome-tweak-tool的dock扩展，可以使你有一个更灵活的dock栏
