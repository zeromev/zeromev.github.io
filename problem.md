# the problem

Individual miners and validators have full control over which transactions go in their blocks and where in Ethereum.

This permits all kinds of [frontrunning](/terms#frontrunning) and [censorship](/terms#censorship) attacks that are harmful and costly to users and illegal in regulated markets.

These attacks may be performed directly by the miner, or the miner may be bribed to do so via the Ethereum gas price auction (GPA) mechanism or increasingly in a [MEV auction](https://medium.com/offchainlabs/mev-auctions-considered-harmful-fa72f61a40ea), although any means of bribery can be used.

In 2014 (pre-genesis), the pseudo-anonymous [founder of zeromev](https://twitter.com/pmcgoohanCrypto) alerted the community to this vulnerability in their post [Miners Frontrunning](https://www.reddit.com/r/ethereum/comments/2d84yv/miners_frontrunning).

In 2019, the seminal paper [Flashboys 2.0](https://arxiv.org/abs/1904.05234) coined the phrase [Miner Extractable Value](/terms#miner-extractable-value) (MEV) to describe how miners profit from this centralized, trusted power that they have over users in the Ethereum network, which still persists today.

Hundreds of millions of dollars have already been taken from Ethereum users in this way. Left unchecked, we expect the problem to [worsen intolerably](https://www.coindesk.com/tech/2021/05/10/why-ethereums-miner-extractable-value-problem-is-way-worse-than-you-think). 

Zeromev aims to eradicate [toxic MEV](/terms#toxic-mev) involving [frontrunning](/terms#frontrunning) and [censorship](/terms#censorship).
