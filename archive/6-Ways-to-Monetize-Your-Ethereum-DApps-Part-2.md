Translating by [maojr](https://github.com/maojr)

# 6 Ways to Monetize Your Ethereum DApps (Part 2)

In [Part 1](https://medium.com/loom-network/6-ways-to-monetize-your-ethereum-dapps-part-1-28e9bb18f87e?source=user_profile---------4-------------------) of this 2-article series we had a theoretical approach towards monetizing your Ethereum DApps. In this part we will look at some code examples that show how you can actually implement them in Solidity.

To start with, there needs to be a function that will allow the withdrawal of the funds to the owner’s address. This is as simple as:

![](https://i.imgur.com/yYJPN1W.png)

This function will transfer the balance of the calling contract to the address at `owner` (using the very popular `onlyOwner` modifier pattern). If you are unfamiliar with how the keywords above work, you might want to stop reading here and resume after completing our lessons at [CryptoZombies.io](https://cryptozombies.io/)

**Disclaimer:** All of the following examples are simplified to illustrate how you can implement **only** the discussed functionalities. We make assumptions about the business logic, and we do not take any rigorous security measures that we would take when creating a suite of smart contracts. Always do a full security audit of your code before pushing to production!

This has been described in the [Official Ethereum Webpage](https://ethereum.org/crowdsale). In order to create a secure crowdsale, it is recommended to use the [audited contracts](https://github.com/OpenZeppelin/zeppelin-solidity/tree/master/contracts/crowdsale) created by Open Zeppelin.

You can follow [this guide](https://blog.zeppelin.solutions/how-to-create-token-and-initial-coin-offering-contracts-using-truffle-openzeppelin-1b7a5dae99b6), or [this video](https://www.youtube.com/watch?v=ShW2zQcY4LY) for that purpose.

![](https://i.imgur.com/SZ98sMV.png)

View the whole code at: [https://ethfiddle.com/O3_2o-oqaZ](https://ethfiddle.com/O3_2o-oqaZ)

In this case, we can see that a user can bypass the `winCount` requirement for leveling up, by paying `1 ether`. The owner would then call the previously discussed `withdraw` function so that they get their funds.

Note that the price of Ether may go up (or down) drastically in the future, which would change the cost of your premium feature. So in a lot of cases it makes sense to add an `onlyOwner` function that allows you to change the cost in the future, otherwise your app may become prohibitively expensive. This goes for all the following examples as well.

In this (much simplified) example, when someone wants to buy a zombie, 10% of the price gets sent to your wallet, while the rest gets transferred to the zombie’s owner.

![](https://i.imgur.com/eTX2syY.png)

View the whole contract at: [https://ethfiddle.com/MuApSyO3jx](https://ethfiddle.com/MuApSyO3jx)

In order to save some gas costs, you can skip the first line of the function, which will instead leave the ether at the contract’s balance. By using the `withdraw` function we described earlier, you can at a later point in time withdraw all the ether that the contract has.

Here we will look at examples of implementing subscription / membership business models for:

1. Lifetime
2. Time-based
3. Usage-based
We will create a contract where certain functions will only be callable by individuals which have been marked as eligible.

This is a simple case of creating a boolean `mapping`, a `modifier` that checks if the boolean is true, and a function that allows a user to become a member for some price.

![](https://i.imgur.com/yiaEXle.png)

View the whole contract at: [https://ethfiddle.com/LgzLNtIIVF](https://ethfiddle.com/LgzLNtIIVF)

Alternatively, instead of using a boolean for member/non-member, we could use a `uint8` and have different membership tiers with access to more and more features: tier 0 for free users, tier 1 for silver membership, tier 2 for gold membership, etc. Then `onlySilver()` could check if the membership tier is `>= 1`.

Simple enough, let’s move on.

Here our business model will assume that the subscription costs **0.005** **ether per day.**

![](https://i.imgur.com/qtRpqHF.png)

View the whole contract at: [https://ethfiddle.com/Dx1jQlgazK](https://ethfiddle.com/Dx1jQlgazK)

In this case when a user calls the `renewSubscription` function, the `subscriptionExpiration` gets initialized to `now` if necessary, and then increased by a number of days depending on how much the user paid. The `onlyMember` modifier can be used to check if the current time has passed the expiration date.

Here the business model involves a user buying function calls upfront, similarly to how you can buy API calls at a set price.

In this example, a user can buy 1000 calls per ether. Every time a user makes a call to a function that has the `onlyIfEnoughCalls` modifier, after checking that they are eligible for the call, the `availableCalls` variable is decremented.

![](https://i.imgur.com/G8F9V8K.png)

View the whole contract at: [https://ethfiddle.com/rO0xD9nIl6](https://ethfiddle.com/rO0xD9nIl6)

In all of the above scenarios, you could simply add the corresponding `only{property}` modifier to any function, and then it would only be callable by the users who are authorized to access it.

In this 2-part article series we discussed and implemented some business models you can apply to your DApp when your goal is to monetize it.

I want to emphasize that all the code given in this post is a very basic implementation of each model and should be adapted to your exact needs.

![](https://i.imgur.com/4W1OsGp.gifv)

Interested in DApp development? Check out our totally free course for how to get started ⬆

[6 Ways to Monetize Your Ethereum DApps (Part 2)](https://medium.com/loom-network/6-ways-to-monetize-your-ethereum-dapps-part-2-857a2820dec4)
