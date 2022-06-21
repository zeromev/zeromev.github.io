* TOC
{:toc}

NOTE:  THIS SITE IS UNDER CONSTRUCTION AND UNDER DEVELOPMENT AND HAS NOT YET BEEN RELEASED

# tl;dr

Ethereum miners and validators have unchecked power to take money from you by [frontrunning](#frontrunning) and [censoring](#censorship) your transactions.

Protect yourself from this today by taking [these steps](#users).

# about us

Zeromev is an organization that aims to protect Ethereum users from [frontrunning](#frontrunning) and [censorship](#censorship).

Hundreds of millions of dollars have already been lost by users to such exploits, which is often called Miner Extractable Value (MEV).

We aim to:

*   __Empower Users__ by providing information to help users understand and avoid harmful MEV.
*   __Protect Users__ by researching and advocating for genuinely preventative protocol level solutions.

We have been funded with a grant from the [Ethereum Foundation](https://www.ethereum.org).

Our flagship product is the [Zeromev Frontrunning Explorer](#frontrunning-explorer) which gives users and researchers detailed information on [transaction reordering](#transaction-reordering) and [MEV](#miner-extractable-value).

Zeromev was founded by the pseudo-anonymous researcher [pmcgoohan](https://twitter.com/pmcgoohanCrypto) who first alerted the community to the vulnerability we now call MEV in their 2014 post [Miners Frontrunning](https://www.reddit.com/r/ethereum/comments/2d84yv/miners_frontrunning).

# the problem

Individual miners and validators have full control over which transactions go in their blocks and where.

This permits all kinds of frontrunning and censorship attacks that are harmful and costly to users and illegal in regulated markets.

These attacks may be performed directly by the miner, or the miner may be bribed to do so via the Ethereum gas price auction (GPA) mechanism or increasingly in a MEV auction, although any means of bribery can be used.

In 2014 (pre-genesis), the pseudo-anonymous [founder of zeromev](https://twitter.com/pmcgoohanCrypto) alerted the community to this vulnerability in their post [Miners Frontrunning](https://www.reddit.com/r/ethereum/comments/2d84yv/miners_frontrunning).

In 2019, the seminal paper [Flashboys 2.0](https://arxiv.org/abs/1904.05234) coined the phrase MEV (Miner Extractable Value) to describe how miners profit from this centralized, trusted power that they have over users in the Ethereum network, which still persists today.

Hundreds of millions of dollars have already been taken from Ethereum users in this way. Left unchecked, we expect the problem to [worsen intolerably](https://www.coindesk.com/tech/2021/05/10/why-ethereums-miner-extractable-value-problem-is-way-worse-than-you-think). 

Zeromev aims to eradicate [toxic MEV](#toxic-mev) involving frontrunning and censorship.

# definition of terms

The definition of terms used by zeromev in the context of Miner Extractable Value (MEV) in Ethereum.

## miners

The miners in Proof-of-Work Ethereum, each of which gets exclusive choice over which transactions go in their blocks and in what order. If validators are not specifically mentioned in the same context, it also includes validators which are the equivalent in Proof-of-Stake Ethereum. Where bribery ordering exists in other domains such as L2s, it may also refer to L2 validators/sequencers.

## miner extractable value

The profit that can be extracted from users by miners using the centralized and trusted power they have to pick and order transactions in their blocks.

## frontrunning

Frontrunning is the ability of miners to insert transactions before a victim transaction for profit. Examples of this include [sandwich attacks](#sandwich-attacks) (see [toxic MEV](#toxic-mev)).

## censorship

Censorship is the ability of miners to delay the execution of a user transaction for profit. Examples of this behaviour include [NFT sniping](#nft-sniping) and [toxic liquidations](#toxic-liquidations) (see [toxic MEV](#toxic-mev)). 

If the inclusion of a transaction on chain is delayed for long enough that its final state is altered or it fails (reverts), we consider that transaction to have been censored.

## toxic mev

[Toxic MEV](#toxic-mev) is the loss incurred to users by miners frontrunning or censoring their transactions.

The hallmark of toxic MEV is miners reordering user transactions for their own profit.

It is a consequence of block building being centralized and trusted in Ethereum. This permits both direct exploitation by the miner and by other parties that bribe the miner to do so.

Despite sandwich attacks being the only clearly toxic MEV type currently identified by zeromev, they alone represent the majority of all MEV quantified.

Once nft sniping, liquidity sandwiching, toxic arbitrage, toxic liquidations, censorship-as-a-service and other as yet undetected toxic MEV types are quantified, more benign forms of MEV not involving reordering may be revealed to be a tiny minority of the total. 

### sandwich attacks

Sandwich attacks are particularly exploitative reordering attacks and account for the majority of currently quantified MEV on Ethereum. 

They commonly occur on DEXs (distributed exchanges) where they involve the frontrunning of an order to manipulate the price against it followed by a backrun enabling the attacker to profit at the victim's expense.

They may also involve an aspect of censorship where the sandwiched transaction is delayed until conditions are right for it to be exploited.

[This example](https://twitter.com/pmcgoohanCrypto/status/1510977122931822605?s=20&t=kPfQHgygmugIF7tib0qLOw) clearly shows an attacker frontrunning and then backrunning a user order for profit. It also shows the victim order having been delayed by 1 mins 43 secs before the attack takes place while the miner's frontrun and backrun are inserted in the block instantaneously by the miner.

Sandwich attacks were predicted [here](https://www.reddit.com/r/ethereum/comments/2d84yv/comment/cjnxw78/?utm_source=share&utm_medium=web2x&context=3) by zeromev founder [pmcgoohan](https://twitter.com/pmcgoohanCrypto) in 2014 in the context of on-chain order book exchanges.

#### pool imbalance attack

A pool imbalance attack is a sub-class of sandwich attack in which the relative size of distributed exchange liquidity pools are switched in the frontrun and reset in the backrun such that the victim may recieve almost nothing in return for their currency when executing an order.

[This example](https://twitter.com/pmcgoohanCrypto/status/1512070425748017158?s=20&t=K2251p60Y2pC2gZQv1fKug) shows such an attack returning the user 124659361459800% less than expected in what was likely a trap set and bait by the attacker.

### liquidity sandwiching

Liquidity sandwiching is an attack against liquidity providers on distributed exchanges such as Uniswap v3 that allow for the provision of liquidity at margin. 

It involves frontrunning a user order with a very high volume of leveraged liquidity over a very tight range, after which this liquidity is withdrawn in the backrun. While users benefit from superior execution in this case, other liquidity providers lose out to this frontrunning activity as their liquidity is greatly diluted by the attacker.

While in traditional markets providing such a high volume of concentrated liquidity would create an unacceptable risk of loss due to margin calls, the ability to precisely target the frontrun and backrun by bribing the miner makes this nearly zero risk for the attacker.

### toxic arbitrage

Arbitrage involves profiting from the price difference of the same asset across different marketplaces.

Arbitrage may be considered neutral MEV similar to latency arbitrage in traditional financial markets, although many arbitrage opportunities likely fall far outside the limits that would be imposed if DEXs were operating under NBBO (national best bid and offer) rules, for example this [arb for $2.4 million](https://twitter.com/bertcmiller/status/1536353430717046786).

Unlike straightforward arbitrage, toxic arbitrage involves an attacker reordering user transactions on the same pair before their backrun and/or censoring them until after their backrun, such that an imbalance is first artifically created and then exploited by the attacker.

Zeromev cannot currently diffentiate toxic and neutral arbitrage, although there are plans to do this. Until then arbitrage is considered as unclassified by zeromev.

### nft sniping

NFT sniping is the practice of seeing a bid on an NFT and frontrunning and/or censoring it such that the attacker wins the auction instead.

As well as the frontrunning and censorship involved, it also creates inefficient marketplaces as the miner takes a large volume of the total amount paid in bribes that could otherwise have gone to the artist.

Such activity is known about but not yet quantified by zeromev.

### toxic liquidations

Liquidations are performed by when a trader's leveraged position is forcibly closed due to a partial or total loss of the trader's initial margin. The transaction performing the liquidation is rewarded with a fee.

This becomes toxic if a trader's attempt to recollateralize their loan to avoid liquidation is censored, or if the price is manipulated by reordering DEX transactions so that a liquidation is triggered when it otherwise would not have been.

Zeromev cannot currently diffentiate toxic and neutral liquidations. Until then, liquidations are considered as unclassified by zeromev.

### censorship-as-a-service

Censorship-as-a-service (Caas) involves bribing miners not just to include your transaction, but to exclude the transactions of other users.

CaaS is a vital and active area of research for zeromev because it is facilitated by the upcoming adoption of full-block mev auctions on Ethereum and the centralization of block building that they incentivize.

A fully operating CaaS market would create a perfectly extortionate economy where users pay close to the maximum they are willing to for every transaction, and in many cases a great deal more.

Those that believe that all MEV will (or even should) be extracted inadvertently believe that CaaS markets are inevitable in Ethereum, as it is simply another form of MEV.

CaaS is not yet quantified by zeromev.

### others

Miners having full control over transaction inclusion and ordering in every Ethereum use case creates a potentially unlimited number of possibilities for toxic MEV attacks.

The list above is far from exhaustive and will expand over time and as the use cases for Ethereum expand.

## unclassified mev

Zeromev cannot currently differentiate toxic and neutral cases of some MEV types, including arbitrages and liquidations.

Because zeromev captures global timing data for each Ethereum transaction, we are in a good position to detect when miners use their power to reorder and censor transactions. This is the hallmark of toxic MEV. Until then, arbitrages and liquidations are considered unclassified by zeromev.

## transaction reordering

There is an objective measure of how corrupt a transaction order has become, which is divergence from send time order (the time at which a user sent their transaction for processing).

The closer a transaction order is to send time order, the less corrupt it is. The further it is from send time order, the more corrupt. Perfect send time order is by definition free from all Toxic MEV.

This [video](https://youtu.be/zf2l3veT9EI) introduces the concept.

# comparison with traditional markets

Comparisons are often made between MEV on Ethereum and HFT (High Frequency Trading) in the financial markets. For a number of reasons, these comparisons are often flawed, with MEV having far more severe negative user impacts.

##  read/write (MEV) vs read only (HFT)

On traditional exchanges such as the NASDAQ and the NYSE, orders are given timestamps at the gateway of the exchange which are then respected throughout the system. Until they have been executed against the order book they are not publicly visible and so cannot be frontrun or censored.

In Ethereum, orders are typically sent to the public mempool. Miners can then not only choose from this pool of visible transactions which to include, they can insert their own where they choose around them, or not include them at all.

This gives miners an opportunity to frontrun and censor transactions to an extent for which there is no direct equivalent in traditional finance.

## bribery vs time ordering

Ethereum uses a mechanism of bribing miners to include transactions. While this is effective for situations where transaction order does not impact state (eg: sending some currency to someone) it is inefficient where transaction order does impact state (eg: an order sent to a DEX or a bid for an NFT).

In the latter case, bribery ordering  devolves into what are now called GPA (gas price auction) wars which impact network performance and maximize the cost of doing business on Ethereum.

Traditional exchanges are not permitted to accept bribes to reorder transactions, and it is highly unlikely that the NYSE would stand the retail, regulatory and legal pressure that would be applied if they did.

## dark pool

If instead users choose to bypass the mempool, they can submit to a third party to include on chain. However firstly they must trust this unregulated third party to include them in a timely fashion and not to frontrun them.

Secondly, that third party must still ultimately trust the miners. The miners still have absolute power to frontrun them (note: in Mev-boost, this power falls to the builders and relayers are validators are blinded as to the content of blocks).

Conversley, dark pools in traditional markets are bound by NBBO prices and best execution regulations.

## latency

Only latency advantages, mev has both (private network services exist to give latency advantages to extractors).

## order flow

## regulatory / legal environment

Traditional markets are regulated by a number of different laws and agencies which are designed to prevent frontrunning and censorship of the kind found in Ethereum.

These include but are not limited to Wire Fraud laws, Rule 611, NBBO prices and Best Execution regulations.

Trade on NASDAQ/NYSE via a direct-access broker and you avoid order flow completely at reasonable cost, or choose Robinhood and still get filled within NBBO prices with marginally inferior execution but pay no fees. Absolutely no sandwiching in either case.

The equivalent situation would be if the NASDAQ allowed orders to be made visible for 12 seconds and sold the right to frontrun and censor them to the highest bidder, a situation which is clearly unacceptable under current laws and regulations.

U.S. Attorney Damian Williams said:  “NFTs might be new, but this type of criminal scheme is not… Today’s charges demonstrate the commitment of this Office to stamping out insider trading – whether it occurs on the stock market or the blockchain.”

SEC: “Rule 611 will be assessed based on the time that orders and quotations are received…” which implies sandwichers are bribing to induce trade-throughs

Best Execution / NBBO prices.

While we are not in a position to offer legal advice on the applicability of these laws to cryptocurrency and Ethereum, it is clear that frontrunning and censorship is not tolerated in traditional finance making it close to impossible that users of traditional finance will be exploited in this way.

# a way forward

The following thoughts on reducing toxic MEV are written in good faith based on many years worth of study in this area. Zeromev always encourages people to do their own research, and will under not under any circumstances take responsibility for losses.

## users

A possible way forward for users looking to avoid or reduce toxic MEV.

### use marketplaces on first-come-first-serve (FCFS) layer 2

Toxic MEV such as sandwich attacks are the result of the unchecked power that miners have to exploit users by reordering and censoring transactions.

By finding environments where this is avoided or greatly reduced, toxic MEV can also be avoided or greatly reduced.

Layer 2 networks (L2s) have been designed to improve scaling on Ethereum. However, a well chosen and trustworthy L2 that employs first-come-first-serve (FCFS) or fair ordering may also be your best defense against toxic MEV. Using such an L2:

*   protects you from being exploited.
*   costs less in transaction fees.
*   reduces the centralizing effects of MEV on the Ethereum base layer.
*   reduces congestion on L1.
*   reduces the overall cost of gas on both Ethereum L1 and L2.

It's good for you, and it's good for the network.

It is important to note that most FCFS L2s are currently centralized. As such it is important to choose an L2 that you trust to order transactions equitably. However, this should not put you off, as miners and validators are also fully trusted for transaction ordering.

Some L2s manage very large volumes and so have high reputational collateral which would be put at risk if they were caught frontrunning users.

Miners, on the other hand, are also trusted for transaction ordering, but are unaccountable and anonymous. Worse, most now run software designed to maximize the exploitation of MEV opportunities, the majority of which is now known to harm users (see [mev-geth](https://github.com/flashbots/mev-geth)). 

The planned integration of [mev-boost](https://github.com/flashbots/mev-boost) with Ethereum consensus clients post-merge should be of special concern to users as it auctions off full blocks to be won by the bidder able to extract the most MEV out of them.

Zeromev intends to produce comparison data on the MEV performance of different L2s in due course.

Until then, we advise you to consider how committed to fair-ordering and frontrunning minimization different L2s are, and that you are aware of the MEV policy of any L2 you consider.

For example, Arbitrum has made it clear that front-running will not be tolerated whereas Optimism has looked to extract MEV from users by design.

### avoid ethereum layer 1 marketplaces

Layer 1 Ethereum is the main Ethereum network. If you have not moved your funds to a layer 2, this will be where you are transacting.

Where transaction order makes no difference to the outcome of a transaction (eg: sending Eth from one wallet to another), it is safe to transact on L1.

Where your transaction may execute differently when placed in a different order, L1 should be avoided if you want to avoid toxic MEV. Examples of this include distributed exchanges and NFT auction markets. Such activities may be best carried out on [fair ordered L2s](#transact-on-first-come-first-serve-FCFS-layer-2) as described above.

### be wary of layer 1 mev protections

If you do decide to use marketplace implementations and other order-sensitive smart contracts on Ethereum L1, understand that there are currently no dependable solutions to protect you from toxic MEV on L1. See [here](https://twitter.com/pmcgoohanCrypto/status/1516410063665127425?s=20&t=4VdFCo4IjKztveeJuZAeyg) for further explanation and examples.

L1 protections must rely on trusting miners who are the very actors that ultimately benefit from extracting MEV.

Due to profit maximization, miners will allow frontrunning protection if it makes them more money overall at the cost of users. If the toxic MEV dries up because of these protections, miners make more by defecting. In other words, miners are incentivized to make such protections fail at the point they start saving users money.

### speak up

Most of the research by Flashbots and the Ethereum Foundation over the last 2 years has been into various iterations of mev auctions which maximize MEV extraction. Precious little research has been commissioned into decentralizing block building and fair ordering by these organizations.

Voice your concerns about toxic MEV and the direction of Ethereum core developers and research and development organizations such as Flashbots.

Vote with your feet by using fair environments such as FCFS L2s.

## miners (pre merge)

In particular, do not run Flashbots mev-geth as this aims to maximize the amount of MEV extracted from users of the network, the majority of which is now known to involve frontrunning which is harmful to users.

## validators (post merge)

Under mev-boost, the builder that wins the block will be the one that can extract the most value from users because they'll be able to afford to pay the most in the block auction.

Our figures show that the majority of MEV in a block is extractable only by frontrunning. As such, a builder that refuses to frontrun will not be able to afford to win a block from one that does.

For this reason we do not consider mev-boost to be a neutral technology, as in this way it incentivizes builders to exploit users to the maximum possible extent.

Validators that choose to run mev-boost also give up any chance of resisting exploitative builders, because the content of prospective blocks is hidden from validators running mev-boost until they have committed to them.

Zeromev aims to supply the community with alternatives that reduce rather than exacerbate frontrunning and censorship and that do not potentially implicate validators in frontrunning and censorship.

## protocol designers

Mev auctions represent not just a risk to users, but also to the network itself.

Mev auctions without encrypted transactions make Ethereum about as secure as a public database of credit card details without a password, ie: perfectly and trivially exploitable.

FCFS ordering negates the bribery warfare of gas price auctions, thereby releasing blockspace and lowering user costs.

Another problem is the loss of auditability. FB auction data is proprietary, centralized and not publicly available (only the end result is), making Ethereum increasingly opaque.

Builder centralization.

### managed block building

In Ethereum today, miners and validators are fully trusted and centralized for block building.

The problem is that miners and validators have nothing to lose buy behaving in their own interests and against the interests of users because they are anonymous and without reputation.

We therefore consider interim solutions permitting a familiar, trusted and centralized actor with reputational collateral for transaction ordering to be superior to the status quo.

Arbitrum L2 is an example of an L2 which is fully trusted but with a large reputation and business operation to protect, so they are incentivized to behave over a validator.

Similarly, interm measures involving fair ordering or hiding of transactions by trusted parties are superior to the status quo and should be considered as an interim measure by protocol designers until block decentralization is solved satisfactoraly.

# zeromev frontrunning explorer

The zeromev frontrunning explorer gives clear and detailed visibility of Miner Extractable Value (MEV) and transaction reordering on the Ethereum network. Transaction reordering (frontrunning and censorship) is the root cause of toxic MEV.

All dates and times are in UTC (Coordinated Universal Time).

## walkthrough

Watch this short walkthrough of all the main features of the zeromev frontrunning explorer.

<iframe
    width="640"
    height="480"
    src="https://www.youtube.com/embed/zf2l3veT9EI"
    frameborder="0"
    allow="autoplay; encrypted-media"
    allowfullscreen
>
</iframe>

Or follow the steps yourself below:

### toxic MEV (3 mins)

*    [click here](https://www.zeromev.org/block?num=14959522) to jump to block number 14959522
*    there are 2 sandwich attacks at the top
*    'sandwich' is the victim transaction
*    'frontrun' and the 'backrun' are the attacking transactions which lost the user $-13199 in the first case
*    the 'frontrun' pushes up the price so the victim overpays
*    the 'backrun' allows the attacker to profit from this
*    hover over 'sandwich' for details
*    notice that the user loss is higher than the attacker's profit, which is typical
*    the delay column shows that the victim had to wait 1 min 58 secs to be included, only to be attacked when they were
*    hover over it to see the delay as measured by each zeromev node
*    hover over arrival time to see first time each zeromev node saw this transaction when it was pending

### heatmap (+2 mins)

*    look at the multi-coloured heatmap bar on the left under the 'block order' button
*    the colours are all mixed up because the time order of transactions in the block is mixed up too 
*    this is bad news because toxic MEV happens when miners order transactions by self-interest and not by time
*    click on 'fair order'
*    the heatmap is now showing that the transactions have been sorted in time order with the oldest first (light yellow), and the most recent last (dark black)
*    notice that the earliest transaction in the block was delayed by 17 mins 24 secs before being included
*    the sandwich attacks have disappeared, so what happened to them?
*    click on 'info' to see only transactions of interest
*    the victim sandwich transactions are at still near the top
*    scroll down and you'll see the attacking frontrun and backrun transactions now out of harms way at the bottom
*    had the block been ordered by time, neither of these sandwich attacks would have been possible and these 2 users would not have lost a combined $-14421.

### flashbots bundles (+1 min)

*    so how were these sandwich attacks performed with such precision?
*    scroll up and click on 'block order' and then 'all'
*    Flashbots provide a service allowing people to bribe miners to include bundles of their own and other people's transactions in whatever order they choose
*    the column with the robot icon shows that the first sandwich attack was sent in Flashbots bundle 2, and the second in bundle 3
*    this service makes sandwich attacks trivial to perform and riskless for the attacker because if they fail it costs them nothing
*    perhaps unsurprisingly, user losses from sandwich attacks increased after Flashbots released this service

### network performance (+1 min)

*    we can see that time ordering solves the problem of toxic MEV, but how accurately can we know time order in a distributed network like Ethereum?
*    see the delay box at the top of the page
*    it tells us that transactions were delayed by an average of 59 secs before being included
*    it also tell us that the oldest transaction in the block had to wait 17 mins 24 secs before being included
*    hover over it for details
*    now look at the network box
*    it shows us that the actual performance of the Ethereum peer-to-peer network had a delay of only 62 milliseconds at this time, far less than the our victim transactions were delayed by (around 2 minutes)

### summary

We have seen:

*    two sandwich attacks where the victim transactions were censored for around 2 minutes before being frontrun and backrun by their attackers for a loss of $-14421
*    that both attacks were enabled by Flashbots auctions
*    that fair ordering transactions would have made these attacks impossible
*    that the fair order of transactions in the network is usefully knowable

Now try putting your wallet address into the search box at the top, and seeing if you have been the victim of toxic MEV.

## search bar

At the top of each page is a search box.

As with most blockchain explorers, you can search for a block by Ethereum:
*   blocknumber
*   transaction hash
*   address

Having searched by transaction hash, a 'Jump To Tx' button allows you to quickly find the transaction in question in the block.

## home page

This shows recent users losses due to MEV in realtime. Figures are currently shown for both toxic MEV, which is harmful to users, and unclassified MEV which has not yet been differentiated into toxic or neutral MEV.

Click on 'Refresh' to get the most recent data available. It is normal for there to be a lag of a few minutes while blocks are processed and classified by the system.

Click on any block number to drill down into the details.

## block page

The block page is the heart of the zeromev frontrunning explorer.

The view it gives of transaction timing and MEV is unparalleled by other blockchain explorers.

See [walkthrough](#walkthrough) for more.

### heatmap

The time order heatmap is a key innovation of the zeromev frontrunning explorer. It lays bare the transaction reordering that underlies toxic MEV.

Light (yellow) indicates transactions that would have been included first in a block had it been fair ordered (ie: ordered by time), while dark (black) transactions would have been included last in a block.

Try clicking between the block order, gas order and fair order buttons to see the impact that different ordering schemes have on a block.

See [heatmap walkthrough](#heatmap-2-mins) for more.

#### heatmap calculation

The arrival time column shows the time at which a pending transaction was first seen by any one of the globally distributed zeromev nodes.

The delay is the difference between the time a pending transaction was first seen, and when it was included in the Ethereum blockchain.

From this we get the time column, which is where the transaction would have come in the block order had it been ordered by time.

A colour is given to each transaction based on the time column, with low numbers being light (yellow) and high numbers dark (black).

See [heatmap walkthrough](#heatmap-2-mins) for more.

### block box

Shows the block number along with a summary of MEV in the block, a transaction count, and the Eth price in USD at the time the block printed.

### delay box

Shows the average and maximum amount the transactions were delayed before being included in this block.

Hover over to see block arrival times for each zeromev node.

See [network performance](#network-performance-1-min) for more.

### network box

Shows the performance of the Ethereum peer-to-peer network and includes a count of the number of nodes used to collect the sample.

Hover over to see individual measurements for each zeromev node, as well as average and standard deviation calculations.

See [network performance](#network-performance-1-min) for more.

### ordering buttons

The ordering buttons allow you to try out different what-if orderings of transactions in a block.

#### block order

The original order of the block as determined by the miner.

#### gas order

The order of the block if sorted by gas price.

#### fair order

The order of the block if sorted by the first-seen arrival times of any of the globally distributed zeromev nodes.

See [heatmap walkthrough](#heatmap-2-mins) for more.

### filter buttons

Allow the user to filter the transaction table by different criteria.

#### all

Shows all transactions in the block.

#### info

Shows only transactions which zeromev has classified in some way.

As well as MEV types, this includes DEX swaps and NFTs purchases.

#### toxic

Shows only transactions which were the victim of MEV attacks and the transactions that attacked them.

#### other

Shows all MEV related transactions.

### transaction table

The transaction table shows every transaction in the block on a single page when 'all' is selected.

If you searched for a specific transaction or clicked on one from the address page, a 'Jump To Tx' button allows you to quickly find the transaction in question in the block.

Each column in the table is described below.

#### time

The index position of a transaction when ordered by time.

See [heatmap calculation](#heatmap-calculation) for more.

#### delay

The delay between when a transaction was first seen by any of the zeromev nodes and when it was executed and published in the block.

Hover over a delay value to see the delay measured by each individual zeromev node.

'miner' means that the transaction was not seen in the mempool of any of the zeromev nodes, and was likely inserted by the miner when they created the block.

#### mev

This gives details of MEV and other information.

*   Toxic MEV is in red (hover over for details).
*   Unclassified MEV is in grey (hover over for details).
*   Non MEV such as straightforward swaps and NFT trades are shown in light blue.

#### impact

Summarizes the loss to the user of an MEV instance.

#### action

Gives information about the execution of the transaction. It may include swaps, liquidations and NFT trades.

#### flashbots bundle

When populated, it shows that the transaction was inserted by the miner having been bribed for inclusion in a [Flashbots Bundle](https://docs.flashbots.net/flashbots-auction/searchers/advanced/understanding-bundles).

The first number is the Flashbots bundle number and the second is the index of the transaction within the bundle.

Examples:
2.1 is the first transaction in bundle 2.
4.6 is the sixth transaction in bundle 4.

Please note that while Flashbots Bundles are start from 0 in their API, Zeromev starts Flashbots Bundles from 1 as this is the same as the official [Flashbots Bundle Explorer](https://flashbots-explorer.marto.lol/).

#### transaction hash

A an abbreviated hash of the Ethereum transaction. Hover over for the full hash. Click to link to it on Etherscan.

#### arrival time

The arrival time column shows the time at which a pending transaction was first seen by any one of the globally distributed zeromev nodes.

Hover over a delay value to see the arrival times measured by each individual zeromev node.

#### from

The originating address of the transaction.

#### to

The destination address of the transaction.

#### value

The value in Eth of the transaction.

#### gas price

The bribe to the miner to include the transaction in the chain. The miner may also have been bribed for inclusion and priority in a [Flashbots Bundle](#flashbots-bundle) or by any other route.

Denominated in Gwei.

## address page

You can navigate to the address page by searching for a valid Ethereum address in the Search Box.

You can then page through all transactions made from this address. 

Clicking on a transaction hash here drills down into the block containing that transaction. A 'Jump To Tx' button allows you to quickly find the transaction in question in the block.

# zeromev extractor

# zeromev classifier

# research

# terms of service / disclaimer
 
