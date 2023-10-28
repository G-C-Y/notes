## 1. 清除 git 的全局设置（针对已安装 git）
若之前对 git 设置过全局的 user.name 和 user.email。
类似 (用 git config --global --list 进行查看你是否设置)
```shell
$ git config --global user.name "你的名字"
$ git config --global user.email  "你的邮箱"
```
必须删除该设置
```shell
$ git config --global --unset user.name "你的名字"
$ git config --global --unset user.email "你的邮箱"
```
## 2. 生成新的 SSH keys
### 1）GitHub 的钥匙
指定文件路径，方便后面操作：~/.ssh/id_rsa.gitlab
```shell
ssh-keygen -t rsa -f ~/.ssh/id_rsa.github -C "lx@qq.com"
```
直接回车3下，什么也不要输入，就是默认没有密码。
注意 github 和 gitlab 的文件名是不同的。
### 2）Gitee 的钥匙
```shell
ssh-keygen -t rsa -f ~/.ssh/id_rsa.gitlab -C "lx@vip.qq.com"
```
### 3)完成后会在~/.ssh / 目录下生成以下文件

- id_rsa.github
- id_rsa.github.pub
- id_rsa.gitlab
- id_rsa.gitlab.pub
## 3.添加识别 SSH keys 新的私钥
默认只读取 id_rsa，为了让 SSH 识别新的私钥，需要将新的私钥加入到 SSH agent 中
```shell
$ ssh-agent bash
$ ssh-add ~/.ssh/id_rsa.github
$ ssh-add ~/.ssh/id_rsa.gitlab
```
## 4. 多账号必须配置 config 文件(重点)
若无 config 文件，则需创建 config 文件
### 创建config文件
```shell
$ touch ~/.ssh/config    
```
### config 里需要填的内容
亲测可以不缩进，所以方便看，建议缩进。
### 最简配置
```shell
Host github.com
    HostName github.com
    IdentityFile ~/.ssh/id_rsa.github
```
### 完整配置
```shell
#Default gitHub user Self
Host github.com
    HostName github.com
    User git #默认就是git，可以不写
    IdentityFile ~/.ssh/id_rsa.github

#Add gitLab user 
    Host git@gitlab.com
    HostName gitlab.com
    User git
    IdentityFile ~/.ssh/id_rsa.gitlab

# gitee
Host gitee.com
    Port 22
    HostName gitee.com
    User git
    IdentityFile ~/.ssh/id_rsa.gitee


# 其他自己搭建的
Host git@git.startdt.net
    Port 22
    HostName http://git.startdt.net
    User git
    IdentityFile ~/.ssh/lab_rsa.startdt
```
下面对上述配置文件中使用到的配置字段信息进行简单解释：

- Host
它涵盖了下面一个段的配置，我们可以通过他来替代将要连接的服务器地址。
这里可以使用任意字段或通配符。
当ssh的时候如果服务器地址能匹配上这里Host指定的值，则Host下面指定的HostName将被作为最终的服务器地址使用，并且将使用该Host字段下面配置的所有自定义配置来覆盖默认的/etc/ssh/ssh_config配置信息。
- Port
自定义的端口。默认为22，可不配置
- User
自定义的用户名，默认为git，可不配置
- HostName
真正连接的服务器地址
- PreferredAuthentications
指定优先使用哪种方式验证，支持密码和秘钥验证方式
- IdentityFile
指定本次连接使用的密钥文件
## 5.在 github 和 gitlab 网站添加 ssh
### Github
Github 添加SSH公钥
直达地址：[https://github.com/settings/keys](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fsettings%2Fkeys)
过程如下：

1. 登录 Github
2. 点击右上方的头像，点击 settings
3. 选择 SSH key
4. 点击 Add SSH key

在出现的界面中填写 SSH key 的名称，填一个你自己喜欢的名称即可。
将上面拷贝的~/.ssh/id_rsa.xxx.pub文件内容粘帖到 key 一栏，在点击 “add key” 按钮就可以了。
添加过程 github 会提示你输入一次你的 github 密码 ，确认后即添加完毕。
### Gitlab
Gitlab 添加SSH公钥
直达地址：[https://gitlab.com/profile/keys](https://links.jianshu.com/go?to=https%3A%2F%2Fgitlab.com%2Fprofile%2Fkeys)

1. 登录 Gitlab
2. 点击右上方的头像，点击 settings
3. 后续步骤如 Github
## 6.测试是否连接成功
由于每个托管商的仓库都有唯一的后缀，比如 Github 的是 [git@github.com](https://links.jianshu.com/go?to=mailto%3Agit%40github.com):*。
所以可以这样测试：
ssh -T [git@github.com](https://links.jianshu.com/go?to=mailto%3Agit%40github.com)
而 gitlab 的可以这样测试：
ssh -T [git@gitlab.corp.xyz.com](https://links.jianshu.com/go?to=mailto%3Agit%40gitlab.corp.xyz.com)
如果能看到一些 Welcome 信息，说明就是 OK 的了
![image.png](https://images.cherryfloris.eu.org/2023/1678074339880-603dc59f-b315-4583-b969-ac68bf224e15.png)
结果如果出现这个就代表成功：

- GitHub -> successfully
- GitLab -> Welcome to GitLab
- Gitee -> successfully
### 测试 clone 项目
```shell
git clone git@github.com:alixaxel/pagerank.git
Cloning into 'pagerank'...
remote: Enumerating objects: 54, done.
remote: Total 54 (delta 0), reused 0 (delta 0), pack-reused 54
Receiving objects: 100% (54/54), 9.86 KiB | 1.09 MiB/s, done.
Resolving deltas: 100% (25/25), done.

```
参考链接：[https://www.jianshu.com/p/68578d52470c](https://www.jianshu.com/p/68578d52470c)
# 解决git@github.com: Permission denied (publickey). fatal: Could not read from remote repository. 
一:原因分析
Permission denied (publickey) 没有权限的publickey ，出现这错误一般是以下两种原因
客户端与服务端未生成 ssh key
客户端与服务端的ssh key不匹配
找到问题的原因了，解决办法也就有了，重新生成一次ssh key ，服务端也重新配置一次即可。
解决办法：
重新生成ssh key后，ssh-add -l  检查是否有邮箱与密钥生成，没有就添加
![image.png](https://images.cherryfloris.eu.org/2023/1678086471503-05279abf-6dab-4b81-86fe-c0e5c715efbd.png)

![image.png](https://images.cherryfloris.eu.org/2023/1678086548777-38746cca-518e-4af5-9740-004864010c94.png)

# 一个Git终端如何配置多个Git仓库和账户
因为存在双/多账户，需要通过Git配置不同账户的用户和邮箱，这里采取GitLab用全局用户名和邮箱配置，而GitHub针对每个clone到本地的项目进行单独的用户名和邮箱配置，避免冲突。
1.配置全局的用户名和邮箱
// 将GitLab设置为全局 git config --global user.name "gitlab" git config --global user.email "gitlab@126.com"
2.为GitHub上的每个repository/项目单独设置用户名和邮箱
// 注意：下述命令要到每个本地GitHub项目目录下执行 git config user.name "github" git config user.email "github@126.com"
3.最后进行可以代码的修改，拉取、提交、push等，验证配置是否成功
上述都配置、测试成功后，我们就可以在公司项目和自己参与的开源项目之间进行不同的管理和使用了。
```shell
git config --global user.name cherry
git config --global user.email guocy_oepd@si-tech.com
```
![image.png](https://images.cherryfloris.eu.org/2023/1678088364019-bf29ca85-c49b-45ad-bcf0-2198bf200432.png)
```shell
git config user.name "cherry"
git config user.signingkey Gcy.1430085869
git config user.email guo_chenying@163.com
```
![image.png](https://images.cherryfloris.eu.org/2023/1678088300533-a01ecdb7-378a-413e-9cbb-d90fa2f9e196.png)
# Git - git-clone 期间 permission denied
[https://blog.csdn.net/BIT_666/article/details/118851295](https://blog.csdn.net/BIT_666/article/details/118851295)
