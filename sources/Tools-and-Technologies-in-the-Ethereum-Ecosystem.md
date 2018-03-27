# Tools and Technologies in the Ethereum Ecosystem

![](https://i.imgur.com/Jjkpwfr.png)

If you are a developer new to Ethereum/blockchain, it is possible you are overwhelmed (at least I was) trying to understand all the tools and technologies in the Ethereum ecosystem. So I decided to briefly describe the various components you come across frequently while starting to learn Ethereum. Hopefully this will help you get a big picture of the Ethereum ecosystem and how all the pieces fit together.

Ethereum is a smart contract blockchain on which you can build decentralized applications (called smart contracts). If you are a technologist, this white paper is worth reading: [https://github.com/ethereum/wiki/wiki/White-Paper](https://github.com/ethereum/wiki/wiki/White-Paper).

If you have built web applications before, I wrote a [post](https://medium.com/@mvmurthy/ethereum-for-web-developers-890be23d1d0c#.8wo4bi611) comparing Ethereum blockchain and web application architecture which might help understand Ethereum at a high level.

Geth is the official client software provided by the [Ethereum Foundation](http://ethereum.org/). It is written in the Go programming language. This software packages a few components which is worth understanding:

When you start this client daemon, it connects to other clients (also called nodes) in the network and downloads a copy of the blockchain. It will constantly communicate with other nodes to keep it’s copy of the blockchain up to date. It also has the ability to mine blocks and add transactions to the blockchain, validate the transactions in the block and also execute the transactions. It also acts as a server by exposing APIs you can interact with through RPC.

![](https://i.imgur.com/eqExYxM.png)

2. [geth console](https://github.com/ethereum/go-ethereum/wiki/geth)

This is a command line tool which lets you connect to your running node and perform various actions like create and manage accounts, query the blockchain, sign and submit transactions to the blockchain and so on.

3. Mist Browser

This is a desktop application used to communicate with your node. Anything you can do using the geth console can be accomplished through this Graphical User Interface.

Parity is another good implementation of the Ethereum protocol and is written in the Rust programming language. It is an unofficial client and is maintained by a company called [Parity Inc](https://parity.io/). Any one can implement the client software and join the Ethereum network. You can follow the specs in this [yellow paper](https://ethereum.github.io/yellowpaper/paper.pdf) to implement your own client!

![](https://i.imgur.com/xQGGQr2.png)

Just like you have geth, mist browser and so on to communicate with the ethereum node, there is also a javascript library called Web3.js which can be used to interact with a node. Since it is a javascript library, you can use it to build web based dapps.

![](https://i.imgur.com/c8Y7lNd.png)

Solidity is the most popular programming language used to write smart contracts to run on the Ethereum blockchain. It is a high level language which when compiled gets converted to EVM (Ethereum Virtual Machine) byte code. This is very similar to the world of Java where there are JVM languages like Scala, Groovy, Clojure, JRuby etc. All these on compilation generate byte code which run in the JVM (Java Virtual Machine). You can also create a language like Solidity as long as you follow the specs and your language compiles down to the valid EVM byte code!

There is a also very nice browser based IDE where you can write contracts, compile and deploy to the blockchain here: [http://remix.ethereum.org/](http://remix.ethereum.org/)

Just like you have frameworks for web application development such as Ruby on Rails, Python/Django etc, Truffle and Embark are the two most popular frameworks used to develop dapps. They abstract away lot of the complexities of compiling and deploying your contract on the blockchain.

If you are new to Ethereum dapp development, I wrote a series of guided tutorials to get started [here](https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2), [here](https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-2-30b3d335aa1f) and [here](https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-3-331c2712c9df).

If you hang out in the Ethereum community for more than a week, you will inevitably come across Metamask. As of this writing, it is a chrome plugin used to interact with the Ethereum node. It is unrealistic for everyone in the world to run a node to interact with the blockchain. So, the folks at Metamask host a number of nodes so you don’t have to. All you have to do is install Metamask and it automatically connects to their nodes.

![](https://i.imgur.com/xQGGQr2.png)

Ethereum Naming System is the DNS for the Ethereum world. Just like you map an IP address to a human readable name, you can map any Ethereum contract or wallet address to a human readable name.

Ex: 146.115.22.177 → google.com. Instead of typing the ip address in your browser, you type google.com which resolves to that IP address

Ex: 0x80C013d980aB049471c88E1603b8b4a60E03295C is my wallet address. If you are in the mood to send me some Ether, you don’t have to memorize this address. Once ENS launches, I will probably map it to mvmurthy.eth and you can use that to send me money easily :).

The blockchain is good to store small amounts of data. What if you want to store a patient record, a sale deed or some large file which needs to be publicly timestamped? It is expensive and also not scalable to store a blob in the blockchain. Swarm is used to solve this problem. Swarm is a decentralized content storage and distribution service. You can think of it as a CDN but instead of the entire CDN hosted on one company’s servers, it is distributed on computers across the internet. Just like you run an Ethereum node, you run a swarm node to connect to the swarm network.

When you deploy an Ethereum contract on to the blockchain, you get a deployed address and JSON interface of the [ABI](https://github.com/ethereum/wiki/wiki/Ethereum-Contract-ABI) (The contract interface similar to API). When you want someone to use your contract, you have to give them the deployed address and the ABI. In the future, the ABI will be stored on Swarm so anyone can look up the ABI just by looking at the Ethereum address.

IPFS (Inter Planetary File System) is conceptually exactly similar to Swarm. It is a decentralized storage system. It is not related to Ethereum directly but can be integrated with Ethereum.

You can read about the differences between Swarm and IPFS here: [https://github.com/ethersphere/go-ethereum/wiki/IPFS-&-SWARM](https://github.com/ethersphere/go-ethereum/wiki/IPFS-&amp;-SWARM)

You don’t hear a lot about Whisper but is an interesting technology in the Ethereum ecosystem. It is a communication protocol for Dapps to interact with one another. You can read more about it here: [https://github.com/ethereum/wiki/wiki/Whisper](https://github.com/ethereum/wiki/wiki/Whisper)

Below is an attempt to put all the pieces together:

![](https://i.imgur.com/H48W22N.png)

Hope this helps you get a 10,000 foot view of the Ethereum ecosystem and can now delve into each component and understand it better.

If you are interested in learning more about Ethereum development, you can sign up [here](http://zastrin.com/).

[Tools and Technologies in the Ethereum Ecosystem](https://medium.com/blockchannel/tools-and-technologies-in-the-ethereum-ecosystem-e5b7e5060eb9)