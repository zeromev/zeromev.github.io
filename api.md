![zeromev api logo](/images/api.jpeg)

# zeromev API usage guide

The zeromev REST API allows you to get transaction level MEV summary data for the Ethereum blockchain.

Please read the [data sources & limitations](https://info.zeromev.org/sources.html) page before using the API and take note of our [terms of service](https://info.zeromev.org/disclaimer.html).

## access

The endpoint and schema will be found here after the API launch. Access is public and unauthenticated.

## quick start

- [`mevBlock`](https://info.zeromev.org) returns one or more blocks of MEV transactions.
- [`mevTransactions`](https://info.zeromev.org) returns all MEV transactions for an Ethereum address.
- [`mevTransactionsSummary`](https://info.zeromev.org) returns MEV summary data for an Ethereum address.

## usage & best practices

### MEV types

Each MEV transaction has an `mev_type`.

| type | description |
| -------- | -------- |
| arb     | an arbitrage transaction allowing the extractor to profit from price discrepancies between exchanges.     |
| frontrun     | the frontrun transaction in a sandwich. This initiates the attack and moves the price against the victim.     |
| sandwich     | a victim transaction in a sandwich. There can be one or more of these per attack.     |
| backrun     | this is the backrun in a sandwich, allowing the attacker to close their position and extract a profit.     |
| liquid     | refers to a liquidation event in a DeFi lending protocol.     |
| swap     | swaps are included to provide volume data for non-MEV transactions.     |

### handling swap volume

Although not strictly MEV, swaps are included in the dataset to allow for MEV vs overall swap volume reports. 

Please follow these guidelines for best accuracy:
- `user_swap_volume_usd` refers to the estimated volume of swaps less those which were sent only to extract value.
- this is usually the correct value to aggregate in reports like the above.
- `extractor_swap_volume_usd` refers to swaps sent by MEV extractors in order to extract MEV and should only be used when this data is specifically required.
- swap volumes are limited to those tokens known to zeromev and for which valid exchange rates can be calculated.
- this makes it the most appropriate swap volume data for comparison with our MEV data.
- the amount of MEV is greatly underestimated at the moment due to both [known](https://info.zeromev.org/sources.html) and unknown limitations with MEV classification and the lack of cross-domain MEV classification and other MEV types.
- as such, please be aware that MEV to volume reports will be lower bound and may be somewhat misleading

### multiple protocol

- where there are multiple swaps in a single transaction for different protocols, these are given a generic protocol value of `multiple`.
- frontruns, backruns, and sandwiched types always have one well defined protocol and are not limited in this way.
- arbs are detected as single transactions involving multiple swaps and protocols and their protocol column will be set to `multiple`.

### imbalance

- most extractors will balance the backrun of a sandwich attack with the frontrun to extract the maximum possible risk free profit.
- we call these balanced sandwiches.
- some sandwiches may be (or appear to be) overweight on either the frontrun or the backrun.
- we call these unbalanced sandwiches.
- the cause of these is an open research area, but examples include:
    - the extractor using the sandwich to take a position at a discounted price.
    - the extractor engaging in cross-domain MEV, closing out what appears to be an open position on L1 against a CEX or other chain / L2.
    - limitations in the MEV detection involving overlapping attacks or attacks co-mingled with arbitrage as in [this example](https://zeromev.org/block?num=16749931).
- zeromev calculates sandwiches in a way that aims to compensate for these imbalances.
- an `imbalance` value is provided through the API to provide visibility of when sandwiches have been re-balanced in this way.
- a non-zero `imbalance` value indicates the sandwich was overweight on that side and needed to be re-balanced. 
- on a backrun transaction, `backrun imbalance = (calculated back out - original back out) / calculated back out`
- on a frontrun transaction, `frontrun imbalance = (calculated front in - original front in) / calculated front in`

### data coverage

MEV data has been extracted from block number 9216000 and is updated continuously.

### rate limiting

Calls are limited to a maximum of 5 per second.
