在 [我（本文作者）过去的文章中](https://medium.com/loom-network/why-you-should-learn-to-build-blockchain-apps-be9a92e8d08e), 我们已经说明了你为什么应该学习创建区块链分布式应用。

在这篇文章中，我们将讨论你怎么将他们货币化。

在讨论具体的DApp案例之前，让我们试着回答一个流行的问题：
> 传统app怎么赚钱？

简单说，广告商会支付给内容提供者和技术公司（你，其他开发者）钱，让他们把广告推到顾客（你的用户）面前。顾客依次被广告影响（不管他们是不是这么认为），然后在广告商的产品上花钱。

在过去的APP市场，有Lite，Regular和Pro版本的app。用户会试用提供给他们的产品，如果他们喜欢，则会购买完整版本的应用程序。

![](https://i.imgur.com/SUZR9rP.png)


使用该商业模式的公司，诸如Spotify，Slack或Onedrive等，通过购买付费订阅的用户来获得收入。


免费增值模式的其他例子还包括，允许用真实货币购买游戏内物品的游戏类应用程序。

免费游戏MMORPG利用了所谓的“免费限制”方法。魔兽世界中的免费玩家，最高等级之允许为20级。其他游戏则对你可以探索的区域进行限制。这类游戏的最佳内容是为“付费玩家”游戏玩家保留的。

> 考虑到上述情况，当DApp开发人员寻求将自己的DApp货币化时，可以着眼于很多容易解决的问题。

正如[前一篇文章](https://medium.com/loom-network/why-you-should-learn-to-build-blockchain-apps-be9a92e8d08e)中所讨论的, 你始终可以通过由令牌支持的众包来引导你的项目。

在这种情况下，你需要定义你的令牌[ [1](https://medium.com/@mrdavey/good-discussion-and-question-2446e3827de2) ]的需求:

* 你的dapp的核心功能 ( [Golem](https://golem.network/), [Aragon](https://aragon.one/), [Request](https://request.network/) )
* 提供你的网络的访问权( [BAT](https://basicattentiontoken.org/), [Bloom](https://hellobloom.io/) )
* 将产品利润分配给代币持有者（TenX，Numerai）请注意，在这种情况下，你需要注意法规和KYC合规性，具体取决于你的代币是否被视为证券。

Cryptokitties从每次成功拍卖中收取3.75％的费用。这被证明是一个[非常有利可图的收入模式](https://medium.com/@codetractio/a-look-into-cryptokitties-revenue-model-6466b705a998)。

![](https://i.imgur.com/Z4HZHLa.png)

上周CK（Cryptokitties）的使用量致使交易费用陡升到800 ETH。 来源: [DappRadar.com](https://dappradar.com/)

举个一般的例子:

1. **A**通过你的服务从**B**买东西
2. 支付费用的**Y%**给服务提供商（你自己）  
3. (100- **Y** )% 支付给 **B**。
这里有一个警告. 
如果你向终端用户收取“不公平”的服务费用，那么终端用户将最后会复制你的智能合约并发布一个较低费用甚至免费的版本（考虑你的合同已经过验证且开放源代码的情况，而这也是人们对以太坊DApps通常期望的）.

> 找出合适的价格来向用户收费是关键；不过这篇文章里我们不会介绍定价模型。

从前面讨论过的免费增值模式中激励自己, 并拿我们在[CryptoZombies](https://cryptozombies.io/)中构建的游戏作示例，设想一下:

假设你的CryptoZombie（加密僵尸军团）需要10次胜利才能升级，而且随着等级的提高越来越难。

从第10级到第11级的升级比从第1级升级到第2级要困难得多。 用户需要花费更多的精力来升级他们的CryptoZombie（加密僵尸军团）。

![](https://i.imgur.com/z7Rewob.png)

收益递减规律

在这里你可以实现一个功能，它允许僵尸“跳过”这个努力并且直接升级，作为回报，用户需要支付一些数量的以太。

这样一来，免费玩家仍然能够获得最终游戏结果，但愿意额外付费的玩家可跳过这个努力的过程。

同样的情况也适用于重置僵尸的冷却时间。 僵尸通常需要在再次战斗之前等待`冷却时间`秒，但我们可以做到让用户支付一小笔费用来跳过冷却时间。

在这里你有很多不同的方式来用DApps获利，我们将在本文的第2部分讨论具体实现的代码。

你可以添加订阅或购买会员功能到你的合同中，这样某些功能只能被订阅者或高级会员调用。

订阅服务的持续方法可以是:

* **基于时间长度:** 用户被允许调用一个函数，直到X时间过去，例如，他们可以支付1个月的访问权限。
* **基于使用次数:** 用户被允许调用X次函数。你可以在[维基百科](https://en.wikipedia.org/wiki/Subscription_business_model)上阅读更多关于订阅的模型。


同样的，如何实现这些特定代码的示例将在本文章的第二部分中介绍。


考虑到我们正在谈论关于DApp本身的广告，这是一种不太流行的方法。[ThousandEtherHomepage](http://thousandetherhomepage.com/)就是如此。你可以在合约中付费认领一些阵列，这些阵列会在DApp的前端以像素显示出来。就像你在下图看到的，这些像素已被一些项目（包括其他类型）用于其品牌宣传。

![](https://i.imgur.com/fYNqkJi.png)


如果上述任何内容听起来都太麻烦了，你可以随时在你的服务/ DApp中加上你加密货币的地址，接受慷慨者的捐助。

你也可以将[eth-button](https://eth-button.github.io/eth-button/)添加到你的网页上以进行Metamask集成。

![](https://i.imgur.com/hS3Kocb.png)

[eth-button.github.io/eth-button](http://eth-button.github.io/eth-button)

第一部分是更强调理论。第2部分将包含实现上述货币化想法的代码。

敬请关注！

![](https://i.imgur.com/eTXoU5g.gifv)

对DApp开发感兴趣？查看我们完全免费的课程，了解如何开始 ⬆

[原文链接](https://medium.com/loom-network/6-ways-to-monetize-your-ethereum-dapps-part-1-28e9bb18f87e)
