![zeromev logo](/images/zeromevgethlogo.png)

ℹ️ please note: the latest version of this document can now be found [here](https://info.zeromev.org/zmgeth-proposal.html) ℹ️

# Zeromev-Geth: Unilateral Fair Ordering

## problem

The default transaction ordering in Ethereum results in validators being bribed to [frontrun](https://info.zeromev.org/terms.html#frontrunning) users.

This is worsened by [MEV-Boost](https://ethresear.ch/t/mev-boost-merge-ready-flashbots-architecture) which auctions off blocks to whichever builder is most profitable at frontrunning (and/or capturing [private order flow](https://ethresear.ch/t/two-slot-proposer-builder-separation/10980/10)).

There are currently no good options for validators wishing to avoid this moral and [legal jeopardy](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4187752). 

While robust solutions to this problem are possible with consensus changes[^1][^2], these are several years away at best. 

This document introduces an interim solution for individual validators wishing to act well and in a fully decentralized manner.

## overview

By changing a few lines of code, Geth can be made to order transactions by receive time instead of gas price.

*Validators using this fork will no longer be accepting bribes for frontrunning* (either via MEV Auctions or Gas Price Auctions).

### advantages
- **mitigates most frontrunning** because bribes of all kinds are ignored and [selfish reordering](https://info.zeromev.org/problem) is minimized
- **validators may not be legally culpable** for any frontrunning that remains, as they are no longer accepting bribes to do so (note: this is not legal advice- speak to a lawyer!)

### issues

Here are some of the main issues with this approach, followed by further discussion and proposed solutions:

- [frontrunning within network latency](#frontrunning-within-network-latency)
- [backrunning latency battles](#backrunning-latency-battles)
- [validators earning less](#validators-earning-less)
- [DDOS attacks](#DDOS-attacks)

### solutions

#### frontrunning within network latency

An attacker may be able to frontrun a transaction seen in the p2p network by getting their transaction to the [proposer first](https://medium.com/initc3org/strategic-latency-reduction-in-blockchain-peer-to-peer-networks-6599bf38fd53) via a more [direct route](https://bloxroute.com/).

The only robust solution to this is to [encrypt transactions](https://ethresear.ch/t/shutterized-beacon-chain/12249) until after ordering is established, but this is beyond scope.

This situation is anyway improved by time ordering, because this kind of frontrunning is limited to network latency (~500ms). Under the status quo transactions can be frontrun by seconds, minutes or hours.

The more we reduce the latency between users and proposers, the more we also reduce these remaining frontrunning opportunities, to zero in the best case:

![Unilateral Fair Ordering Overview](https://i.imgur.com/oXxniu4.png)

In this scheme, wallet nodes that receive user transactions directly also permit validators to connect directly to them. If these connections could be optimized to be as fast as the dedicated [distribution networks](https://bloxroute.com/) used by extractors themselves, frontrunning would no longer be possible.

Validators can connect to wallets in one (or both) of two ways:
- peered as [static nodes](https://geth.ethereum.org/docs/interface/peer-to-peer) in their execution clients
- via JSON-RPC websocket subscriptions

This preserves decentralization in that the public mempool is still used (unlike with builder based private order flow solutions).

Because of the wide adoption of [Infura](https://infura.io/) by both wallets and validators, it is possible that conditions already exist to avoid frontrunning.

For example, if a validator has a direct socket connection to Infura, even users of [Bloxroute](https://bloxroute.com/) may struggle to frontrun Metamask users in those blocks.

#### backrunning latency battles

With time ordering, backrunners can no longer bribe validators to put their transaction at the top of the block. To be successful, they must simply be the quickest to respond.

##### validators backrunning

It may seem that this will inevitably lead to spam from latency battles between backrunners. But validators have a big advantage over any other actor: *they can add transactions to their own block with zero latency*.

When a backrunnable transaction is received, the validator can immediately backrun it without breaking their own fair-ordering rules.

Even where transactions arrive in batches, if the proposer was peering directly with the wallet node, other backrunners are unlikely to be able to compete.

In this way, [neutral MEV](https://info.zeromev.org/terms.html#neutral-mev) can be extracted by the validator and spam can be avoided without the need for MEV auctions (which maximize [toxic MEV](https://info.zeromev.org/terms.html#toxic-mev)).

##### validators not backrunning

Even if validators choose not to backrun, this will not necessarily lead to spam.

The situation is better than with gas price auctions, because there is no bidding war. An extractor will only send one transaction per opportunity rather than multiple bids under an auction.

Also, it is not commonly known that Geth already orders transactions by time where they share the same gas price. Not only that, but this was actually done to *mitigate* spam. As [this discussion](https://github.com/ethereum/go-ethereum/issues/21350) makes clear, there were concerns about spamming due to this modification. As far as we are aware, this has not occurred.

You can see this clearly [here](https://zeromev.org/block?num=14012201). The vast majority of this block is receive time ordered to a high degree of accuracy due to most of the transactions within it sharing the same gas price.

![Zeromev Block 140122101 - Mostly Receive Time Ordered](https://i.imgur.com/3XRuhT0.png)

When validators do not backrun themselves, whoever has the lowest latency network will benefit instead. As such, it is likely that backruns will be done by a small number of highly resourced actors.

While profits would be centralized in that case, spam would be less of an issue. To avoid centralization, validators may be encouraged to backrun and given the tools to do so.

This is made easier by the fact that backrunning a single known state requires far less sophistication and hardware cost than frontrunning the very large set of all possible ordering states.

##### blockspace reclaimed from frontrunning

It should also be noted that where there is less frontrunning, there will also be fewer frontrunning transactions, and so the blockspace taken up by these will be reclaimed.

#### validators earning less

Unfortunately, validators ordering by receive time alone will earn less because they are only paid in tips after EIP-1559. They have a a few options here:

##### altruism

Altruistic validators may choose to include low or zero tip transactions anyway. 

##### base fee percentage

To improve earnings without rewarding frontrunning, validators may require transactions to have a tip greater than some percentage of the base fee to be included.

Users can rest assured that their transactions will be included in time order as long as they tip at least this amount (similar to a fee payment to a centralized exchange).

##### select by gas

Validators can choose to build a block by gas price as usual, but then order the transactions within it by receive time.

In this case, they earn the same as any standard Geth validator, while not permitting frontrunning within their block.

You can see how blocks like this might look by clicking on 'Fair Order' for any block on zeromev.org.

#### DDOS attacks

There is no DDOS attack vector because of the EIP-1559 base fee.

## references

[^1]: https://ethresear.ch/t/shutterized-beacon-chain/12249

[^2]: https://eprint.iacr.org/2021/1465

[^3]: https://medium.com/initc3org/strategic-latency-reduction-in-blockchain-peer-to-peer-networks-6599bf38fd53

[^4]: https://info.zeromev.org/problem.html
