# The Beginner’s Guide to Ethereum’s Roadmap

![](https://i.imgur.com/ID5HBfW.png)

Ethereum’s mission is to become a decentralized world computer that replaces server farms. Think of it as a single computer that the whole world can use. It can’t be shut down or turned off. As an overview, here’s a [beginner’s guide to Ethereum](https://blog.coinbase.com/a-beginners-guide-to-ethereum-46dd486ceecf) and an explanation of [how it technically works](https://medium.com/@preethikasireddy/how-does-ethereum-work-anyway-22d1df506369).

If Ethereum is a computer, then each one of these updates can be looked at as an operating system (OS). Similar to Google launching Android Oreo or Apple launching iOS 10, Ethereum is launching in four stages.

Each stage adds new features and improves the user friendliness and security of the platform, while allowing Ethereum to scale.

1. **Frontier** (July 2015) — First live release of the Ethereum network. It allowed developers to experiment, mine Ether, and begin building dApps and tools.
2. **Homestead** (March 2016) — First production release of Ethereum that brought many protocol improvements which lay the foundations to future upgrades and for speeding up transactions.
3. **Metropolis** (Oct 2017) — Lighter, faster and more secure Ethereum broken down into two releases: Byzantium (Oct 2017) and Constantinople (TBA)
4. **Serenity** (TBA) — Will bring us the long-awaited Proof of Stake using the Casper consensus algorithm.
All of these updates will help Ethereum scale, which means faster transaction times and lower fees for everyone. As you can see, the Ethereum team has done a great job of scaling transactions.

![](https://i.imgur.com/7xujvcK.png)

Source: [Etherscan](https://etherscan.io/chart/tx)

Metropolis promises to be a lighter, faster and more secure version of Etherem. It will also provide greater flexibility to smart contract developers.

Metropolis will be split into two core releases: Byzantium and Constantinople. The first hard fork (Byzantium) took place in [October](https://www.coindesk.com/ethereum-executes-blockchain-hard-fork-byzantium/). The second hard fork (Constantinople) does not have a set date yet but is expected in 2018.

Each of these phases includes a set of Ethereum Improvement Proposals or EIP for short. Byzantium has a total of [nine EIPs](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-609.md) to improve the network’s privacy, scalability and security. All of these updates will result in faster blocks and lower fees for users.

Here are the major updates of Metropolis:

* Privacy — ability to perform anonymous transactions (zk-SNARKs)
* Easier programming for developers
* More predictable [gas charges](https://ethereum.stackexchange.com/questions/3/what-is-meant-by-the-term-gas)
* Increased security for wallets (account abstraction)
* Mining adjustment that will make mining more difficult (difficulty bomb)
In Metropolis, developers will get a new privacy tool — the ability to verify zk-SNARKs efficiently on-chain. zk-SNARKs is an abbreviation of “zero-knowledge succinct non-interactive arguments of knowledge.”

Simply, a zero knowledge proof is one which demonstrates the truth of a statement without revealing any additional information beyond what it’s trying to prove.

Here’s a simple example. I need to prove to John that I know the passcode to a random cell phone. In order for me to do that, I need to unlock the phone without revealing the passcode entered.

A zero-knowledge proof is when a *prover* (me) convinces a *verifier* (John) that they have certain knowledge without revealing the actual knowledge. In this example, I can type in the passcode into the phone and show that the phone is unlocked without revealing what I typed.

So, how does this impact Ethereum? Certain contact variables can be made private. Instead of storing this secret information on the blockchain, it can be stored with users. Some things that can be hidden in a transaction include the sender, recipient, amount, and data.

In addition to zkSnarks (used in zCash), Ethereum will get ring signatures as well (used in Monero’s privacy scheme). This is a fancy way of setting that Ethereum will get the best of both!

**Account abstraction**
 In software engineering, abstraction is a tool that allows programmers to think on a certain level of complexity, hiding the details not important to the problem at hand. Developers use abstractions to prevent overloading the end user with details when they care more about higher level concepts.

This will give users more control over their private keys while also adding the ability for contracts to pay mining fees. Abstraction will also reduce the risk of being hacked by [quantum computing](https://hackernoon.com/how-i-cornered-the-bitcoin-mining-market-using-a-quantum-computer-9e5dceba9f92).

**Mining difficulty-bomb**
 The time bomb is to begin the process of moving Ethereum away from Proof of Work (PoW) over to Proof of Stake (PoS). This will make it more difficult for miners and make it less profitable for them in the future as we move from a miner-based PoW to a validator-based PoS system. Also, the number of ETH issued per block will drop from 5 to 3.

This is the last phase of the Ethereum roadmap and will switch the Ethereum Network from Proof-of-Work to Proof-of-Stake. The hope for serenity is to bring the Ethereum network mainstream.

![](https://i.imgur.com/1fUYs42.png)

Source: [Blockgeeks](https://blockgeeks.com/guides/proof-of-work-vs-proof-of-stake/)

Most blockchains run on ‘proof-of-work’ which means that miners solve cryptographic puzzles to mine a block to the blockchain. These puzzles get harder over time and requires a lot of energy and computing power.

The problem with ‘proof-of-work’ is that it’s becoming more and more centralized. This means that a few mining companies control the hashrate of Bitcoin. [As of right now, 71.2% of the hashrate is controlled by five mining pools.](https://blockchain.info/pools)

As the cryptographic puzzles become more challenging, it requires more hardware and energy which is also very expensive. This makes it harder for anyone to mine, which further centralizes to a few mining pools.

Why is this bad? If these five mining pools coordinated, they can unleash a [51% attack](https://www.investopedia.com/terms/1/51-attack.asp). The attackers would be able to prevent new transactions from gaining confirmations, allowing them to halt payments between users. An event like this could possibly even legitimize a different blockchain such as Bitcoin Cash.

Ethereum’s solution to this is to move towards ‘proof-of-stake’. This means that validators (instead of miners) will have to put up Ether as a stake and then ‘validate’ blocks by placing a bet on it. If the block gets appended, you will get a reward proportional to your stake. If you bet on the wrong block, your stake will be taken away.

Proof-of-stake also helps solves some of the problems with proof-of-work. It helps achieve decentralization, energy efficiency, and helps Ethereum scale.

This is the name of the ‘proof-of-stake’ protocol for Ethereum. There are two version of Casper. One is being led by [Vlad Zamfir](https://twitter.com/VladZamfir?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor) who has been at the forefront of Ethereum’s development. The other is called FFG (friendly finality gadget) that is being led by Vitalik Buterin.

Similarly, there will be stakers who “stake” their coins by locking them down in special wallets. These stakers will be rewarded through an annual dividend of ether. So, the more ETH you stake, the larger your dividends will be.

In PoS, no matters what happens, you will always win and have nothing to lose. The only way to lose your stake is if you maliciously validate wrong blocks.

Casper moves towards a “proof of stake” consensus which prevents a 51% attack from ever happening. [Temporary and sustained 51% attacks](https://ethereum.stackexchange.com/questions/542/during-a-51-attack-what-can-the-attacker-actually-accomplish) hold key implications for Ethereum’s future. Casper secures it further.

Casper will pave the way for scaling Ethereum to achieve mainstream adoption. In order to do this, Ethereum needs to handle large volumes of transactions. Otherwise, costs skyrocket and it takes longer for transaction to go through.

Ethereum founder Vitalik recently proposed a plan to help scale Ethereum through sharding. Rather than have transactions run in linear order, sharding allows blocks to happen in parallel.

Think of this as the difference between downloading one song from a friend vs using a Torrent to download the same file from thousands of people.

![](https://i.imgur.com/nSlbKuc.png)

[Sharding Intro](https://docs.mongodb.com/v3.0/core/sharding-introduction/) from MongoDB

Sharding is also the process of splitting up the chain data, so that every node only has to worry about a small portion of the chain.

This will allow Ethereum to process thousands of transactions per second — all on the same chain. It’s estimated that this will happen in a few years.

* Bitcoin is processing ~7 transactions / second
* Ethereum is processing ~15 transactions / second
* Paypal is processing ~200 transactions / second
* Visa is processing ~2,000 transactions / second but has the capacity to process 56,000 transactions / second
As you can see, Bitcoin and Ethereum have a long way to exceed the number of transactions that Visa is currently doing. (There is also a new company called [Hashgraph](https://squawker.org/technology/blockchain-just-became-obsolete-the-future-is-hashgraph/) that claims that it can process 250K transactions / second!)

Similar to Bitcoin, Ethereum has a scaling problem with rising smart contract fees that slow down transaction times, especially during ICOs. Plasma is an update which fixes the scaling issues with Ethereum. This is done in collaboration between Vitalik Buterin and Joseph Poon from the Lightning Network. (Picture crypto’s Kanye and Jay-Z working on a new album together.)

According to [Vitalik Buterin](http://ethereumworldnews.com/2020-roadmap-ethereum/), there are four major problems that need to be solved to push Ethereum to the next level: privacy, consensus safety, smart contract safety, and the biggest challenge to solve — scalability.

Ethereum is still a nascent technology but there are many promising scaling features that will allow to reach mainstream. If Ethereum can achieve its ambitious multi-year vision then it will lay down the foundation and backbone of the blockchain ecosystem!

[The Beginner’s Guide to Ethereum’s Roadmap](https://hackernoon.com/the-beginners-guide-to-ethereum-s-2020-roadmap-2ac5d2dd4881)