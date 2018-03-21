在 [我（本文作者）过去的文章中](https://medium.com/loom-network/why-you-should-learn-to-build-blockchain-apps-be9a92e8d08e), 我们已经说明了你为什么应该学习创建区块链分布式应用。

在这篇文章中，我们将讨论你怎么货币化他们。

在投入到这种特殊的Dapp案例之前，让我们普及一个问题：
> 传统app怎么赚钱？

简单说，广告商会支付给内容提供者和技术公司（你，其他开发者）钱，让他们把广告推到顾客（你的用户）面前。顾客轮流被广告影响（即使他们认为他们不是），导致顾客在广告上的产品上花钱。

在过去的APP市场，有Lite，Regular和Pro版本的app。用户会试用该产品提供的产品，如果他们喜欢，则会购买完整版本的应用程序。

![](https://i.imgur.com/SUZR9rP.png)


使用该商业模式，诸如Spotify，Slack或Onedrive等公司可以为其用户购买付费订阅的用户获得收入。


免费增值模式的其他例子包括允许购买真实货币的游戏内物品的游戏应用程序。

免费游戏MMORPG利用了所谓的“免费限制”。作为魔兽世界中的免费玩家，最高允许等级为20级。其他游戏对您可以探索的区域有限制。这类游戏的最佳内容是为“付费玩家”游戏玩家保留的。

> 考虑到上述情况，当DApp开发人员寻求将其DApp货币化时，可能会遇到很多低级问题。

正如[前一篇文章](https://medium.com/loom-network/why-you-should-learn-to-build-blockchain-apps-be9a92e8d08e)中所讨论的, 你始终可以通过由令牌支持的众包来引导您的项目。

在这种情况下，您需要定义您的令牌[ [1](https://medium.com/@mrdavey/good-discussion-and-question-2446e3827de2) ]的需求:

* 你的dapp的核心功能 ( [Golem](https://golem.network/), [Aragon](https://aragon.one/), [Request](https://request.network/) )
* 提供访问你的网络( [BAT](https://basicattentiontoken.org/), [Bloom](https://hellobloom.io/) )
* 将产品利润分配给代币持有者（TenX，Numerai）请注意，在这种情况下，您需要注意法规和KYC合规性，具体取决于你的代币是否被视为安全性。

Cryptokitties为每次成功拍卖收取3.75％的费用。这被证明是一个[非常有利可图的收入模式](https://medium.com/@codetractio/a-look-into-cryptokitties-revenue-model-6466b705a998)。

![](https://i.imgur.com/Z4HZHLa.png)

上周CK（Cryptokitties）的使用量在交易费用中达到800 ETH。 来源: [DappRadar.com](https://dappradar.com/)

举一个一般的例子:

1. **A**使用你的服务从**B**买些东西
2. 支付**Y%**给服务提供商（你自己）   
3. (100- **Y** )% 支付给 **B**。
这里有一个警告. 
如果您向最终用户收取“不公平”的服务费用，那么最终用户将最终复制您的智能合同并以较低费用或免费费用发布其版本（因为您的合同已经过验证且开放源代码，这通常是以太坊DApps的预期）.

> 找到合适的数量来为用户收费是关键。但是我们不会在这篇文章中介绍定价模型

从前面讨论过的免费增值模式激励自己, 
并通过使用我们在[CryptoZombies](https://cryptozombies.io/)中构建的游戏作为示例，请考虑以下内容:

假设你的CryptoZombie（僵尸军团）需要10次胜利才能升级，而且随着等级的提高越来越难。

从第10级到第11级的升级比从第1级升级到第2级要困难得多。 用户需要花费更多的精力来升级他们的CryptoZombie（僵尸军团）。

![](https://i.imgur.com/z7Rewob.png)

收益递减规律

在这里你可以实现一个功能，它允许僵尸“跳过”这个努力并且直接升级，并且作为回报，用户需要支付一些数量的以太。

这样一来，免费玩牌的玩家仍然能够获得最终游戏结果，但愿意支付溢价的玩家可以跳过这一努力。

同样的情况也适用于重置僵尸的冷却时间。 僵尸通常需要在再次战斗之前等待`冷却时间`秒，但我们可以做到这一点，因此用户可以支付一小笔费用并跳过冷却时间。

在这里有很多不同的方式可以使DApps获利，我们将在本文的第2部分讨论特定的代码实现。

您可以添加订阅或成员资格功能到您的合同，以使某些功能只能由订阅者或高级会员进行调用。

订阅的时间可能是:

* **基于时间:** 用户被允许调用一个函数，直到X时间过去，例如，他们可以支付1个月的访问权限。
* **基于使用:** 用户被允许调用X次函数。您可以在[维基百科](https://en.wikipedia.org/wiki/Subscription_business_model)上阅读更多关于订阅模型。


再次，我们将看看如何在本文的第2部分中实现这些特定的代码示例。


考虑到我们正在谈论关于DApp本身的广告，这是一种不太流行的方法。[ThousandEtherHomepage](http://thousandetherhomepage.com/)就是这么做的。您可以在合约中声明若干阵列插槽，这些阵列插槽由DApp前端的像素表示。如下图所示，这些像素已被项目（其中包括）用于宣传其品牌。

![](https://i.imgur.com/fYNqkJi.png)


如果上述任何内容听起来都太麻烦了，您可以随时在您的服务/ DApp中为您的慷慨捐助者添加您的加密货币地址。

您也可以将[eth-button](https://eth-button.github.io/eth-button/)添加到您的网页以进行Metamask集成。

![](https://i.imgur.com/hS3Kocb.png)

[eth-button.github.io/eth-button](http://eth-button.github.io/eth-button)

第一部分是一个更理论的方法。第2部分将包括基于上述一些货币化概念的代码实现。

敬请关注！

![](https://i.imgur.com/eTXoU5g.gifv)

对DApp开发感兴趣？查看我们完全免费的课程，了解如何开始 ⬆

[原文链接](https://medium.com/loom-network/6-ways-to-monetize-your-ethereum-dapps-part-1-28e9bb18f87e)
