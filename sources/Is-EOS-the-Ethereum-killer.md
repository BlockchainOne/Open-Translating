# Is EOS the Ethereum killer?

![](https://i.imgur.com/aiBlOr6.jpg)

Today at [Consensus 2017 event held in NY](http://www.coindesk.com/events/consensus-2017) Dan Larrimer announced his new project —  [EOS](http://eos.io/). Dan is known as the leader behind BitShares, Graphene and Steem technologies.

You can see live stream recording of the announcement [here](https://www.pscp.tv/w/1YpJknevAnEGj).

> You need to scale to millions of users, but you can’t

If you are going to build some DApp (decentralized application), then what options do you have today?

* Corda and Hyperledger Fabric are for private networks only and have limited smart contract support.
* RChain, Rootstock/RSK, have not yet been released or not production-ready.
* BitShares and Graphene have very good throughput, but limited smart contracts capabilities.
* [Polkadot repo has not been updated in the last 6 month](https://github.com/polkadot-io/).
* NXT, Waves, Lisk, Tezos, Tauchain (you name it…) are not competitors…
It seems that you are left only with **Ethereum** which has a very bad throughput and high transaction costs.

Why not try to combine the scalability of Graphene and the power of Ethereum’s smart contracts together? Etherum will migrate from Proof-of-work to Proof-of-stake (scheduled at the end of 2017/beginning of 2018) so we have some time to build a new competitor.

2 months ago [Dan Larrimer resigned from Steemit](https://steemit.com/steem/@dantheman/thank-you) in order to (obviously) develop/promote his new tool. Welcome, the new Ethereum killer!

> I created Steem with a team of 2 developers working for 3 months

There’s not much technical information available currently. But EOS is not just about smart contracts + high scalability. It has a completely different design and vision compared to Ethereum.

EOS uses Delegated Proof-of-Stake just like Graphene does.

It uses Network Bandwidth Allocation system to effectively share the blockchain.

> It’s like time sharing. It’s like owning an instance on an Amazon web service that you can share

In EOS the human-readable source code (the “bot”) is uploaded directly to the blockchain. As we know, the Ethereum smart contracts are binary data instead.

If there’s a bug in your application — then community can freeze it and then deploy a fix. Very interesting!

> EOS is structured like a group of people and/or scripts (bots) that are exchanging messages between them. It could be thought of as an email system where every user or bot has an account

The Account also known as the “Application” is a private JSON-formatted database easily accessible by any blockchain explorers.

All the communications between apps have self-describing interfaces, and declarative permission scheme. This means that you have to describe what messages your app wants to receive and what it will send (probably). It allows to *firewall* applications from each other but still allows them to communicate.

> Unlike e-mail, the recipient and any accounts copied on the message have the ability to reject the message in which case the message will not be delivered to them

EOS is designed to support communication not just internally, but externally too. So it should be possible to connect other blockchains to communicate with them.

You can check what smart contracts look like in EOS here —  [https://steemit.com/eos/@eosio/implementing-a-hypothetical-currency-application-on-eos](https://steemit.com/eos/@eosio/implementing-a-hypothetical-currency-application-on-eos). This article was published by Dan 6 days ago (16th of May, 2017).

Q1. How do smart contracts work in parallel?
**Answer by Dan**: “All the contracts are processed on the same chain, the messages are on the block chain, not the state. Every single account operates like its own chain, and supports interoperation between all other accounts without locking, so determinism is preserved”

Q2. Are there any blockchains comparable to EOS?
**Answer by Dan**: “No, this is an incremental improvement on Steem and Bitshares. It is the general case to those special cases. It builds on more than 4 years of continuous development and innovation from the Bitshare and Steem community”.

Q3. Do you plan to run Steemit on top of EOS?
**Answer by Dan**: “EOS can support applications like Bitshares or Steem. But it’s totally up to Steem team”.

Q4. What about EOS token distribution?
**Answer by Dan**: “We will send this information later in the mailing list”.

Q5. What does EOS stand for? Ethereum On Steroids?
**Answer by Dan**: “Hahaha, no”

Wow! Great product. Can’t wait to see and try it. We are going to be among the first EOS app developers. By the way, EOS logo is a geometric structure that forms a heart!

The only bad thing is that they have Brock Pierce on board now. I think he is a junkie. Not good for the team. Sorry. Even the [blockchain constitution](https://steemit.com/eos/@dantheman/what-could-a-blockchain-constitution-look-like) won’t help.

From the official [EOS Telegram channel](https://t.me/EOSproject):
“Now Brock Pierce is at the microphone. He seems a little hung over from the party he hosted last night”.

**Do you think EOS is the Ethereum killer?**

p.s. We are currently building the “Microcompany Tokenization Platform” here —  [https://web.thetta.io](https://web.thetta.io/)

We need your help. Become a part of our team/community (+bounties and +rewards) and deliver great product together with us!

[Is EOS the Ethereum killer?](https://medium.com/chain-cloud-company-blog/is-eos-the-ethereum-killer-ad24277d8c9c)