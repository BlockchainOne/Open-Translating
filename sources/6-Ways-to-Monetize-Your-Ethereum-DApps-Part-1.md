Translating by lucas
# 6 Ways to Monetize Your Ethereum DApps (Part 1)

In [our last article](https://medium.com/loom-network/why-you-should-learn-to-build-blockchain-apps-be9a92e8d08e), we went over **why** you should learn to build Blockchain DApps.

In this article, we will talk about **how** you can monetize them.

Before getting into DApp-specific cases, let’s try answering a popular question:

> How do traditional apps make money?

Simply said, advertisers pay content providers and technology companies (you, the developer) to put advertisements in front of consumers (your users). Consumers in turn are influenced by the advertisements (whether they think they are or not), and spend money on the advertiser’s products.

In the old App Store days, there were the ‘Lite’ or ‘Regular’ and the ‘Pro’ versions of apps. Users would try out what the product offered, and if they liked it would purchase the full version of the App.

![](https://i.imgur.com/SUZR9rP.png)

Using that business model, companies such as Spotify, Slack or Onedrive generated revenue from their users who would purchase a paid subscription for their service.

Other examples of the freemium model include gaming apps which allow the purchase of in-game items for real currency.

Free-to-play MMORPG’s have utilized the so-called ‘Free to Play Restrictions’. As a free player in World of Warcraft, the maximum allowed level is Level 20. Other games, had limitations on the areas you could explore. The best content of such games is reserved for the “Pay to Play” gamers.

> With the above in mind, there is a lot of low hanging fruit a DApp developer can go after when looking to monetize their DApp.

As discussed in [the previous post](https://medium.com/loom-network/why-you-should-learn-to-build-blockchain-apps-be9a92e8d08e), you can always bootstrap your project through a crowdsale backed by a token.

In this case you need to define the need for your token[ [1](https://medium.com/@mrdavey/good-discussion-and-question-2446e3827de2) ]:

* Core functionality of your DApp ( [Golem](https://golem.network/), [Aragon](https://aragon.one/), [Request](https://request.network/) )
* Provides access to your network ( [BAT](https://basicattentiontoken.org/), [Bloom](https://hellobloom.io/) )
* Distribute profits of the product to token holders (TenX, Numerai)
Note that in this case you need to be careful with regulations and KYC compliance depending on if your token is considered a security or not.

Cryptokitties charged a 3.75% fee for each successful auction. This proved to be a [very profitable revenue model](https://medium.com/@codetractio/a-look-into-cryptokitties-revenue-model-6466b705a998).

![](https://i.imgur.com/Z4HZHLa.png)

Last Week CK usage peaked 800 ETH in transaction fees. Source: [DappRadar.com](https://dappradar.com/)

As a more general example:

1. **A** buys something from **B** using your service
2. **Y** % of that amount goes to the service provider (you)
3. (100- **Y** )% goes to B
There is a caveat here. If you make a decentralized service that has an “unfair” fee towards the end-user, someone will eventually copy your Smart Contracts and release a version of them with lower fees or no fees at all (given that your contracts are Verified and Open Sourced, which is typically expected of Ethereum DApps).

> Finding the right amount to charge your users is the key here; however we will not get into pricing models in this post.

Inspiring ourselves from the freemium model discussed before, and by using the game we’re building in [CryptoZombies](https://cryptozombies.io/) as an example, think of the following:

Let’s say that your CryptoZombie requires 10 wins in order to level up, and that gets harder as its level increases.

Leveling up from Level 10 to Level 11, will be harder than leveling up from Level 1 to Level 2. Users need to consume a lot more effort in order to level up their Zombie Army.

![](https://i.imgur.com/z7Rewob.png)

Law of Diminishing Returns

Here you can implement a function, which allows the Zombie to “skip” the effort and level up directly, and in return the user would need to pay some amount of ether.

That way, players who play for free are still able to achieve end-game results, but the ones who are willing to pay a premium can skip the effort.

The same could apply for resetting the cooldown of a Zombie. Zombies typically need to wait for `cooldown` seconds before fighting again, but we could make it so users can pay a small fee and skip the cooldown.

There are a lot of different ways you could monetize DApps here, and we will talk about specific code implementations in part 2 of this article.

You could add a subscription or membership functionality to your contracts , to make it so that certain functions can only be called by subscribers, or by premium members.

The duration of the subscription could be:

* **Time-Based:** The user is allowed to call a function until X time has passed, e.g. they could pay for 1 month of access.
* **Usage-Based:** The user is allowed to call a function X times.
You can read more about Subscription models on [Wikipedia](https://en.wikipedia.org/wiki/Subscription_business_model).

Again, we will look at specific code examples of how to implement this in part 2 of this article.

This has been a less-popular method, considering we are talking about advertisements on the DApp itself. The [ThousandEtherHomepage](http://thousandetherhomepage.com/) does just that. You are able to claim a number of array slots in the Contract, which get represented by pixels in the DApp’s front-end. As seen by the picture below, these pixels have been used by projects (among others) in order to advertise their brand.

![](https://i.imgur.com/fYNqkJi.png)

If any of the above sounds like too much a hassle, you can always just add your cryptocurrency address at your service/DApp for any generous donors.

You could also add the [eth-button](https://eth-button.github.io/eth-button/) to your webpage for Metamask integration.

![](https://i.imgur.com/hS3Kocb.png)

[eth-button.github.io/eth-button](http://eth-button.github.io/eth-button)

Part 1 was a more theoretical approach. Part 2 will include code implementations based on some of the monetization concepts discussed above.

Stay tuned!

![](https://i.imgur.com/eTXoU5g.gifv)

Interested in DApp development? Check out our totally free course for how to get started ⬆

[6 Ways to Monetize Your Ethereum DApps (Part 1)](https://medium.com/loom-network/6-ways-to-monetize-your-ethereum-dapps-part-1-28e9bb18f87e)
