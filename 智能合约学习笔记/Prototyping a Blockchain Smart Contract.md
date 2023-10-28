## Notes on building and deploying a Smart Contract in Ethereum
W_elcome to Part 5 of the Product Manager’s Guide to the blockchain series! If you somehow landed on my publication for the first time, Welcome! I recommend you start from_[part 1](https://medium.com/the-time-of-the-product/the-product-managers-guide-to-the-blockchain-part-1-fb95dfb7af31)_, and then read_[part 2](https://medium.com/the-time-of-the-product/why-ethereum-when-we-already-have-bitcoins-blockchain-3359eb7e087e)_and_[part 3](http://part%203/)_and_[part 4](https://medium.com/the-time-of-the-product/heres-how-i-built-a-private-blockchain-network-and-you-can-too-62ca7db556c0)_before reading this post. However if you already know what you are doing, by all means feel free to read on._

I once sent a legally binding agreement as a pdf file to another party to read and approve. They promptly sent me a copy of the executed agreement, and I saved the executed agreement into a secure folder.
6 months later, we had some disagreement around a business issue and I pulled up the agreement to discuss resolution, only to find that an important clause in that agreement was forged. Before sending me the signed agreement, the other party modified a sentence in agreement that changed the meaning of a key clause entirely.
Of course, I was careless for not ensuring that the executed agreement was EXACTLY the same, word-to-word as the one I created — but when you are a startup or a small business trying to remove legal obstacles and get business going, you don’t think about verifying every single word in an executed agreement. That seemingly simple blunder cost me dearly.
I have to think that this happens a lot even today, but the good news is concepts such as blockchain Smart Contracts can totally change that.
# **Smart Contracts 101**
If you think about the blockchain as a distributed operating system of the future, then Smart Contracts are its killer app. Very often, Smart contracts are said to be akin to a blockchain based vending machine. Just as a vending machine takes in dollars/cents as inputs and is_configured_to dispense your choice of snack or drink — Smart contracts are a virtual vending machine of sorts. Instead of dollars and cents , Smart Contracts take cryptocurrency (ether in Ethereum’s case) as inputs and will execute some code based on some pre-configured rules as an output. These rules obviously can be defined by whoever is writing the contract.
Before we get deeper into smart contracts, it wouldn’t be a terrible idea to revisit what a plain old paper contract looks like

- _There are 2 or more parties involved_
- _The contract is offered by one party_
- _The contract is accepted by all remaining parties.Traditionally acceptance is indicated by some form of a signature_
- _Each party has to do something and receives something in exchange_
- _If any one party doesn’t do their job, other party can go to a higher authority — an arbitrator, or a judge for recourse._

Here is an escrow contract , as an example.

TCredits: escrow.com
The issue with this type of contracts is that the buyer and the seller have to trust a third party (in this case escrow.com). The buyer has to trust escrow.com with their funds, and the seller has to trust escrow.com to disburse funds to them as soon as the item has been verifiably delivered.
The age old problem of lots of people_trusting_each other — recipe forbad outcomes in business.
The cool thing about smart contracts is that they are_trustless_&_self-actualizing_.
All one needs to do is to code the rules of the contract and deploy on the blockchain — the contract is guaranteed to execute the terms agreed upon.
Additionally, the inherent property of smart contract residing on a distributed blockchain makes the contract transparent and tamper proof. As I experienced first hand, paper contracts can be tampered with even after both parties have agreed to terms.
# Smart Contracts = Trustless Contracts
With Smart contracts, an escrow contract can easily be set up — without any third party involvement, in a completely trustless fashion and that translates to powerful implications for the future.
As a rule of thumb, any industry or application that deals in paper based contractual and reporting documentation is subject to be disrupted by blockchain based Smart Contracts.
## Shipping and Cargo


80 percent of documentation in Shipping and like ‘bills of lading’ is still in paper form. Fraudulent shipping document costs the shipping industry billions in losses.[Forged paperwork and stolen cargo is the #1 problem in the shipping industry](http://www.maritime-executive.com/article/4-Cargo-Frauds-to-Watch-Out-For-2014-01-30). With Blockchain based smart contracts and IoT Sensors working in tandem it is possible to detect issues with cargo and inform a smart contract that can self-execute to refund a damaged party without the need for litigation or any human intervention.
Here is a[great article](https://dupress.deloitte.com/dup-us-en/focus/signals-for-strategists/using-blockchain-for-smart-contracts.html#endnote-2)from Delloitte Insights that talks about the range of applications — from smart health records to insurance to equipment warranties — that will be built due to the power of Smart Contracts and automatic implementation of terms of multiparty agreements

[source](https://dupress.deloitte.com/dup-us-en/focus/signals-for-strategists/using-blockchain-for-smart-contracts.html#endnote-2)
# Ok, enough theory — lets build a very simple contract and deploy it.
At a very high level, here is what’s involved in building & deploying a smart contract on a blockchain. (We will be building and deploying our contract on our private Ethereum chain.)

1. Finalize the terms and conditions of the contract, just like any regular paper/paperless contract.
2. The terms and conditions of the contract are then coded into a Ethereum high level language such as[Solidity](https://solidity.readthedocs.io/en/develop/)(syntax is similar to Javascript), compiled into_bytecode_format and then “_deployed_” on the Ethereum Blockchain. (We will look at these_buzzwords_in greater detail below)
3. Once deployed, the contract gets a public key address, that can be used to call the contract and trigger its execution.
4. Also, once a smart contract is deployed to the Ethereum blockchain, it cannot be changed even by the entity that created it.
## Here’s what we have so far
In the l[ast post](https://medium.com/the-time-of-the-product/heres-how-i-built-a-private-blockchain-network-and-you-can-too-62ca7db556c0), we built our own ethereum blockchain and then created a private network with a single node to share this blockchain. We also created an account for this node, and then mined some ether into this account to do_interesting things_on our private blockchain network.Well, the time to do interesting things has come :)
We will now use this account (lets call it Abhi’s account) to deploy a smart contract into our private blockchain. Just so we can focus on the mechanics of deployment our simple contract will do just one thing, — extend a greeting every time somebody calls the contract.
Once the mechanics are out of the way, you can always create custom contracts for whatever your use case is.
By the way, this is a derivative of the[Hello world contract](https://www.ethereum.org/greeter)from Ethereum’s documentation.
Before we move forward, if you have not already created a private blockchain and a private network that shares it , please do so —[here’s how to do that.](https://medium.com/the-time-of-the-product/heres-how-i-built-a-private-blockchain-network-and-you-can-too-62ca7db556c0)
# There are basically just 4 Steps to create and deploy a smart contract to the Ethereum Blockchain
# 1. Start your private Ethereum network
Why do we need to connect to this private network? — Because we will need to access the account we created on this network in the previous post. We will use this account to deploy our Smart Contract.
Assuming you are on a mac, open your terminal and run this snippet.
_Please remember to modify the snippet below with the appropriate paths to your data directory_
geth — **identity** “yourIdentity” — **init** /path_to_folder/CustomGenesis.json — **datadir** /path_to_your_data_directory/data_directory
This is the same snippet we used to create our private blockchain in the[previous post](https://medium.com/the-time-of-the-product/heres-how-i-built-a-private-blockchain-network-and-you-can-too-62ca7db556c0). This essentially sets our pointer to the**CustomGenesis.json**file to ensure we are using the same blockchain we created.
Remember, every blockchain has a unique genesis file.
Next, restart your private network (with its pre-defined_network id_). Again, this_network id_will be unique to your network.
geth --**datadir** /_path_to_your_data_directory_/data_directory --**networkid** 9876
With the two snippets above, your private network should be up and running.
Next, open another terminal window and run the following command.
geth attach _/path_to_your_data_directory/YOUR_FOLDER_/geth.ipc
Assuming everything went well so far, you should see a javascript console.
This console is where we will write and deploy our smart contract to our private network!


javascript console
Alright, we are all set. Now time to write the actual smart contract.
## As we talked about earlier, Our (very) simple Smart Contract will do just one thing —_extend a greeting every time somebody calls the contract_.
_This following code snippet is a slight modification of_[ethereum’s tutorial on smart contracts](https://www.ethereum.org/greeter)_. While a very helpful tutorial, it can be pretty complicated to understand and implement for beginners — so I will try to simplify and deconstruct each line of code on a high level ._
pragma solidity ^0.4.0;**contract greeter {     address owner;**
**     string greeting;function greeter(string _greeting) public {**
**        greeting = _greeting;**
**        owner = msg.sender;**
**    }**
**    **
**    function kill() **
**     { if (msg.sender == owner) selfdestruct(owner);**
**     }    function greet() constant returns (string) **
**    {**
**        return greeting;**
**    }**} 
## What the code above means:
#1 we defined a variable called  **owner** of the type **address**. This **owner** variable will receive the address of the account that is creating the contract (which in this case is our account)#2 We defined another variable and named it **greeting** . This is a string variable. **greeting** will store our greeting to whoever calls this contract. #3 The **greeter function **does two things, it assigns values to the **owner** and **greeting** variables. When we create this contract, the **owner** variable will store our public key, and the **greeting** variable will store the greeting that we want to display when somebody calls our smart contract.  (e.g. "Hello! My name is Abhi")#3. The **kill () function** will help us clean up useless smart contracts from our private blockchain. Only the account that created a smart contract can kill it.#4. **greet()** is  main function of the smart contract that will return the value of the **greeting** variable to the entity invoking the smart contract
This contract is coded in[Solidity](http://solidity.readthedocs.io/en/develop/)which is a contract-oriented, high-level language similar to that of JavaScript. Solidity is designed to target the Ethereum Virtual Machine (EVM). (Read[Part 2](https://medium.com/the-time-of-the-product/product-managers-guide-to-blockchain-part-3-fb0cffbff7f8)to learn more about EVMs)
# 2. Go[here](https://remix.ethereum.org/#version=soljson-v0.4.17+commit.bdeb9e52.js)and type the contract code snippet in the Remix editor.
[Remix](https://remix.ethereum.org/#version=soljson-v0.4.17+commit.bdeb9e52.js)is the tool that helps us write and compile smart contracts written in Solidity to bytecode (_computer generated gibberish_) that Ethereum Virtual Machine can understand and process.

remix- this is a solidity editor and compiler
Click the “**Details**” button under the Compile menu above and you should see a popup (that will pretty much give you all the code that you need)

# 3. copy the code from the WEB3DEPLOY section.
This is code that we will use to deploy our smart contract to our private Ethereum blockchain network. It should look something like this.

…..and all that code does is**3 things**.
## Thing #1. It sets our greeting message
var **_greeting** = "Hello World! This is Abhi!" ; /* replace this with whatever greeting you want your Smart Contract to return */
## Thing #2. It creates a new contract instance with all its methods and events defined in its[json](https://web3js.readthedocs.io/en/1.0/glossary.html#glossary-json-interface)format
var **browser_greeter_sol_greeterContract** = web3.eth.contract([{"constant":false,"inputs":[],"name":"kill","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"greet","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[{"name":"_greeting","type":"string"}],"payable":false,"stateMutability":"nonpayable","type":"constructor"}]);
This JSON format definition of the smart contract is also called the contract’s Application Binary Interface or**ABI.**We’ll return to the ABI soon.
## Thing #3. It sets the owner of the contract , the bytecode of the contract to be deployed & the cost of deploying this contract to the Ethereum blockchain
(You need ether to do pretty much anything on the Ethereum blockchain, remember?)
var **browser_greeter_sol_greeter** = **browser_greeter_sol_greeterContract.new**( _greeting, 
{**from**: web3.eth.accounts[0], 
 **data**:'0x6060604052341561000f57600080fd5b6040516103a03803806103a0833981016040528080518201919050508060019080519060200190610041929190610088565b50336000806101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff1602179055505061012d565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106100c957805160ff19168380011785556100f7565b828001600101855582156100f7579182015b828111156100f65782518255916020019190600101906100db565b5b5090506101049190610108565b5090565b61012a91905b8082111561012657600081600090555060010161010e565b5090565b90565b6102648061013c6000396000f30060606040526000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806341c0e1b514610048578063cfae32171461005d57600080fd5b341561005357600080fd5b61005b6100eb565b005b341561006857600080fd5b61007061017c565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156100b0578082015181840152602081019050610095565b50505050905090810190601f1680156100dd5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b6000809054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff16141561017a576000809054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16ff5b565b610184610224565b60018054600181600116156101000203166002900480601f01602080910402602001604051908101604052809291908181526020018280546001816001161561010002031660029004801561021a5780601f106101ef5761010080835404028352916020019161021a565b820191906000526020600020905b8154815290600101906020018083116101fd57829003601f168201915b5050505050905090565b6020604051908101604052806000815250905600a165627a7a72305820c16d0d07cad4b5e82b9e94f4c8ed7e1bdbd0d52cda44575374e0b136d94f99fa0029',
gas: '4700000'},function (e, contract)
{  
    console.log(e, contract);    
     if (typeof contract.address !== 'undefined') 
         { console.log('Contract mined! address: ' +contract.address + ' transactionHash: ' + contract.transactionHash);}  
})

Before we move on, the**data**attribute in the code above is worth talking about.
The gibberish this attribute holds is the_bytecode_of the smart contract — and this bytecode is what will be deployed to the Ethereum blockchain.
All in all, The key thing to understand is that the Solidity complier takes the contract code in Solidity that the EVM cannot understand and turns it into bytecode that the EVM can understand.
Okay now that we have this code, let us return to our terminal with Geth Javascript console running and ….
# 3. Deploy the code copied from the WEB3DEPLOY section into geth terminal
When you run these code snippets on the geth terminal, you are basically setting up an Ethereum network_transaction_that is requesting all the nodes in the Ethereum network to deploy our smart contract code on the blockchain.
At this time go ahead and run the code from the WEB3DEPLOY section into geth terminal.

(my terminal window, after running code snippets #1 & #2 — ignore the ‘undefined’ prompts)
## Important:
If the code execution fails, you might have to_unlock_our Ethereum account before you can successfully deploy this code, since it needs ether from the account that is deploying the contract. This is to pay for cost of the gas needed to deploy the contract on the blockchain.
you can unlock your account by typing :

web3.eth.accounts[0] simply fetches the public key of your first account — in case you have multiple accounts. (Sidenote: To see how many accounts you have simply type **personal.listAccounts **in the Javascript console.)
Enter your passphrase & you are all set.
Now, go ahead and run the code again and you should get no errors.

# 4. Start Mining
For a smart contract to be deployed on the Ethereum blockchain, miners in the network must mine this block that contains our_smart contract creating_transactions. This would typically take a while , since the transaction needs to be propagated through the network and miners need to validate the blocks.
But here is the good news, since we are deploying our smart contract to our_private_blockchain network, where the only node and miner is us — we can simply start mining and within seconds mine the transaction block that contains our smart contract.
To start mining type:
miner.start()
And you’ll see within a few seconds the contract is mined, which basically means that smart contract has been deployed to our private blockchain.

Contract is mined!
Also, notice that our smart contract has got an address on our private network now — (**0x9f8cedf1f93e46fac74cb9415db8bbec85f239b4**)!
We can now use this address to call our smart contract!
# Calling our Smart Contract
Now that our smart contract is deployed on our private Ethereum Blockchain, we can invoke our smart contract! There are only two things one needs:

1. **The ABI definition of the Smart Contract**
2. **The ddress of the Smart Contract**

**Application Binary Interface**or ABI definition of a smart contract is the list of the contract’s functions and arguments in JSON format.
If an account wants to use a smart contract’s function , it uses the smart contract’s**ABI**to create a_bytecode_which along with a smart contract’s_address_on the network helps anyone access the functions of that particular smart contract.
The ABI definition of our smart contract can be found from code snippet from the WEB3DEPLOY section .
var browser_greeter_sol_greeterContract = web3.eth.contract(**_[{"constant":false,"inputs":[],"name":"kill","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"greet","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[{"name":"_greeting","type":"string"}],"payable":false,"stateMutability":"nonpayable","type":"constructor"}]_**);(ABI in **_bold italics)_**
..alternatively, the ABI can also be accessed via the[Remix](https://remix.ethereum.org/#version=soljson-v0.4.17+commit.bdeb9e52.js)tool

Ok, so lets call the smart contract. Type these two snippets in your geth javascript console.
var myContract = web3.eth.contract(**_[{"constant":false,"inputs":[],"name":"kill","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"greet","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[{"name":"_greeting","type":"string"}],"payable":false,"stateMutability":"nonpayable","type":"constructor"}]_**); myContract.at("**0x9f8cedf1f93e46fac74cb9415db8bbec85f239b4**").greet();

BOOM! The smart contract should return your greeting !
# Congratulations!
With that you have deployed your very first smart contract to your own private Ethereum network!
Obviously, real world smart contracts are would be much more sophisticated and meaningful, involving complicated scenarios that is stuff of lawyers — but the deployment steps for any contract would pretty much remain the same.
Also, If you add more nodes to your network, each node can call this smart contract — all they would need is the**ABI definition**of the contract and it’s**address**!
A really cool next step would be to ask your friends to join your private blockchain network by becoming nodes — or to create another node yourself[using the steps mentioned in part 4](https://medium.com/the-time-of-the-product/heres-how-i-built-a-private-blockchain-network-and-you-can-too-62ca7db556c0).
The 2 things that any new node needs to ensure before they can connect to your private Ethereum networkare that they connect to the same_genesis file ,_and they use same_network id_as your private Ethereum Network.
Good Luck, And Thanks for reading!
## If you found the post helpful, please recommend it to others by clapping for this post ! If you have insights or comments, I would love to hear from you . You can also reach out to me directly on[twitter](https://twitter.com/ChakrVyuh).
[Abhishek Chakravarty](https://chakrvyuh.medium.com/?source=post_sidebar--------------------------post_sidebar-----------)
👋[https://twitter.com/ChakrVyuh](https://twitter.com/ChakrVyuh)
原po： [https://chakrvyuh.medium.com/prototyping-a-blockchain-smart-contract-78877464e38e](https://chakrvyuh.medium.com/prototyping-a-blockchain-smart-contract-78877464e38e)
[
](https://policy.medium.com/medium-terms-of-service-9db0094a1e0f?source=post_page-----78877464e38e--------------------------------)
