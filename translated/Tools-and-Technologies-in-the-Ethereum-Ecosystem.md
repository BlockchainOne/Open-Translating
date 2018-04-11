# 以太坊生态中的工具与技术

![](https://i.imgur.com/Jjkpwfr.png)

如果你是一个以太坊或区块链开发者新手，那么很可能你正有点不知所措地（至少我是）试图去了解以太坊生态中的所有工具与技术。所以我决定简单介绍一下你在开始学习以太坊时会经常遇到的各种各样的组件。希望这将有助于你对整个以太坊生态，以及生态中的每一部分是如何联系在一起的有一个全局观。

## 1. [以太坊](http://ethereum.org/)
***

以太坊是一个智能合约区块链平台，在上面你可以创建去中心化的应用程序（也被称为智能合约 【译注：称为 Dapps 更合适】）。 如果您是技术专家，那么这个白皮书值得研读：
[https://github.com/ethereum/wiki/wiki/White-Paper](https://github.com/ethereum/wiki/wiki/White-Paper).

如果你之前有创建过 web 应用程序，我有写过一篇[文章](https://medium.com/@mvmurthy/ethereum-for-web-developers-890be23d1d0c#.8wo4bi611)去比较以太坊区块链和 web 应用程序架构，这可能有助于你更深入地了解以太坊。

## 2. [Geth](https://github.com/ethereum/go-ethereum)
***

Geth 是由[以太坊基金会](http://ethereum.org/)提供的官方客户端软件。它是用 Go 编程语言编写的。 这个软件包含了下面几个值得了解的组件：

### 客户端守护进程
***

当您启动这个客户端守护程序时，它会连接到网络中的其它客户端（也被称为节点）并下载一个区块链拷贝。 它将不断与其他节点进行通信，以使其区块拷贝保持更新到最新状态。 它还具有挖掘区块并将交易添加到区块链，验证并执行区块中的交易的能力。 它还可以充当 API 服务器，您可以通过 RPC 方式来其访问其暴露的 API 接口。

![](https://i.imgur.com/eqExYxM.png)

### [geth 终端](https://github.com/ethereum/go-ethereum/wiki/geth)
***

这是一个命令行工具，它可以让你连接到正在运行的节点，并执行像创建和管理帐户、查询区块链、签署并提交交易给区块链等各种各样的操作。

### Mist 浏览器
***

这是一个用于与你的节点通信的桌面应用程序。 任何你能使用 geth 终端完成的操作都可以通过此图形用户界面来完成。

## 3. [Parity](https://github.com/paritytech/parity)
***

Parity， 用 Rust 语言编写， 是另一个对以太坊协议很好的实现。 这是一个由一家名为 [Parity Inc](https://parity.io/) 的公司维护的非官方客户端。任何人都可以实现这样的客户端软件并加入以太坊网络。 你可以按照这本[黄皮书](https://ethereum.github.io/yellowpaper/paper.pdf) 中的规范来实现自己的客户端！

![](https://i.imgur.com/xQGGQr2.png)

## 4. [Web3.js](https://github.com/ethereum/web3.js/)
***

就如同你用 geth，mist 浏览器等来与以太坊节点进行通信一样，还有一个名为 web3.js 的 javascript 库，也可以用来与一个节点进行交互。 由于它是一个 javaScript 库，你可以使用它来构建基于 web 的去中心化应用 (dapps)。

![](https://i.imgur.com/c8Y7lNd.png)

## 5. [Solidity](https://solidity.readthedocs.io/en/develop/)
***

Solidity 是用于编写在以太坊区块链上运行的智能合约最流行的编程语言。 它是一种编译时转换为 EVM （以太坊虚拟机）字节码的高级语言。 这与具有诸如 Scala，Groovy，Clojure，JRuby 等 JVM 语言的 java 世界非常相似。所有这些 JVM 语言都可以在编译时生成可在 JVM（Java虚拟机）中运行的字节码。 只要遵循规范，你也可以创建一个像 Solidity 这样的语言，编译时转换为有效的 EVM 字节码！

还有一个非常棒的基于浏览器的 IDE，在这里你可以编写智能合约并将其编译部署到区块链上: [http://remix.ethereum.org/](http://remix.ethereum.org/)。

## 6. [Truffle](http://truffleframework.com/)/[Embark](https://github.com/iurimatias/embark-framework)
***

就像你有 Ruby on Rails，Python / Django 等 web 框架去做应用程序开发一样，Truffle 和 Embark 是用于开发以太坊去中心化应用（dapps）的两个最流行的框架。 它们将在区块链上编译和部署合约的许多复杂的东西都抽象化了。

如果你是个以太坊去中心化应用（dapp）开发新手，在[这里](https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2)，[这里](https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-2-30b3d335aa1f)还有[这里](https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-3-331c2712c9df)我已经为你写了一系列入门教程。

## 7. [Metamask](https://metamask.io/)
***

如果在以太坊社区晃荡超过一周，你一定会遇到 Metamask。它目前是一个用于与以太坊节点进行交互的 chrome 浏览器插件。 让世界上的每个人都运行一个节点与区块链交互是不切实际的。 所以，写 Metamask 的那帮家伙们自己运行了一定数量的节点，这样你就不需要这么做了。 所有你需要做的就是装上 Metamask ，然后它就会自动连接到他们的节点了。

![](https://i.imgur.com/xQGGQr2.png)

## 8. [ENS](http://ens.domains/)
***

以太坊域名系统（Ethereum Naming System）是以太坊世界的 DNS。 就像你将 IP 地址映射到方便人们读取的名称一样，你可以将任何以太坊合约或钱包地址映射到一个易读的名称。

例如: 146.115.22.177 → google.com. 您不需要在浏览器中输入 IP地址，输入 google.com 就好了，它会被解析到相应的 IP 地址。

例如: 0x80C013d980aB049471c88E1603b8b4a60E03295C 是我的钱包地址。如果你想转给我一些以太币，你并不需要记住这个地址。 一旦 ENS 启动，我可能会将其映射到 mvmurthy.eth，然后你就可以很轻松地用它给我转钱了 :)。

## 9. [Swarm](http://swarm-gateways.net/bzz:/theswarm.eth/)
***

区块链能很好地存储少量的数据。 如果你想要存储病历，销售合同或需要公开时间戳的大型文件该怎么办呢？在区块链中存储大块数据是昂贵并且不可扩展的。 Swarm 被用来解决这个问题。 Swarm 是一个去中心化的内容存储和分发服务。 您可以将它视为 CDN，但它并不是在一家公司的服务器上托管的所有 CDN，而是通过互联网在计算机上分发。 你可以像运行一个以太坊节点一样，去运行一个 Swarm 节点并连接到 Swarm 网络上。

当你将一个以太坊合约部署到区块链时，您会获得一个部署地址和一个 [ABI](https://github.com/ethereum/wiki/wiki/Ethereum-Contract-ABI) JSON 接口（类似于 API 的合约接口）。当你希望有人使用您的合约时，你需要提供部署地址和 ABI 。 将来，ABI 会被存储在 Swarm 中，以便每个人都可以通过查看以太坊地址来查找 ABI。

## 10. [IPFS](https://ipfs.io/)
***

IPFS（星际文件系统）在概念上与 Swarm 非常相似。 它是一个去中心化的存储系统。 与以太坊没有直接关联，但可以与以太坊集成。

你可以在这里查看 Swarm 和 IPFS 之间的不同: [https://github.com/ethersphere/go-ethereum/wiki/IPFS-&-SWARM](https://github.com/ethersphere/go-ethereum/wiki/IPFS-&amp;-SWARM)

## 11. [Whisper](https://github.com/ethereum/wiki/wiki/Whisper)
***

你可能没怎么听到过 Whisper，不过它也是在以太坊生态系统中一项有趣的技术。 它是 Dapps 之间交互的通信协议。 你可以在这里看到关于它的更多内容: [https://github.com/ethereum/wiki/wiki/Whisper](https://github.com/ethereum/wiki/wiki/Whisper)

下图尝试把所有这些东西放在一起：

![](https://i.imgur.com/H48W22N.png)

希望这能让你对以太坊生态系统有一个概括性的了解，并从现在开始能对每个相关组件进行更深入的研究和理解。

如果你有兴趣学习更多关于以太坊开发的知识，欢迎在[这里](http://zastrin.com/)注册。

via:[Tools and Technologies in the Ethereum Ecosystem](https://medium.com/blockchannel/tools-and-technologies-in-the-ethereum-ecosystem-e5b7e5060eb9)

作者: [Mahesh Murthy](https://medium.com/@mvmurthy?source=post_header_lockup)
译者: [Ashton](https://github.com/cdljsj)
校对: [dbarobin](https://github.com/dbarobin)
