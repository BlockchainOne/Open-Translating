# Mining is the new black

**UPDATED March 5th, 15.00**

Last year we published a [story](https://securelist.com/miners-on-the-rise/81706/) revealing the rise of miners across the globe. At the time we had discovered botnets earning millions of USD. We knew this was just the beginning of the story, which turned out to develop rapidly.

Together with the rest of the world, we have been watching the hike in cryptocurrency, for example, the price of Bitcoin and Altcoins continuously beat records throughout 2017.

![](https://i.imgur.com/LtRLb3E.png)

*Bitcoin and Altcoins prices growth in 2017*

While some spend time talking about what’s good or bad for the market and the global economy, we’ve seen that such a spike in prices was definitely a call for threat actors, meaning there are good opportunities for cybercriminals to earn money.

As a result, many cybercriminal groups have switched to malicious miner distribution, and the number of users that have encountered cryptocurrency miners has increased dramatically. We have found, that by the end of 2017, 2.7 million users had been attacked by malicious miners – this is almost 1.5 times higher than in 2016 (1.87 mln).

![](https://i.imgur.com/lcGZWGH.png)

*Number of Kaspersky Lab users attacked by malicious miners in 2017*

They become so active and popular that even ransomware – which has frightened the world for the last couple of years, seems to step aside for this threat.

Here are some reasons why:

Firstly, miners and ransomware both have a clear monetization model. In the case of ransomware, attackers infect PCs, decrypt files and earn money by receiving a ransom for users’ data. The miners model is similar in its simplicity: attackers infect victims, make coins using CPU or GPU power, and earn real money through legal exchanges and transactions.

![](https://i.imgur.com/EYqaQGu.png)

*Miners’ monetization scheme*

Secondly, unlike ransomware, it is very hard for users to understand if they’ve been infected by miners or not. In general, users use their computer for Internet surfing. This activity is not high loaded for CPU. The other 70-80% of CPU power is used by mining programs, and some of them have special functions to reduce mining capacities or cancel the process at all, if another resource-demanding program (for example, a videogame) is executed.

Most importantly, it is now very easy to make your own miner. Those interested can get everything that they need:

* Ready to use partner programs
* Open mining pools
* A lot of miner builders
We have found that the most popular miner pool used by threat actors is Nanopool.

![](https://i.imgur.com/n4uHoRy.png)

*Statistics for used legitimate pools*

If actors use open pools, it’s possible to find out how much money threat actors could earn.

![](https://i.imgur.com/b6B3Uj7.png)

*Example of wallet information*

Also, according to our data, 80% of illegal miners contain the open source code of legal miners, or it is just a legal miner that has been packed.

## Ways of spreading

Usually, threat actors collaborate with potentially unwanted application (PUA) partner programs to spread miners. However, some small criminal groups try to spread malware by using different social engineering tricks, such as fake lotteries, etc. Potential victims need to download a generator of random numbers from a file-sharing service and run this on a PC to participate. It’s a simple trick, but a very productive one.

Another popular method is web-mining through a special script being executed in browser. For example, in 2017 our security solutions [stopped](https://www.kaspersky.com/blog/web-miners-protection/20556/) the launch of web miners on more than 70 million occasions. The most popular script used by cybercriminals is Coinhive, and usual cases of its use in the wild are websites with a lot of traffic. The longer the user session on those sites, the more money the site’s owner earned from mining. Major incidents involving Coinhive are hacked web pages, such as the Pirate Bay case, [YouTube ads](https://www.kaspersky.com/blog/miners-in-youtube-ads/21025/) or [UFC fight pass](https://np.reddit.com/r/MMA/comments/7b4zdk/fight_pass_is_shady_ysk_ufc_fight_pass_is_using/dpf96js/) mining. However, other examples of its legal use are also known.

There are other groups, which do not need to spread miners to many people. Instead, their targets are powerful servers in big companies. Thus, for instance, [Wannamine](https://www.pandasecurity.com/mediacenter/mobile-news/wannamine-cryptomining-malware/) was spreading in internal networks using an EternalBlue exploit, and earned nine thousand Monero this way (approx. two million dollars). However, the first miner that used the EternalBlue exploit was [Adylkuzz](https://www.proofpoint.com/us/threat-insight/post/adylkuzz-cryptocurrency-mining-malware-spreading-for-weeks-via-eternalblue-doublepulsar). In our previous [research](https://securelist.com/miners-on-the-rise/81706/) we described another miner family – Winder – that has used an extra service to restore a miner when it was being deleted by an AV product. That botnet earned a half million dollars.

## Sophisticated techniques

This year we are observing the next trend – threat actors behind miners have begun to use malware techniques from targeted attacks. Our latest discovery is the “hollow” miner that uses a process-hollowing technique.

In this case the infection vector is a PUA module. A victim may have just wanted to download a legitimate application, but instead they downloaded a PUA with a miner installer inside. This miner installer drops the legitimate Windows utility *msiexec* with a random name, which downloads and executes a malicious module from the remote server. In the next step it installs a malicious scheduler task which drops the miner’s body. This body executes the legitimate system process and uses a process-hollowing technique (legitimate process code is changed to malicious). Also, a special flag, system critical flag, is set to this new process. If a victim tries to kill this process, the Windows system will reboot. So, it is a challenge for security solutions to deal with such malicious behavior and detect the threat properly.

![](https://i.imgur.com/2gZ5sCq.png)

*Infection chain*

![](https://i.imgur.com/LAQrxqk.png)

*Process hollowing example*

Using such sophisticated technique, botnets earned over seven million dollars during the second half of 2017.

Also this year, we found one threat group that has been targeting big organizations with the main purpose to utilize their computer resources for mining. After getting into a corporate network they get access to the domain controller, and as a result they use domain policies to launch malicious code. In this particular case, actors executed malicious PowerShell script on each endpoint and server inside the corporate network.

![](https://i.imgur.com/Mpchfmn.png)

*Malicious powershell script*

This script has the following logic:

* After launching, it checks if this endpoint belongs to specific accounts, i.e. senior levels or information security officers. If it is true, then the script won’t execute the miner.
* This script also checks current date and time information. It will execute the malicious miner in non-working time.
## So what’s next?

Should we expect a further evolution in this class of malware? For sure. Moreover, we will see a spread in malware that uses new blockchain technologies. One of the recent and very promising technologies is the blockchain-based proof-of-space (PoSpace) concept.

Unlike proof-of-work (PoW) used in general mining botnets, a PoSpace algorithm needs a hard disk space. Therefore, a new type of miners based on this algorithm will be aiming first of all at big data servers.

On the one hand, monetization in this case is like that in usual malware miners with a PoW algorithm. On the other, this technology can provide cybercriminals with another profit. The blockchain on the PoS algorithm is a very big decentralized anonymous data center that can be used to spread malware or illegal content. As a result, it can bring more damage. Data will be encrypted and no one will know where it is physically stored.

![](https://i.imgur.com/0p9QYWV.png)

*Mining scheme based on proof-of-concept algorithm*

To protect your network against such threats we advise you:

* Conduct a security audit on a regular basis
* Use security solutions on endpoints and servers
Kaspersky Lab products detect such threats with various verdicts.

* PDM:Trojan.Win32.Generic
* not-a-virus:RiskTool.Win32.BitCoinMiner
* HEUR:Trojan.Win32.CoinMiner

[Mining is the new black](https://securelist.com/mining-is-the-new-black/84232/)