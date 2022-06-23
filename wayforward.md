# a way forward

The following thoughts on reducing [toxic MEV](/terms#toxic-mev) are written in good faith based on many years worth of study in this area and with the best interests of Ethereum users in mind.

Zeromev always encourages people to do their own research, and will under not under any circumstances take responsibility for losses.

## users

Our recommendations for users are designed to:

*   protect you from being exploited for [toxic MEV](/terms#toxic-mev) to the maximum extent possible.
*   cost you less in transaction fees.
*   reduce the centralizing effects of MEV on the Ethereum mainnet.
*   reduce congestion on Ethereum mainnet.
*   reduce the overall gas costs on Ethereum mainnet and Layer 2.

### summary of recommendations

*   [only use ethereum mainnet for token deposits and transfers.](#only-use-ethereum-mainnet-for-token-deposits-and-transfers)
*   [use a first come first serve (FCFS) layer 2 for everything else.](#use-a-first-come-first-serve-FCFS-layer-2-for-everything-else)

### only use ethereum mainnet for token deposits and transfers

Ethereum mainnet is becoming an increasingly hostile place to do business. 

The [Ethereum Foundation](https://ethereum.org) under the advice of [Flashbots](https://docs.flashbots.net) are currently on a path of [maximizing MEV extraction](https://ethresear.ch/t/mev-boost-merge-ready-flashbots-architecture/11177) the majority of which has been shown to involve [frontrunning](/terms#frontrunning) and [censorship](/terms#censorship).

While your tokens and direct token transfers are safely secured by the distributed nature of Ethereum consensus, popular use cases such as token swaps and NFT trades are extremely vulnerable to [toxic MEV](/terms#toxic-mev).

Please consider avoiding such activities on Ethereum mainnet altogether wherever possible. 

#### mainnet MEV protection vulnerabilities

If you do decide to use order-sensitive smart contracts on Ethereum mainnet, understand that there are currently no dependable solutions to protect you from [toxic MEV](/terms#toxic-mev) in that environment. See [here](https://twitter.com/pmcgoohanCrypto/status/1516410063665127425?s=20&t=4VdFCo4IjKztveeJuZAeyg) for further explanation and examples.

In short, mainnet protections must rely on trusting miners who are the very actors that benefit from [toxic MEV](/terms#toxic-mev). Miners are incentivized to make such protections fail at the point they start saving users money. Some miners have taken that decision already.

If you do decide to use mainnet MEV protections, please set transaction parameters assuming you are still vulnerable (eg: tight slippage on a DEX swap).

### use a first come first serve (FCFS) layer 2 for everything else

A quick look at the zeromev frontrunning explorer clearly shows how miners profit from users by reordering their transactions (frontrunning and censorship). 

By using a [Layer 2 network](https://ethereum.org/en/layer-2) (L2) that enforces the time order of transactions, most harmful [toxic MEV](/terms#toxic-mev) can be avoided.

Choose a First Come First Serve (FCFS) L2 with a high [Total Value Locked](https://l2beat.com) (TVL) that ensures they have a lot at risk reputationally, legally and financially if they choose to exploit you.

Ethereum miners are similarly trusted for transaction ordering, but are unaccountable and anonymous. Worse, the majority now run software designed to maximize the exploitation of MEV and are not worthy of your trust.

Avoid L2s that offer bribery ordering or have dubious or exploitative MEV policies. For example, [Arbitrum](https://portal.arbitrum.one/) offers FCFS ordering, and has made it clear that frontrunning will [not be tolerated](https://docs.ata.network/mev/solutions/mev-minimization-prevention/#arbitrum-by-offchain-labs), whereas [Optimism](https://www.optimism.io/) has looked to extract MEV from users [by design](https://ethresear.ch/t/mev-auction-auctioning-transaction-ordering-rights-as-a-solution-to-miner-extractable-value/6788).

### looking to the future

The recommendations above empower you to take effective action **today** to protect yourself from [toxic MEV](/terms#toxic-mev).

The following organizations are at the fore of research to mitigate [toxic MEV](/terms#toxic-mev) in a fully distributed setting:

*   [Chainlink: Fair Sequencing Services](https://blog.chain.link/chainlink-fair-sequencing-services-enabling-a-provably-fair-defi-ecosystem/)

*   [Shutter Network](https://shutter.ghost.io/)

*   [Arbitrum (Offchain Labs) MEV Wiki](https://www.mev.wiki/solutions/mev-minimization/arbitrum-offchain-labs)
