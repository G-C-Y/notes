基于节点红的监视服务，可监听以太坊区块链上的事件
## 前提条件（30分钟）
确保您正在运行[受支持](https://nodered.org/docs/faq/node-versions)的node.js[版本](https://nodered.org/docs/faq/node-versions)。
## 步骤1：下载并安装Node-Red
[对于Linux / Mac](https://nodered.org/docs/getting-started/local)：
sudo npm install -g --unsafe-perm node-red
![image.png](https://images.cherryfloris.eu.org/2021/1620658107860-8471e98c-5355-45f5-a325-b629ae2f99b5.png)
[对于Windows](https://nodered.org/docs/getting-started/windows)：
npm install -g --unsafe-perm node-red

## 第2步：下载或克隆存储库（2分钟）
git clone https://github.com/shopfs/service.git
![image.png](https://images.cherryfloris.eu.org/2021/1620658981194-30d66db8-4d54-4ac9-8967-9f390e95b473.png)
（此处记得使用github提速小技巧）
cd <cloned repo root folder path>
![image.png](https://images.cherryfloris.eu.org/2021/1620659266018-60d9d12f-a7be-4568-aa0a-d9e831a5dd0a.png)
npm install

使用以下命令启动红色节点
node-red  --userDir <cloned repo root folder path>
![image.png](https://images.cherryfloris.eu.org/2021/1620659712308-4a061226-cada-4a36-8783-f693ec448c65.png)
运行后，请转到：[http：// localhost：1880](http://localhost:1880/)
![image.png](https://images.cherryfloris.eu.org/2021/1620660140504-db42b615-7745-4a87-b34d-4840ba9aae18.png)
[https://nodered.org/docs/](https://nodered.org/docs/)   官方网址
