### Virtual-Doctor
Virtual Doctor是一个基于React的Web应用程序，用于数字化医生与患者之间的通信。该应用程序使用区块链来保护患者和医生的信息。此应用程序的主要功能是：登录身份验证，与医生在线约时间 ，提供处方，创建报告，通过管理员删除患者或医生。此应用程序由三个用户Admin，Doctor和Patient组成。管理员仅具有添加和删除其他用户的权限，并且无权访问任何患者的健康信息。管理员仅管理系统中的添加用户，删除用户和密码更改请求。我们系统中的第二种用户类型是患者，患者有权查看其医疗信息并进行约会，该患者无法更改其医疗信息。一旦将数据添加到区块链上，就无法以任何方式进行更改。我们系统中的第三种用户类型是医生，医生有权查看他的约会，开药和创建患者报告。有权添加患者报告的只有医生。我们的智能合约还使用OnlyDoctor的修饰符，该修饰符可确保医生是唯一可以添加患者医疗信息的人。GitHub链接：[https://github.com/Nancy-cy/Virtual-Doctor.git](https://github.com/Nancy-cy/Virtual-Doctor.git)
```markdown
To run frontend separately(port 3000)
	
	cd frontend
	npm start

--------------------------

To run backend separately(port 5000)

	npm run server(with nodemon)
	npm start

--------------------------

To run both concurrently

	npm run dev

--------------------------

To run flask server(port 4000)

	pip install -U flask-cors
	set FLASK_APP=app.py
	set FLASK_RUN_PORT=4000
	flask run

--------------------------

for backend package.json

	npm i bcryptjs body-parser concurrently cors express pg
	npm i -D nodemon

	npm start

--------------------------

for frontend package.json

	cd frontend
	npm i antd formik react react-dom react-redux react-router-dom react-scripts react-simple-chatbot redux styled-components yup

npm start

--------------------------

NOTE:
	DML contains password in hashed format .The password is 1234
	When creating a new user, the id is used as a password and the user can change it after logging in

	Admin   ->  A190001 - 1234
	Doctor  ->  D190001 - 1234
	Patient ->  P190001 - 1234
```
前端后端运行之后，出现登录界面，但无法进入，原因是数据库没有连接，这时候需要新建一个数据库，开发者已给出本地的数据，建表即可。
```markdown
Create DB with PostgreSQl

https://youtube/RySuQtMiBxQ

	(Go to)SQl shell

	login with postgres user and password

	CREATE USER taha WITH PASSWORD 'taha1';

	CREATE DATABASE hospital WITH OWNER taha;

	\l
	
	\c hospital

Connect PostgreSQL DB with DBeaver

https://youtube/XRdl0P4V-PU
```
![image.png](https://images.cherryfloris.eu.org/2021/1622717175618-7cfdbba7-e796-4cce-b336-70253dc6e893.png)
![image.png](https://images.cherryfloris.eu.org/2021/1622717253841-7ed3c0e6-c821-43e0-a36e-d9d276bbfc94.png)
数据库部分
### 在 Ubuntu 上安装 PostgreSQL
PostgreSQL 可以从 Ubuntu 主存储库中获取。然而，和许多其它开发工具一样，它可能不是最新版本。
首先在终端中使用 [apt 命令](https://itsfoss.com/apt-command-guide/) 检查 [Ubuntu 存储库](https://itsfoss.com/ubuntu-repositories/) 中可用的 PostgreSQL 版本：
```markdown
apt show postgresql
```
![image.png](https://images.cherryfloris.eu.org/2021/1622706113518-684aabb3-d834-44d1-bde2-9fe55f9e2b5d.png)
在我的 Ubuntu 16.04 中，它显示 PostgreSQL 的可用版本是 9.5（9.5+173 表示版本9.5）而 PostgreSQL 版本 11 已经发布。
根据这些信息，你可以自主决定是安装 Ubuntu 提供的版本还是还是获取 PostgreSQL 的最新发行版。
#### 通过 Ubuntu 存储库安装 PostgreSQL
在终端中，使用以下命令安装 PostgreSQL：
```markdown
sudo apt update
sudo apt install postgresql postgresql-contrib
```
根据提示输入你的密码，依据于你的网速情况，程序将在几秒到几分钟安装完成。说到这一点，随时检查 [Ubuntu 中的各种网络带宽](https://itsfoss.com/network-speed-monitor-linux/)。
什么是 postgresql-contrib?
postgresql-contrib 或者说 contrib 包，包含一些不属于 PostgreSQL 核心包的实用工具和功能。在大多数情况下，最好将 contrib 包与 PostgreSQL 核心一起安装。
#### PostgreSQL 配置
可以通过执行以下命令来检查 PostgreSQL 是否正在运行：
```markdown
service postgresql status
```
通过 service 命令，你可以启动、关闭或重启 postgresql。输入 service postgresql 并按回车将列出所有选项。现在，登录该用户。
默认情况下，PostgreSQL 会创建一个拥有所权限的特殊用户 postgres。要实际使用 PostgreSQL，你必须先登录该账户：
```markdown
sudo su postgres
```
你的提示符会更改为类似于以下的内容：
postgres@ubuntu-VirtualBox:/home/ubuntu$ 
![image.png](https://images.cherryfloris.eu.org/2021/1622707223744-9292333c-bb56-48ba-ba74-b6a82563d9eb.png)
现在，使用 psql 来启动 PostgreSQL Shell：
psql
你应该会看到如下提示符：
postgress=#
你可以输入 \q 以退出，输入 \? 获取帮助。
要查看现有的所有表，输入如下命令：
\l
输出内容类似于下图所示（单击 q 键退出该视图）：
![image.png](https://images.cherryfloris.eu.org/2021/1622707152555-fb277f2d-401a-490c-b399-d3beca1556e0.png)
_PostgreSQL Tables_
使用 \du 命令，你可以查看 PostgreSQL 用户：
![image.png](https://images.cherryfloris.eu.org/2021/1622707152592-89cf9936-92ed-4266-a4e1-9dfc837f8256.png)
_PostgreSQLUsers_
你可以使用以下命令更改任何用户（包括 postgres）的密码：
ALTER USER postgres WITH PASSWORD 'my_password';
**注意：**将 postgres 替换为你要更改的用户名，my_password 替换为所需要的密码。另外，不要忘记每条命令后面的 ;（分号）。
建议你另外创建一个用户（不建议使用默认的 postgres 用户）。为此，请使用以下命令：
CREATE USER my_user WITH PASSWORD 'my_password';
运行 \du，你将看到该用户，但是，my_user 用户没有任何的属性。来让我们给它添加超级用户权限：
ALTER USER my_user WITH SUPERUSER;
你可以使用以下命令删除用户：
DROP USER my_user;
要使用其他用户登录，使用 \q 命令退出，然后使用以下命令登录：
psql -U my_user
你可以使用 -d 参数直接连接数据库：
psql -U my_user -d my_db
你可以使用其他已存在的用户调用 PostgreSQL。例如，我使用 ubuntu。要登录，从终端执行以下命名：
psql -U ubuntu -d postgres
**注意：**你必须指定一个数据库（默认情况下，它将尝试将你连接到与登录的用户名相同的数据库）。
如果遇到如下错误：
psql: FATAL:  Peer authentication failed for user "my_user"
确保以正确的用户身份登录，并使用管理员权限编辑 /etc/postgresql/11/main/pg_hba.conf：
sudo vim /etc/postgresql/11/main/pg_hba.conf
**注意：**用你的版本替换 11（例如 10）。
对如下所示的一行进行替换：
local   all             postgres                                peer
替换为：
local   all             postgres                                md5
然后重启 PostgreSQL：
sudo service postgresql restart
使用 PostgreSQL 与使用其他 SQL 类型的数据库相同。由于本文旨在帮助你进行初步的设置，因此不涉及具体的命令。不过，这里有个 [非常有用的要点](https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546) 可供参考! 另外, 手册（man psql）和 [文档](https://www.postgresql.org/docs/manuals/) 也非常有用。
#### 总结
阅读本文有望指导你完成在 Ubuntu 系统上安装和准备 PostgreSQL 的过程。如果你不熟悉 SQL，你应该阅读 [基本的 SQL 命令](https://itsfoss.com/basic-sql-commands/)。
参考：[https://linux.cn/article-11480-1.html](https://linux.cn/article-11480-1.html)

### 在Ubuntu上安装DBeaver
下载安装包
```markdown
wget http://dbeaver.jkiss.org/files/dbeaver-ce-latest-linux.gtk.x86_64.tar.gz
```
解压
```markdown
tar -zxvf dbeaver-ce-latest-linux.gtk.x86_64.tar.gz 
```
打开文件夹，执行dbeaver
```markdown
cd dbeaver
sudo ./dbeaver
```
![image.png](https://images.cherryfloris.eu.org/2021/1622716428235-b7ac162f-e378-4354-8c95-bd26e0f72778.png)
然后连接数据库hospital，登录密码，然后点击上访的SQL编辑器，将作者给的三段代码粘贴，这个是用SQL建表插入数据的过程
![image.png](https://images.cherryfloris.eu.org/2021/1623290916228-31812b86-d7e3-4162-851f-3be17b5da606.png)
之后便可看到web应用程序成功接入后台。
![image.png](https://images.cherryfloris.eu.org/2021/1623290404334-b58cc12f-e3cb-45c3-b9e4-bbd1de35aa58.png)
NOTE:
webpack的目录结构app/ - 你的应用文件运行的默认目录。这里面包括推荐的javascript文件和css样式文件目录，但你可以完全决定如何使用这些目录。

contract/ - Truffle默认的合约文件存放目录。

migrations/ - 部署脚本文件的存放目录

test/ - 用来测试应用和合约的测试文件目录

truffle.js - Truffle的配置文件
[
](https://blog.csdn.net/weixin_43988498/article/details/109284993)
