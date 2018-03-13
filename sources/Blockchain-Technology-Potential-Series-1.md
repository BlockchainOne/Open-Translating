# Blockchain Technology Potential (Series 1) – A Review of a Recent PAYPAL CryptoCurrency Patent Filing and What It Means for the Future of the Technology

In the midst of the currently bearish environment for cryptographically-enabled digital currencies, or cryptocurrencies for short, this series will be looking at the less noticed developments that tell a lot about the value of this technology and point to actually a really bright future for those that position themselves correctly in its budding development.
In the first of these series, we will be taking a look at a recently filed Paypal patent, what it tells us about how they see the technology, how they may be positioning themselves, and what it might say about the future potentially.

One problem with the crypto community is that things happen so fast that sometimes many are conditioned to be impatient. Just like in 2014, many were lamenting and down on themselves for buying at the top, and many abandoned at the height of the downturn. But those who got in substantially at the time are able to retire today by 2017. In general, many new entrants into this technology expect good things to happen within weeks.

Bitcoins was at about $1200 at the height of its 2014 bubble before falling by about 80$. In 2017 many people would have been happy to have bought at its pre-crash value. Yes sometimes things change really rapidly within weeks in cryptocurrencies but the best strategy would likely be to really understand fundamentally the technology and then with true understanding make the best informed judgement. And then not second guess that on a daily, weekly, or even monthly basis. And no one does not have to be a programmer to be one of the winners of the immense change that will likely take place in the next couple of years.

So let’s get into the patent filing.
**TITLE:** EXPEDITED VIRTUAL CURRENCY TRANSACTION SYSTEM
**PUBLICATION NO.:** US 2018/0060860
**PUBLICATION DATE:** MAR. 1 2018
**FILING DATE:** AUG. 30 2016
**LINK TO PUBLICATION:** [USPTO site link to patent](http://appft.uspto.gov/netacgi/nph-Parser?Sect1=PTO2&amp;Sect2=HITOFF&amp;u=%2Fnetahtml%2FPTO%2Fsearch-adv.html&amp;r=1&amp;p=1&amp;f=G&amp;l=50&amp;d=PG01&amp;S1=20180060860.PGNR.&amp;OS=dn/20180060860&amp;RS=DN/20180060860)

The invention in the patent is basically a way to perform an instant transaction on a blockchain that would normally require some time for the transaction to be confirmed. The idea behind the patent is to pre-split any balance a user has in their wallet into smaller sub amounts in multiple addresses on the blockchain. When it is time to make a payment and the amount is known, they simply combine those smaller balances into the payment amount and send the private keys of the secondary addresses to the other party instead of transferring anything on the blockchain. Sending the keys over encrypted media can be done virtually in an instant using an wallet App built, say by Paypal. Once the other party has the private keys to the amount then they do not need to wait for anything to be mined on the blockchain. The patent then includes provision for destroying copies of the sub-address address keys from the original owner after they are transferred.

![](https://i.imgur.com/6oCcIqY.png)

**Source:** Illustration by Current Author.

*This paragraph can be ignored for any disinterested in math*
An example of the breakdown of a balance of 300 units, for instance into smaller addresses is shown in the figure above. From those sub-wallets, any amount to pay can be composed, and the keys to those smaller amounts all sent to the recipient or merchant. For instance, in the figure, amounts of 142 and 37 units are shown. For a non-round figure such as 231, the decomposition would be into 1 (100s), 12 (10s), and 11 (1s). We leave it as an exercise to the reader why not 2 (100s), 3 (10s) and 1 (1s). The algorithm to accomplish this was missing in the patent application, but would involve some mildly nifty base 10 operations1. (Note also that the above is the author's description of how this could be accomplished.)

*Continue*
So basically with this method, Paypal would potentially be able to accomplish instant payment over a blockchain that needs 10 minutes for transactions to confirm, and allows an App built on that principle to be usable for in-person, in-store transactions. This is distinct from the method used currently by crypto-debit cards where you essentially transfer balances into the control of the provider from which they can essentially make payments on your behalf instantly because they control the keys to the balances. Also, this is not the same problem as scaling. Scaling simply addresses how many transactions a blockchain can handle not how fast. For instance, Bitcoin Cash improved on Bitcoin scaling by mining bigger blocks, so they can fit in more transactions in each block, but still every 10 minutes.

**What Does This Mean for Blockchains and CryptoCurrencies?**

This probably means that Paypal sees a potential in using blockchain for instant payments. It also means that the gap that currently exists in many first and second generation blockchains that render them unusable for in-store transactions or situations where you need to make payments instantly still needs to be addressed. No store will keep a checkout line open for 10 minutes for the customer’s bitcoin transfers to the store’s account to get mined. And much work is going on in addressing this gap including by third generation blockchains. Note that second generation blockchains like Ethereum for instance take about 25 seconds – still probably long for in-store transaction. However, centralized blockchains like Ripple and Lumens take a few seconds.

Also, third generation solutions such as EOS and Steem also do take a few seconds. DAG-type blockchains like IOTA, Byteball, and Nano are expected to take seconds as well but have barely yet being tested for any reasonable length of time in production conditions. This all shows that the entire technology field is still basically at the ground floor. Maybe first floor at best. There is going to be so many more changes and more innovations that will slowly be proven as we go along. It also means there are lots of opportunities as well. And finding those requires due diligence, and not following trading analysts for recommendations that lack understanding of the technology or the fundamentals behind it.

**Will This Specific Patent Prove Important in the Long Run?**

I personally doubt this. I can only surmise that this was submitted at a time bitcoin fees were low. Splitting every balance into small sub-balances is going to slowly accumulate a lot of fees, otherwise. And this method clutters a blockchain that may already have scaling challenges with more transactions in splitting balances up, and using up more addresses. The method does have a merit in that it can be built on top of any blockchain. It also maintains the decentralized solution when built on top of a decentralized blockchain. However, I expect that some of the other off-chain solutions to enable instant transactions such as Lightning on Bitcoins, Raiden and Plasma on Ethereum, and Masternode instant send methods on Dash, and centralized solutions, might prove to more temporarily fill that gap. In particular, I expect the centralized methods of crypto-debit cards, or centralized hubs of the Lightning-style networks to probably end up filling the gap until on-chain solutions mature; which will still take a few years.

If this article has inspired you towards any innovative ideas let us know below, and feel free to reference this article. All reasonable comments will be upvoted. And follow for more such articles in future, and upvote it to 100% so many more can see this content.

1. This would require that for a number of order 10n, the subdivisions must have at least 10 sub items of order 10n-1.
**References:**
[https://cointelegraph.com/news/2018-blockchain-and-cryptocurrency-outlook-expert-blog](https://cointelegraph.com/news/2018-blockchain-and-cryptocurrency-outlook-expert-blog) (Prediction of Current Bearish Stretch)

[https://www.sciencedirect.com/science/article/pii/S1567422317300480](https://www.sciencedirect.com/science/article/pii/S1567422317300480) (Peer Reviewed Fundamental Modeling of Cryptocurrency Values)

[https://steemit.com/bitcoins/@kenraphael/there-is-little-chance-bitcoins-can-sustain-any-real-recovery-until-this-fundamental-metric-begins-to-turn-upwards-again](https://steemit.com/bitcoins/@kenraphael/there-is-little-chance-bitcoins-can-sustain-any-real-recovery-until-this-fundamental-metric-begins-to-turn-upwards-again) (Pointing Out Weeks Ago that Bitcoin Might Still be Bearish While Analysts Were Already Telling Followers to Buy at 11K, and 12K)

[https://steemit.com/bitcoin/@kenraphael/a-review-of-a-few-fundamental-metrices-that-drive-bitcoin-value-and-what-they-currently-indicate](https://steemit.com/bitcoin/@kenraphael/a-review-of-a-few-fundamental-metrices-that-drive-bitcoin-value-and-what-they-currently-indicate) (Some Fundamental Metrics that Drive Bitcoin Market Value)

**About the Author**
Ken has a doctorate in Engineering, and a master’s in Computer Aided Engineering, An IT professional, programmer and published researcher with over thirty publications in various fields of technology, including several peer reviewed journals and publications.

**Legal Disclaimer:** I am not a financial adviser and this is not financial advice. The information provided in this post and any other posts that I make and any accompanying material is for informational and educational purposes only. It should not be considered financial or investment advice at all. You should consult with a financial or investment professional to determine what may be best for your individual needs. This is only opinion. It is not advice nor recommendation to either buy or sell anything! It's only meant for use as informative, educational, or entertainment purposes.

[Blockchain Technology Potential (Series 1) – A Review of a Recent PAYPAL CryptoCurrency Patent Filing and What It Means for the Future of the Technology](https://steemit.com/bitcoin/@kenraphael/blockchain-technology-potential-series-1-a-review-of-a-recent-paypal-cryptocurrency-patent-filing-and-what-it-means-for-the)