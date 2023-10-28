# 创建一个solidity文件(包含两个智能合约)
## 众筹项目的智能合约
```go
contract Funding{
    //众筹faqiren
    bool flag=false;
    address public manager;
    string public projectName;
    uint public supportMoney;
    uint public endTime;
    uint public goalMoney;
    address[] public players;
    mapping(address=>bool) playersMap;
    Request[] public requests;

    struct Request{
        string description;
        uint money;
        address shopAddress;
        bool complete;
        /*address[] voteAddress;*/
        mapping(address=>bool) voteMap;
        uint voteCount;
    }

    function createRequest(string  _description,uint _money,address _shopAddress) public onlyManger{
        // require(msg.sender==manager);
        Request memory request=Request({
            description : _description,
            money : _money,
            shopAddress : _shopAddress,
            complete : false,
            /* voteAddress: new address[](0),*/
            voteCount : 0
            });
        requests.push(request);
    }

    function approveRequest(uint index)public{
        Request storage request=requests[index];
        /*bool supporter = false;
        for(uint i=0;i<players.length;i++)
        {
            if(players[i]==msg.sender)
            supporter =true;
        }
        require(supporter);*/

        require(playersMap[msg.sender]);
        /*
         bool vote=false;
         for(uint j=0;j<request.voteAddress.length;j++)
         {
             if(request.voteAddress[j]==msg.sender)
             vote=true;
         }
         require(!vote);*/
        require(!requests[index].voteMap[msg.sender]);
        request.voteCount++;
        requests[index].voteMap[msg.sender]=true;
    }


    function finalizeRequest(uint index)public onlyManger{
        Request storage request=requests[index];
        require(!request.complete);
        require(request.voteCount*2>=players.length);
        require(this.balance>=request.money);
        request.shopAddress.transfer(request.money);
        request.complete = true;
    }

    constructor (string _projectName,uint _supportMoney,uint _goalMoney,address _address) public {
        // manager=msg.sender;
        manager=_address;
        projectName=_projectName;
        supportMoney=_supportMoney;
        goalMoney=_goalMoney;
        endTime=now+4 weeks;
    }

    function support() public payable{
        require(msg.value==supportMoney);
        players.push(msg.sender);
        playersMap[msg.sender]=true;
    }

    function getPlayerCount() public view returns(uint)
    {
        return players.length;
    }

    function getPlayers() public view returns(address[])
    {
        return players;
    }

    function getTotalBalance() public view returns (uint){
        return this.balance;
    }

    function getRemainDays() public view returns(uint){
        return (endTime-now)/24/60/60;
    }

    /* function checkStatus() {
         require(!flag);
         require(now>endTime);
         require(this.balance>goalMoney);
         flag=true;

     }*/

    modifier onlyManger()
    {
        require(msg.sender==manager);
        _;
    }

}
```
## 部署智能合约的合约创建
```go
contract FundingFactory{

    //address[] public fundings;
    uint public numFundings = 0;
    mapping(uint => address) addrfundings;

    function deploy(string _projectName,uint _supportMoney,uint _goalMoney) public{
        addrfundings[numFundings]=new Funding(_projectName,_supportMoney,_goalMoney,msg.sender);
        numFundings++;
    }
    function getAddr()public view returns(address){//拿到本次部署的智能合约地址
        return addrfundings[numFundings - 1];
    }

}
```
## 编译文件（暴露Factory智能合约）
```go
//编译
const path=require('path');
const fs=require('fs');
const solc=require('solc');
//contract文件夹的名字
const srcpath = path.resolve(__dirname,'contract','Funding.sol');
//console.log(srcpath);读出地址
const source = fs.readFileSync(srcpath,'utf-8');
//console.log(source);打印出智能合约，读出来了
const result=solc.compile(source,1);
//console.log(result);
//console.log(result.contracts[':FundingFactory']);
//暴露信息 contracts方法
module.exports=result.contracts[':FundingFactory'];
```
## 编译文件（暴露Funding智能合约）
```go
//编译
const path=require('path');
const fs=require('fs');
const solc=require('solc');
//contract文件夹的名字
const srcpath = path.resolve(__dirname,'contract','Funding.sol');
//console.log(srcpath);读出地址
const source = fs.readFileSync(srcpath,'utf-8');
//console.log(source);打印出智能合约，读出来了
const result=solc.compile(source,1);
//console.log(result);
/*console.log(result.contracts[':Funding'].interface);
console.log(result.contracts[':FundingFactory'].interface);*/
//暴露信息 contracts方法
module.exports=result.contracts[':Funding'];
```
## 使用ganache-cl测试
### 获取的参数，以及先获得账户信息，Factory的部署
```go
const ganache=require('ganache-cli');
const Web3=require('web3');

let{interface,bytecode}=require('../compile');

const web3=new Web3(ganache.provider());
const assert=require('assert');

let contract;
let accounts;
let contractFactory;
beforeEach (async ()=>{
    accounts = await web3.eth.getAccounts();
    contract= await new web3.eth.Contract(JSON.parse(interface))
        .deploy({
                data:bytecode,
            
            }
        ).send({
            from:accounts[0],
            gas:'1000000'
        });

});
```
### 测试
```go
describe('测试彩票的智能合约',()=>{

   /* it('测试智能合约的部署情况',async ()=>{
       assert.ok(contract.options.address);
       console.log("部署的地址是"+contract.options.address);
    })*/
    it('测试FundingFactory智能合约的编译和部署',async ()=>{
        assert.ok(contract.options.address)
        console.log("address"+contract.options.address);
    });
    it('测试FundingFactory智能合约的deploy方法',async ()=>{
        await contract.methods.deploy('小夜灯',79,10000).send({
          from:accounts[0],
          gas:'1000000',
            //value:['小夜灯',79,10000]
        });
        //console.log((contract.methods));

        var address = await contract.methods.getAddr().call({

            //value:['小夜灯',79,10000]
        });

        console.log(address);
        interface = require('../compileFunding').interface;
       /* console.log(interface);*/
        contractFactory= await new web3.eth.Contract(JSON.parse(interface),address)
            /*.deploy({
                    data:bytecodeFunding,
                    // arguments:['小夜灯',79,10000,'0xEdb827b148DCBE9E14F03348475fA45650A7E1c5']
                }
            ).*//*send({
                from:accounts[1],
                gas:'1000000'
            });*/
           // console.log(contractFactory);
        //console.log((contractFactory.methods));
           // console.log(contractFactory.options.address);
            await contractFactory.methods.createRequest('点亮黑夜','10000',accounts[0]).send({
                from:accounts[0],
                gas:'1000000',
            });

    });

});
```
### 先使用Factory的deploy的方法部署Funding的智能合约，再通过getAddr方法获取地址
### 通过contractFactory= await new web3.eth.Contract(JSON.parse(interface),address)部署Factory重新实例化部署出来。最后为测试Funding合约中createRequest成功的方法案列。
