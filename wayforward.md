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
