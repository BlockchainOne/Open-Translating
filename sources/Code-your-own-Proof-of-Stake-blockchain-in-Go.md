# Code your own Proof of Stake blockchain in Go!

![](https://i.imgur.com/LjKGMrb.png)

*Questions about the following tutorial? Why wait? Join us in our* [Telegram](https://t.me/joinchat/FX6A7UThIZ1WOUNirDS_Ew) *chat!*

In our [last post](https://medium.com/@mycoralhealth/code-your-own-blockchain-mining-algorithm-in-go-82c6a71aba1f), we talked about what Proof of Work was and showed you how to code your own Proof of Work blockchain. The 2 most popular cryptocurrencies, Bitcoin and Ethereum are both based on Proof of Work.

But what are the downsides of Proof of Work? One of the major ones is electricity consumption. There is a race to set up bigger and bigger mining rigs to get the hardware power needed to mine more bitcoin. Check out the madness for yourself in this photo of a mining setup:

![](https://i.imgur.com/gYHR415.png)

This costs an insane amount of electricity. Bitcoin mining alone [consumes more energy](https://powercompare.co.uk/bitcoin/) than 159 countries! This is pretty irresponsible. However, from a technological perspective there are other downsides to Proof of Work. As more and more people participate in mining, the difficulty of the consensus algorithm needs to go up, creating a need for more hashing power. This means blocks and transactions take longer to get processed and get more expensive to mine. Proof of Work is a race to the bottom.

There are many thought leaders trying to find alternatives to Proof of Work. The most promising one so far is Proof of Stake. There are already production-ready blockchains based on Proof of Stake like [Nxt](https://nxtplatform.org/what-is-nxt/) and [Neo](https://neo.org/). Ethereum is probably moving to Proof of Stake — their [Casper](https://github.com/ethereum/research/wiki/Casper-Version-1-Implementation-Guide) project is already live on their test net.

**So what the heck is Proof of Stake?**

Instead of nodes competing with each other to solve hashes, in Proof of Stake, blocks are “minted” or “forged” (there is no “mining” so we don’t use that word in Proof of Stake) based on the amount of tokens each node is willing to put up as collateral. These nodes are called **validators**. **We will be using the terms “nodes” and “validators” interchangeably in this tutorial.** The tokens are specific to the blockchain. So in Ethereum, each node (validator) would put up Ether as collateral.

The more tokens each validator is willing to put up as collateral, the greater the chance they have to forge the next block and receive a reward. You can think of this as deposit interest. The more money you put in your savings account at your bank, the greater the monthly interest payment you receive.

Similarly, your probability of forging the next block increases the more tokens you put up as collateral. You are “staking” your tokens, which is why this consensus mechanism is called Proof of Stake.

**What are the downsides to Proof of Stake?**

You can probably already guess that a validator who has an excessively large amount of tokens staked will enjoy a disproportionately high probability of forging new blocks. However, this isn’t really different from what we see in Proof of Work. Bitcoin mining farms are [getting so powerful](https://interestingengineering.com/bitcoin-mining-company-bitmain-made-almost-4-billion-in-profits-in-2017) that regular people haven’t been able to mine on their own laptops in years. Thus, many people argue that Proof of Stake is actually more democratized since anyone can at least participate on their own laptops without setting up a giant mining rig. They don’t need expensive hardware, just enough tokens to stake.

There are other downsides to Proof of Stake, both from a technological and economic standpoint. We won’t get into all of them here but [here](https://bitcoin.stackexchange.com/questions/25743/what-are-the-downsides-of-proof-of-stake) is a nice intro. In reality, Proof of Stake and Proof of Work both have their strengths and projects like Ethereum’s Casper blends features from both.

As always, the best way to understand how Proof of Stake works is to write your own code!

We recommend checking out our [networking tutorial](https://medium.com/@mycoralhealth/part-2-networking-code-your-own-blockchain-in-less-than-200-lines-of-go-17fe1dad46e1) before proceeding. It’s not compulsory but in some parts of the following tutorial we will be moving quickly, so it will help you to review it.

**Caveats**

Our blockchain will implement the core concepts of Proof of Stake. However, because we need to be reasonable with length, the following production-level elements of a Proof of Stake blockchain will be left out. If you’d like to see any of these in the future, make sure to let us know in our [Telegram](https://t.me/joinchat/FX6A7UThIZ1WOUNirDS_Ew) chat!

* *Full peer-to-peer implementation*. Networking is simulated and the central blockchain state is held by a single Go TCP server. In this tutorial, the state is broadcast to each node from the single server.
* *Wallet and balance tracking*. We have not implemented a wallet in this code. Nodes are spun up in the network and the token amount is inputted in `stdin`. So you can type in any amount you want. A full implementation would associate each node with a hash address and keep track of token balances in each.
**Architecture**

![](https://i.imgur.com/3emkVX3.png)

* We’ll have a Go-based TCP server to which other nodes (validators) can connect.
* The latest blockchain state will get broadcast to each node periodically.
* Each node will propose new blocks.
* Based on the number of tokens staked by each node, one of the nodes will be randomly (weighted by the number of tokens staked) chosen as the winner, and their block will get added to the blockchain.
**Setup and Imports**

Before starting to write the code, we need to set an environment variable so our TCP server knows which port to use. Let’s create a  `.env` file in our working directory with one line in it:

`ADDR=9000`

Our Go program will read from this file and know to expose port 9000 so our nodes can connect to it.

Now let’s create a `main.go` file in our working directory and start coding!

As usual, let’s make our package declaration and write up the imports we’ll need.

* `spew` is a convenient package that pretty prints our blockchain to the terminal
* `godotenv` allows us to read from our  `.env` file we created earlier
**Quick pulse check**

If you’ve read our other tutorials, you’ll know at this stage we want to take our pulse. We’re a healthcare company so when we’re adding data to our blocks let’s not pick something boring like Bitcoin amounts. *Put two fingers on your wrist and count how many times you feel your pulse in a minute*. This is going to be your `BPM` integer we’ll use throughout the tutorial.

**Global variables**

Now let’s declare all our global variables we’ll need.

``` go
// Block represents each 'item' in the blockchain
type Block struct {
    Index     int
    Timestamp string
    BPM       int
    Hash      string
    PrevHash  string
    Validator string
}

// Blockchain is a series of validated Blocks
var Blockchain []Block
var tempBlocks []Block

// candidateBlocks handles incoming blocks for validation
var candidateBlocks = make(chan Block)

// announcements broadcasts winning validator to all nodes
var announcements = make(chan string)

var mutex = &sync.Mutex{}

// validators keeps track of open validators and balances
var validators = make(map[string]int
```

* `Block` is the content of each block
* `Blockchain` is our official blockchain, that is simply a series of validated blocks. The `PrevHash` in each block is compared to the `Hash` of the previous block to make sure our chain is robust. `tempBlocks` is simply a holding tank of blocks before one of them is picked as the winner to be added to `Blockchain`
* `candidateBlocks` is a channel of blocks; each node that proposes a new block sends it to this channel
* `announcements` is a channel where our main Go TCP server broadcasts the latest blockchain to all the nodes
* `mutex` is a standard variable that allows us to control reads/writes and prevent data races
* `validators` is a map of nodes and the amount of tokens they’ve staked
**Basic blockchain functions**

Before proceeding with our Proof of Stake algorithms, let’s write up our standard blockchain functions. This should be review if you’ve seen our [previous tutorials](https://medium.com/@mycoralhealth/code-your-own-blockchain-in-less-than-200-lines-of-go-e296282bcffc?source=user_profile---------13----------------). If you haven’t, that’s ok but we’ll be going through this quickly.

```go
// SHA256 hasing
// calculateHash is a simple SHA256 hashing function
func calculateHash(s string) string {
    h := sha256.New()
    h.Write([]byte(s))
    hashed := h.Sum(nil)
    return hex.EncodeToString(hashed)
}

//calculateBlockHash returns the hash of all block information
func calculateBlockHash(block Block) string {
    record := string(block.Index) + block.Timestamp + string(block.BPM) + block.PrevHash
    return calculateHash(record)
}
```

We start with our hashing functions. `calculateHash` takes in a string and returns its SHA256 hash representation. `calculateBlockHash` hashes the contents of a block by concatenating all its fields.

``` go
// generateBlock creates a new block using previous block's hash
func generateBlock(oldBlock Block, BPM int, address string) (Block, error) {

    var newBlock Block

    t := time.Now()

    newBlock.Index = oldBlock.Index + 1
    newBlock.Timestamp = t.String()
    newBlock.BPM = BPM
    newBlock.PrevHash = oldBlock.Hash
    newBlock.Hash = calculateBlockHash(newBlock)
    newBlock.Validator = address

    return newBlock, nil
}
```

`generateBlock` is how a new block is created. The important fields we include in each new block are its hash signature (calculated by `calculateBlockHash` previously) and the hash of the previous block `PrevHash` (so we can keep the integrity of the chain). We also add a `Validator` field so we know the winning node that forged the block.

``` go
// isBlockValid makes sure block is valid by checking index
// and comparing the hash of the previous block
func isBlockValid(newBlock, oldBlock Block) bool {
    if oldBlock.Index+1 != newBlock.Index {
        return false
    }

    if oldBlock.Hash != newBlock.PrevHash {
        return false
    }

    if calculateBlockHash(newBlock) != newBlock.Hash {
        return false
    }

    return true
}
```

`isBlockValid` performs the `Hash` and `PrevHash` check to make sure our chain has not been corrupted.

**Nodes (Validators)**

When a validator connects to our TCP server, we need to provide it some functions that achieve a few things:

* Allow it to enter a token balance (remember for this tutorial, we won’t perform any balance checks since there is no wallet logic)
* Receive a broadcast of the latest blockchain
* Receive a broadcast of which validator in the network won the latest block
* Add itself to the overall list of validators
* Enter block data `BPM`  — remember, this is each validator’s pulse rate
* Propose a new block
We’ll write all this up in a `handleConn` function. Here it is. Don’t worry! We’ll walk you through it all.

``` go
func handleConn(conn net.Conn) {
    defer conn.Close()

    go func() {
        for {
            msg := <-announcements
            io.WriteString(conn, msg)
        }
    }()
    // validator address
    var address string

    // allow user to allocate number of tokens to stake
    // the greater the number of tokens, the greater chance to forging a new block
    io.WriteString(conn, "Enter token balance:")
    scanBalance := bufio.NewScanner(conn)
    for scanBalance.Scan() {
        balance, err := strconv.Atoi(scanBalance.Text())
        if err != nil {
            log.Printf("%v not a number: %v", scanBalance.Text(), err)
            return
        }
        t := time.Now()
        address = calculateHash(t.String())
        validators[address] = balance
        fmt.Println(validators)
        break
    }

    io.WriteString(conn, "\nEnter a new BPM:")

    scanBPM := bufio.NewScanner(conn)

    go func() {
        for {
            // take in BPM from stdin and add it to blockchain after conducting necessary validation
            for scanBPM.Scan() {
                bpm, err := strconv.Atoi(scanBPM.Text())
                // if malicious party tries to mutate the chain with a bad input, delete them as a validator and they lose their staked tokens
                if err != nil {
                    log.Printf("%v not a number: %v", scanBPM.Text(), err)
                    delete(validators, address)
                    conn.Close()
                }

                mutex.Lock()
                oldLastIndex := Blockchain[len(Blockchain)-1]
                mutex.Unlock()

                // create newBlock for consideration to be forged
                newBlock, err := generateBlock(oldLastIndex, bpm, address)
                if err != nil {
                    log.Println(err)
                    continue
                }
                if isBlockValid(newBlock, oldLastIndex) {
                    candidateBlocks <- newBlock
                }
                io.WriteString(conn, "\nEnter a new BPM:")
            }
        }
    }()

    // simulate receiving broadcast
    for {
        time.Sleep(time.Minute)
        mutex.Lock()
        output, err := json.Marshal(Blockchain)
        mutex.Unlock()
        if err != nil {
            log.Fatal(err)
        }
        io.WriteString(conn, string(output)+"\n")
    }

}
```

The first Go routine receives and prints out any announcements that come from the TCP server. These announcements will be who the winning validator is when one is chosen.

The section starting with `io.WriteString(conn, “Enter token balance:”)` allows the validator to enter the number of tokens he wants to stake. Then the validator is assigned a SHA256 address and that address is added to our global `validators` map we declared earlier, along with our new validator’s number of tokens staked.

We then enter `BPM` which is the validator’s pulse rate and create a separate Go routine to process our block logic. The following line is **important**:

`delete(validators, address)`

If the validator tries to propose a polluted block, in our case, a BPM that is not an integer, that throws an error and we immediately delete the validator from our list of validators. They are no longer eligible to forge new blocks and they lose their balance.

**This potential to lose your token balance is a major reason why Proof of Stake is generally secure. If you try to alter the blockchain for your benefit and you get caught, you lose your entire staked token balance. It’s a major deterrent for bad actors.**

We then create a new block with the `generateBlock` function from before and we send it to the `candidateBlocks` channel for further processing. Sending stuff into a channel uses this syntax:

`candidateBlocks <- newBlock`

The last `for` loop periodically prints the latest blockchain so each validator knows the latest state.

**Picking a Winner**

This is the meat of Proof of Stake logic. We need to write up how a winning validator is chosen; the higher the number of tokens they stake, the higher their probability should be to be chosen as the winner who gets to forge their block.

*For simplicity in our code, we will only make validators who propose new blocks eligible to be chosen as the winner. In traditional Proof of Stake, a validator can be chosen as the winner even if they don’t propose a new block. Remember, Proof of Stake isn’t a definition, it’s a concept; there are lots of different implementations of Proof of Stake and like Proof of Work, each implementation has its own nuances.*

Here is our `pickWinner` function. We’ll walk you through it:


``` go
// pickWinner creates a lottery pool of validators and chooses the validator who gets to forge a block to the blockchain
// by random selecting from the pool, weighted by amount of tokens staked
func pickWinner() {
    time.Sleep(30 * time.Second)
    mutex.Lock()
    temp := tempBlocks
    mutex.Unlock()

    lotteryPool := []string{}
    if len(temp) > 0 {

        // slightly modified traditional proof of stake algorithm
        // from all validators who submitted a block, weight them by the number of staked tokens
        // in traditional proof of stake, validators can participate without submitting a block to be forged
    OUTER:
        for _, block := range temp {
            // if already in lottery pool, skip
            for _, node := range lotteryPool {
                if block.Validator == node {
                    continue OUTER
                }
            }

            // lock list of validators to prevent data race
            mutex.Lock()
            setValidators := validators
            mutex.Unlock()

            k, ok := setValidators[block.Validator]
            if ok {
                for i := 0; i < k; i++ {
                    lotteryPool = append(lotteryPool, block.Validator)
                }
            }
        }

        // randomly pick winner from lottery pool
        s := rand.NewSource(time.Now().Unix())
        r := rand.New(s)
        lotteryWinner := lotteryPool[r.Intn(len(lotteryPool))]

        // add block of winner to blockchain and let all the other nodes know
        for _, block := range temp {
            if block.Validator == lotteryWinner {
                mutex.Lock()
                Blockchain = append(Blockchain, block)
                mutex.Unlock()
                for _ = range validators {
                    announcements <- "\nwinning validator: " + lotteryWinner + "\n"
                }
                break
            }
        }
    }

    mutex.Lock()
    tempBlocks = []Block{}
    mutex.Unlock()
}
```

We pick a winner every 30 seconds to give time for each validator to propose a new block. Then we need to create a `lotteryPool` that holds addresses of validators who could be chosen as our winner. Then we check to see there actually are some blocks proposed in our temporary holding tank of proposed blocks with `if len(temp) > 0` before proceeding with our logic.

In the `OUTER` `for` loop, we check to make sure we haven’t already come across the same validator in our `temp` slice. If we do, skip over the block and look for the next unique validator.

In the section starting with `k, ok := setValidators[block.Validator]` we make sure the validator we get from our block data in `temp` is actually an eligible validator that sits in our `validators` map. If they exist, then we add them to our `lotteryPool`  .

*How do we assign proper weights to them based on the number of tokens they staked?*

* We fill our `lotteryPool` with copies of the validator’s address. They get a copy for each token they’ve staked. So a validator who put in 100 tokens will get 100 entries in the `lotteryPool`. A validator who only put in 1 token will only get 1 entry.
We randomly pick the winner from our `lotteryPool` and assign their address to `lotteryWinner`.

We then add their block to our blockchain and announce the winner to the rest of the nodes who won the lottery with this syntax, which sends the message into the `announcements` channel:

`announcements <- “\nwinning validator: “ + lotteryWinner + “\n”`

We clear out our `tempBlocks` holding tank so it can be filled again with the next set of proposed blocks.

That is the core of a Proof of Stake consensus algorithm! That wasn’t so bad was it?

**Almost there!**

Let’s wire up our `main` function now. Here it is:

``` go
func main() {
    err := godotenv.Load()
    if err != nil {
        log.Fatal(err)
    }

    // create genesis block
    t := time.Now()
    genesisBlock := Block{}
    genesisBlock = Block{0, t.String(), 0, calculateBlockHash(genesisBlock), "", ""}
    spew.Dump(genesisBlock)
    Blockchain = append(Blockchain, genesisBlock)

    // start TCP and serve TCP server
    server, err := net.Listen("tcp", ":"+os.Getenv("ADDR"))
    if err != nil {
        log.Fatal(err)
    }
    defer server.Close()

    go func() {
        for candidate := range candidateBlocks {
            mutex.Lock()
            tempBlocks = append(tempBlocks, candidate)
            mutex.Unlock()
        }
    }()

    go func() {
        for {
            pickWinner()
        }
    }()

    for {
        conn, err := server.Accept()
        if err != nil {
            log.Fatal(err)
        }
        go handleConn(conn)
    }
}
```

We start by slurping in the contents of our  `.env` file which is just the port number we’ll use for our TCP server. We then create a `genesisBlock` that new blocks will get added to, to form our blockchain.

We start our TCP server and expose the port in our  `.env` file to which new validators can connect.

We start up a Go routine to take blocks out of our `candidateBlocks` channel and fill our `tempBlocks` holding tank with them, for further processing by our `pickWinner` function we just wrote. We then start up another Go routine for the `pickWinner` function.

The last `for` loop accepts connections from new validators.

Check out the full code here:

What we just accomplished is pretty cool. We wrote up a robust Proof of Stake consensus algorithm from scratch and integrated it with actual TCP networking.

Let’s try this out! Open a terminal window and start up your Go program and TCP server with `go run main.go`  . As expected, we get our `genesisBlock` printed on our console.

![](https://i.imgur.com/JIrYNaz.png)

Now let’s fire up a validator. Open a **new** terminal window and connect to our TCP server with `nc localhost 9000`

We’re then prompted to add a token balance to stake. Enter the number of tokens you want that validator to stake. Then input a pulse rate for that validator.

![](https://i.imgur.com/qQQi2Zv.png)

Since we can have many validators, let’s do the same thing with **another** terminal window.

![](https://i.imgur.com/TiGlMu5.png)

Watch your first terminal as you’re adding new terminals. We see validators get assigned addresses and we get a list of validators each time a new one is added!

![](https://i.imgur.com/MLDuV3d.png)

Wait a little while and check out your new terminals. What’s happening is that our program is spending some time picking a winner. And then boom! A winner is chosen!

![](https://i.imgur.com/JVd3opF.png)

In our case, the first validator was chosen (we can verify the validator’s address by comparing it to the list of validators printed in our main terminal).

Wait a little while again and boom! We see our new blockchain broadcast to all our terminals, with our winning validator’s block containing his `BPM` in the newest block! Cool, right?

![](https://i.imgur.com/8GODWO8.png)

You should be proud of getting through this tutorial. Most blockchain enthusiasts and many programmers have heard of Proof of Stake but couldn’t even begin to explain what it is. You’ve gone even further and actually built a Proof of Stake blockchain from scratch! You’re one step closer to being an expert in next generation blockchain technologies.

Because this is a tutorial, there is more we can do to make this a production ready blockchain. Things to explore next are:

* Read through our [Proof of Work](https://medium.com/@mycoralhealth/code-your-own-blockchain-mining-algorithm-in-go-82c6a71aba1f) tutorial and tinker with it to see if you can create a hybrid blockchain
* Add time chunks where validators have a chance to propose new blocks. Our version of the code lets validators propose new blocks anytime so some blocks may periodically get cut off from consideration
* Add full peer-to-peer capability. This would basically mean each validator would run its own TCP server as well as connecting to others. We would need to add in logic so each node can find each other. Read more about this [here](https://bitcoin.stackexchange.com/questions/3536/how-do-bitcoin-clients-find-each-other).
Check out our other tutorials too:

* Our first, basic blockchain tutorial in [less than 200 lines of Go](https://medium.com/@mycoralhealth/code-your-own-blockchain-in-less-than-200-lines-of-go-e296282bcffc)
* How to store files through the blockchain with [IPFS](https://medium.com/@mycoralhealth/learn-to-securely-share-files-on-the-blockchain-with-ipfs-219ee47df54c)
* [Blockchain networking](https://medium.com/@mycoralhealth/part-2-networking-code-your-own-blockchain-in-less-than-200-lines-of-go-17fe1dad46e1) (a big chunk of the tutorial you just read was based off this)
* Code your own [Proof of Work](https://medium.com/@mycoralhealth/code-your-own-blockchain-mining-algorithm-in-go-82c6a71aba1f)
**To learn more about Coral Health and how we’re using the blockchain to advance personalized medicine research, visit our** [website](https://mycoralhealth.com/) **and follow us on** [Twitter](https://twitter.com/myCoralHealth) **.**

[Code your own Proof of Stake blockchain in Go!](https://medium.com/@mycoralhealth/code-your-own-proof-of-stake-blockchain-in-go-610cd99aa658)