# data and technical

The zeromev system consists of four main components authored in C# .NET Core.

## zeromev overview

| component          | description                                                                      |
|--------------------|----------------------------------------------------------------------------------|
| [extractor service](#extractor-service)  | records the arrival time of pending transactions                                 |
| [classifier service](#classifier-service) | detects, classifies and quantifies instances of MEV                              |
| [api server](#api-server)         | provides compact MEV data to the web client                                      |
| [web client](#web-client)         | single page application drawing data from the api server and third parties       |

# change log

[See here](/change) to review changes to our data and methodology over time.

# extractor service

The extractor service is designed to run locally on full Ethereum nodes which it connects to via both RPC and Websockets.

As soon as a pending transaction is seen for the first time through the websocket subscription, it is timestamped and recorded in a centralized database along with the location id of the server.

The extractor service also captures data from the Flashbots [blocks api](https://blocks.flashbots.net/) which is stored in compressed form in the same database.

Our systems currently run the extractor service alongside the official Ethereum protocol implementation [geth](https://geth.ethereum.org/) in three geographically distributed locations (Europe, Asia and the US). An additional server connects to Infura and is hosted close to their servers.

Arrival timestamps have been captured since block 13358564 (Oct-05-2021). Transactions are tracked for a maximum of 14 days from first seen to block inclusion time.

# classifier service

The classifier service is designed to extract MEV data and write it in compressed form ready for the web client as well as in summary form for analysis.

The classifier keeps track of tick level price data for each Ethereum token parsed from Uniswap v2/v3 swap details exported by mev-inspect-py.

Arbitrages and liquidations are sourced directly from Flashbots [mev-inspect-py](https://github.com/flashbots/mev-inspect-py) running against [erigon](https://github.com/ledgerwatch/erigon) full archive nodes, but with dollar exchange rates for these instances recalculated using the exchange rate data above at block granularity. As such they may differ in results from those found in the mev-inspect-py mev summary table and mev-explore.

Sandwiches are recreated internally using methods modified from the mev-inspect-py code and with sandwich profits recalculated according to zeromev's research [Estimating Sandwich Attack Profits And User Losses](https://docs.google.com/document/d/1CiVE-ASAjoKdc1V8ed6ABPJUAPsa7ADEB5VmnY1TkvI/edit?usp=sharing) as mev-inspect-py has outstanding issues in this area. Sandwich dollar exchange rates are calculated at tick granularity using the method above.

Because of zeromev's reliance on mev-inspect-py for detection, much of the information from the mev-explore [data & metrics](https://explore.flashbots.net/data-metrics) page applies here.

The classifier also sources token details from [ethplorer](https://ethplorer.io/).

The output of the classifier is compressed json written to a database.

# api server

The api service takes data from both the extractor and classifier databases for a given block and serves it in json format to the web client.

# web client

The web client is a single page application written in Blazor WASM. It sources data from the zeromev api server, [infura](https://infura.io/), [etherscan](https://etherscan.io/) and [ethplorer](https://ethplorer.io/).

# acknowledgments

Our credit and thanks go to the following organizations technologies that support the zeromev site and it's systems

* [Nethereum - an open source .NET integration library for blockchain](https://nethereum.com/)
* [Flashbots - mev-inspect-py (MEV inspector)](https://github.com/flashbots/mev-inspect-py)
* [Erigon - very efficient full node Ethereum client](https://github.com/ledgerwatch/erigon)
* [Go Ethereum - official Go implementation of the Ethereum protocol](https://geth.ethereum.org/docs/getting-started)
* [Infura - high availability Ethereum API](https://infura.io/)
* [Etherscan - the ethereum blockchain explorer](https://etherscan.io/)
* [Ethplorer - ethereum tokens explorer](https://ethplorer.io/)
