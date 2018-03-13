# Proof of Work, Proof of Stake and Proof of Burn

Learn the differences between the colloquially accepted meaning of different proofs within the cryptocurrency world of Bitcoin, Ethereum and then some.

This article aims to deliver a basic understanding of the following proofs and the nature around its observance. For all reasons unless explicitly specified, we shall refer to the oldest cryptocurrency in use, Bitcoin.

The concept of proof of work has existed long before blockchains did.
People are often asked to describe the nature of or show their previous work to correctly assess their implicit value. Bitcoin employs a puzzle friendly implementation of a one way hashing algorithm (SHA256) where the initial characters of the to-be generated hash is predefined.

On any input provided to this one way hashing algorithm, the outcome is always a 256 bits or 64 characters in hex format.

Sample SHA 256 Output looks like this: `68e656b251e67e8358bef8483ab0d51c6619f3e7a1a9f0e75838d41ff368f728`

The algorithm is designed such that every slight change in the input results in the output being completely different bearing no resemblance to its input.
A live demo of how one way hashes work can be found [here](https://anders.com/blockchain/hash.html), by Anders.

The nature of one way hashing algorithms is to bear no resemblance to its input. A one way hash function is a deterministic algorithm implying that a given input will always yield its corresponding output and none other.

An ideal one way hash function has no collisions. Given that a specific input always returns a specific output, in order to obtain a different output, the input must change. In bitcoin, the designed puzzle is such that a person must recursively hash until they obtain a hash whose initial digits/characters have already been specified.

The difficulty of obtaining a hash that matches the specific pattern changes increases exponentially as the number of specific digits increases.

In the case of Bitcoin, we can observe on a [blockexplorer](https://blockchain.info/block/000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f) how the hash of each block from genesis block (block 0) lead with a couple of zeros. 
This pattern of obtaining a series of zeroes to lead a hash gets harder as a longer series is demanded. The series of zeros leading a hash required is often used synonymously with the [difficulty level](https://en.bitcoin.it/wiki/Difficulty).

For example:
[Block 1](https://blockchain.info/block/00000000839a8e6886ab5951d76f411475428afc90947ee320161bbf18eb6048) leads with 8 zeros and the computation required for finding the [hash](https://blockchain.info/block-index/14850/00000000839a8e6886ab5951d76f411475428afc90947ee320161bbf18eb6048) that leads with 8 zeros is a lot more than the computation required to find the [hash](https://blockchain.info/block-index/1668012/0000000000000000000d6eed8b074d341f4216871d41afefdab2917f3c02d1ab) of [block 505751](https://blockchain.info/block/0000000000000000000d6eed8b074d341f4216871d41afefdab2917f3c02d1ab) that leads with 19 zeros.

[Block 1](https://blockchain.info/block/00000000839a8e6886ab5951d76f411475428afc90947ee320161bbf18eb6048):

```
00000000839a8e6886ab5951d76f411475428afc90947ee320161bbf18eb6048
```

[Block 505751](https://blockchain.info/block/0000000000000000000d6eed8b074d341f4216871d41afefdab2917f3c02d1ab):

```
0000000000000000000d6eed8b074d341f4216871d41afefdab2917f3c02d1ab
```

Finding the hash involves recursively passing the elements of the proposed block through the hashing function to test for a hash that matches the proposed difficulty and the difficulty level resets every 2016 blocks, roughly about 2 weeks.

The proof of work employed in bitcoin was required to be easy to verify but hard to arrive at. This is solved by using a nonce.A nonce is a non repeating number.

A nonce is included along with other contents of a block and is fed as input to the hashing algorithm. Upon obtaining a hash, if the hash does not correspond to the difficulty level, the nonce is increased by one and hashed again until a hash that appropriately corresponds to the difficulty level is obtained.

This nonce once obtained can be hashed along with the rest of the block’s contents to check the hash to verify. This verification process wouldn’t much time, but in order to come up with the nonce, one must hash the contents of the block and try various multiple iterations to obtain the nonce.

This implies that verification is extremely easy whereas coming up with the nonce in the first place is quite a laborious process.

Upon finding the nonce, the block containing the nonce is hence broadcasted to other bitcoin nodes on the network along with the hash to verify.

The whole process of finding the nonce is described as proof of work.

The nonce is the proof of work to establish that a miner has actually tried computing various iterations before arriving at this number and hence receives a block reward.

This has been adopted from [HashCash](https://en.bitcoin.it/wiki/Hashcash)

References:
[Bitcoin Difficulty Chart](https://bitcoinwisdom.com/bitcoin/difficulty)
[Difficulty Wiki](https://en.bitcoin.it/wiki/Difficulty) [Nonce Wiki](https://en.bitcoin.it/wiki/Nonce)
[HashCash](https://en.bitcoin.it/wiki/Hashcash)

Proof of stake is an algorithm to achieve distributed consensus within blockchain networks.

Proof is Stake is intended to replace Proof of work since a significant chunk of people believe that recursive hashing is largely unproductive and unnecessary.

Unlike bitcoin where anyone can mine irrespectively, Proof of Stake is structured to prioritize certain miners over other miners.

This prioritization can be based on their ownership of ether in the network, however that would cause undesired centralization since the richest miner would then have an unfair permanent advantage in the mining process that happens within the network.

There have been various implementations of numerous proposed ideas such as NXT, Blackcoin, decred hybrid and peercoin. The major problem remains in gaining consensus over what technique or prioritization factor would be necessary in deciding which block variants to be implemented.

Age, total percentage of tokens held in network and balance of address are among the considered factors for implementing proof of stake.

There have been a lot of speculation over Ethereum switching over from proof of work to proof of stake. Ethereum had previously suggested Slasher protocol before designing and implementing their own proof of work algorithm called Ethash.
A proof stake protocol named casper is in experimentation and could probably succeed Ethash.

References:

Proof of burn is an intended alternate replacement for proof of stake and proof of work while achieving distributed consensus.

Proof of work is based on recursive hashing to find a nonce and its implied cost is mainly time, equipment and electricity used while hashing recursively.

Proof of burn’s significance is largely brought about by “burning tokens” in a unrecoverable manner such that it is easy to verify and extremely hard to undo.

For example:

```
1BitcoinEaterAddressDontSendf59kuE -> 13.18813499BTC
```

It is highly unlikely that a private key exists or statistically be generated to that particular bitcoin address.

Proof of burn’s implicit cost is the token that are considered **unspendable**. Proof of work and Proof of burn both have their implied costs where proof of burn’s liability is mainly limited to the value of tokens to be rendered “ **burnt** ”.

In fact, Bitcoin’s first block reward to [this address](https://blockchain.info/address/1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa) is also unspendable or considered burnt..

Proof of burn has been used to add value to many altcoins and cryptocurrencies alike under the belief that burning a particularly valuable token to add the burnt token’s implicit value to a new token that’s to be generated.

[XCP(Counterparty)](https://counterparty.io/news/why-proof-of-burn/) and [Slimcoin](https://slimco.in/) are among the many that have used proof of burn to transfer value from one token to another.

This can be viewed in a similar manner to hedging.
A parent token that’s burnt is hedged and new tokens are released upon the burnt/hedged tokens to be used for other reasons.

Some view burning tokens as a transfer of intrinsic work done to obtain tokens based on the burnt tokens.

For example,on average if it takes 48,800 kw hrs to mine one bitcoin, by burning 10 bitcoins(488,000 kw hrs) and releasing a 488,000 tokens called say, tincoin; each tincoin would considered equivalent result of 1 kw hr of work done.

It all boils down to relative value transfer.

References:

* [How to destroy Bitcoins ?](https://medium.com/@alcio/how-to-destroy-bitcoins-255bb6f2142e)
* [Energy used to mine a single bitcoin](https://www.quora.com/How-many-kwh-does-it-take-on-average-to-mine-a-single-bitcoin)
* [Proof Of Burn Wiki](https://en.bitcoin.it/wiki/Proof_of_burn)

I hope this was helpful.
I write on blockchain, cryptography, psychology, economics, bitcoin and security at times.
Feedback, corrections and improvements are very much appreciated.

Cheers!
 —  [Prahalad Belavadi](http://medium.com/@prahaladbelavadi)

![](https://i.imgur.com/Y0OsymO.png)

[Proof of Work, Proof of Stake and Proof of Burn](https://hackernoon.com/proof-of-work-proof-of-stake-and-proof-of-burn-6823eac2776e)