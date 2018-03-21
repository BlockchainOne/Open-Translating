# 让你的以太坊 DApps 盈利的6种方法（2）

在这个包含两篇文章的系列的[第一部分](https://medium.com/loom-network/6-ways-to-monetize-your-ethereum-dapps-part-1-28e9bb18f87e?source=user_profile---------4-------------------)
我们已经有了让你的以太坊 Dapps 盈利理论上的方法。在这部分，我们将会看一些代码示例，向你展示如何用 Solidity 来真正实现它们。

## 提取资金

首先，需要一个允许提取资金到所有者地址的函数。这就和下面的图中一样简单：
![](https://i.imgur.com/yYJPN1W.png)

这个函数将会转移调用合约的账目到 `owner` （使用最流行的 `onlyOwner` 修饰符 ）的地址。如果你不熟悉上面的关键字是如何工作的，你也许想要暂停阅读，在完成我们在 [CryptoZombies.io](https://cryptozombies.io/) 的课程之后再继续。

** 声明：** 接下来所有的例子都已经被简化，仅用来展示如何实现讨论到的功能。我们对业务逻辑做出假设，并且当我们创建一组智能合约的时候，我们没有做任何严格的安全措施。在部署你的代码前，一定要对你的代码做一个全面的安全审计。

### 1.创建一个发售/发起一个Token

这已经在[以太坊官方网站](https://ethereum.org/crowdsale)描述过。为了创建安全的发售，建议使用 Open Zeppelin 创建的 [audited contracts](https://github.com/OpenZeppelin/zeppelin-solidity/tree/master/contracts/crowdsale)。

你可以参考[这份指南](https://blog.zeppelin.solutions/how-to-create-token-and-initial-coin-offering-contracts-using-truffle-openzeppelin-1b7a5dae99b6), 或者[这个视频](https://www.youtube.com/watch?v=ShW2zQcY4LY)来实现。

### 2.高级功能/跳过努力
![](https://i.imgur.com/SZ98sMV.png)

在这里查看所有的代码: [https://ethfiddle.com/O3_2o-oqaZ](https://ethfiddle.com/O3_2o-oqaZ)

在这个例子中，我们可以看到一个用户可以通过花费 `1ether` 绕过 `winCount` 的升级要求。然后，应用所有者调用我们之前讨论过的 `withdraw` 函数，于是他们得到了他们的资金。

注意以太币的价格也许会在将来剧烈的升高（或降低），这将会改变使用你的高级特性的花费。所以在很多情况下，添加一个允许你在未来改变花费的`onlyOwner`函数是合理的，否则你的应用将可能变得非常昂贵。这适用于接下来所有的例子。

### 3.收取一定比例的交易市场手续费

在这个（非常简化）的例子中，当一个人想买一个僵尸的时候，价格的10%被发送到你的钱包，剩下的被转给到僵尸的拥有者。

![](https://i.imgur.com/eTX2syY.png)

查看整个合约在: [https://ethfiddle.com/MuApSyO3jx](https://ethfiddle.com/MuApSyO3jx)

为了节约一些费用，你可以跳过函数的第一行，这将会把以太币留在交易的余额里。通过使用我们之前描述的 `withdraw` 函数，你可以后面的某个时间点提取合约上所有的以太币种。

### 4.订阅/会员

这里，我们将会看到实现订阅/会员的商业逻辑的例子，主要有

1. 永久有效
2. 基于时间的
3. 基于使用的

我们将会创建一个合约，在合约中包括几个仅仅能够被个人调用的可行的函数。

#### 终生会员

这里是一个简单的例子，创建一个布尔类型的 `mapping`, 一个用来判断布尔值是否为真的 `modifier` 和一个允许一个用户花一些钱成为会员的函数。

![](https://i.imgur.com/yiaEXle.png)

在这里查看整个合约: [https://ethfiddle.com/LgzLNtIIVF](https://ethfiddle.com/LgzLNtIIVF)

或者，相对于使用一个布尔值代表会员/非会员，我们可以使用一个 `uint8` 类型，设计不同的会员等级，拥有更多的特性：免费用户是等级0，等级1是银牌会员，等级2代表金牌会员等。
`onlySilver()` 能够检查会员等级是否 `>=1`。

这很简单，让我们继续。

#### 有时限的会员/订阅

在这里我们的商业模型将会假设订阅每天花费0.005以太币。

![](https://i.imgur.com/qtRpqHF.png)

在这里查看整个合约: [https://ethfiddle.com/Dx1jQlgazK](https://ethfiddle.com/Dx1jQlgazK)

在这个例子中，当一个用户调用 `renewSubscription` 函数的时候，如必要的话 `subscriptionExpiration` 会被初始化为 `now`，并且会根据用户的付费增加一些天数。
`onlyMember` 修饰语可以被用来检查当前的时间是否超过了会员有效期。

#### 基于使用的会员/付费使用

这里的商业模型涉及到一个用户预先购买函数调用，有点类似于你用设定好的价格购买 API 调用。

在这个例子中，用户每个以太币可以购买1000次调用。用户每次调用有`onlyIfEnoughCalls`修饰符的函数，在检查符合调用条件后，`availableCalls` 变量会减少。

![](https://i.imgur.com/G8F9V8K.png)

在这里查看整个合约: [https://ethfiddle.com/rO0xD9nIl6](https://ethfiddle.com/rO0xD9nIl6)

在上面所有的情景中，你可以添加对应的 `only{property}` 类型修饰符给任何函数，然后它将可以被有授权的用户调用。

## 结论

在这个包含两部分的系列文章中，我们讨论并且实现了一些可以应用到你的 DApp 的商业模型，当你的目标是用它盈利的时候。

我想强调这篇文章给出的所有代码都是每个模型最基本的实现，需要根据你的需求进行修改。

![](https://i.imgur.com/4W1OsGp.gifv)

对 DApp 开发感兴趣？看看我们关于如何开始的免费课程。

----
via: https://medium.com/loom-network/6-ways-to-monetize-your-ethereum-dapps-part-2-857a2820dec4

作者：[Georgios Konstantopoulos](https://medium.com/@gakonst)
译者：[maojr](https://github.com/maojr)
校对：
