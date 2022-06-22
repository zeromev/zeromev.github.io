* TOC
{:toc}

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

#### position taking

Sandwich attacks are often used by the attacker to take a position on a currency at a preferential price. This was first predicted by the zeromev founder [pmcgoohan](https://twitter.com/pmcgoohanCrypto) in [this post](https://ethresear.ch/t/mev-auctions-will-kill-ethereum/9060).

If the attacker’s frontrun output does not equal their backrun input, then they will be left with a position.

If the frontrun is greater, then the attacker will end up with a position on the frontrun output token. This is very harmful because it worsens the price for the victim more than a balanced sandwich would. However, the impact of this is already accounted for by the user loss calculation. In these instances, user loss will often be much more sizeable than the attacker profit.

If the backrun is greater, then the attacker will end up with a position on the backrun output token. This excess is reported in brackets in the impact column of the backrun transaction, and in the hover over summary of the attack.

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

Censorship-as-a-service (Caas) involves bribing miners not to include your transaction, but to exclude the transactions of other users.

CaaS is a vital and active area of research for zeromev because it is facilitated by the upcoming adoption of full-block mev auctions on Ethereum and the centralization of block building that they incentivize.

A fully operating CaaS market would create a perfectly extortionate economy where users pay close to the maximum they are willing to for every transaction, and in many cases a great deal more.

Those that believe that all MEV will (or even should) be extracted inadvertently believe that CaaS markets are inevitable in Ethereum, as it is simply another form of MEV.

CaaS is not yet quantified by zeromev.

### others

Miners having full control over transaction inclusion and ordering in every Ethereum use case creates a potentially unlimited number of possibilities for toxic MEV attacks.

The list above is far from exhaustive and will expand over time and as the use cases for Ethereum expand.

## neutral mev

Straightforward arbitrage and liquidations that do not involve frontrunning and censorship to create opportunities or maximize a return are considered neutral or benign by zeromev.

Until MEV types can be differentiated into toxic and neutral MEV by zeromev, they are considered as [unclassified](#unclassified-mev).

## unclassified mev

Zeromev cannot currently differentiate toxic and neutral cases of some MEV types, including arbitrages and liquidations.

Because zeromev captures global timing data for each Ethereum transaction, we will be in a good position to detect when miners use their power to reorder and censor transactions, which is the hallmark of toxic MEV. Until then, arbitrages and liquidations are considered unclassified by zeromev.

Unclassified mev is labelled as 'other' MEV in the [frontrunning explorer](/explorer).

## transaction reordering

There is an objective measure of how corrupt a transaction order has become, which is divergence from send time order (the time at which a user sent their transaction for processing).

The closer a transaction order is to send time order, the less corrupt it is. The further it is from send time order, the more corrupt. Perfect send time order is by definition free from all [toxic MEV](#toxic-mev).

This [video](https://youtu.be/zf2l3veT9EI) introduces the concept.
