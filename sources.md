# data sources & limitations

- [mev-inspect-py](https://github.com/flashbots/mev-inspect-py) (by Flashbots) is used by [zeromev](https://zeromev.org) for MEV classification.
- as such much of the information from the MEV-Explore [data & metrics](https://explore.flashbots.net/data-metrics) page applies here.
- due to known [issues with sandwich profit estimation](https://github.com/flashbots/mev-inspect-py/issues/283) in mev-inspect-py, we recalculate sandwiches using our own AMM [pool extraction method](https://docs.google.com/document/d/1CiVE-ASAjoKdc1V8ed6ABPJUAPsa7ADEB5VmnY1TkvI/edit?usp=sharing).
- other MEV amounts are sourced directly from mev-inspect-py but with dollar exchange rates for these instances recalculated by zeromev using on-chain Uniswap v2/v3 swap data.
- because of this, our USD denominated results may differ from those found in [MEV-Explore](https://explore.flashbots.net/) which uses external data sources.
- known issues with mev-inpsect-py can be tracked on the Flashbots [github](https://github.com/flashbots/mev-inspect-py/issues).
- notably, there is a problem with detecting [split arbitrages](https://github.com/flashbots/mev-inspect-py/issues/220) which may contribute to the [disparity in arbitrage results](#data-source-comparison-test) below.
- there are also issues with overlapping MEV (eg: arbs co-mingled with sandwiches, and sandwiches that crossover with each other) which no MEV detection software fully handles at present.
- as such, this data must be considered a lower bound of MEV.

## data source comparison test

- [Eigenphi](https://eigenphi.io/) make a good data source comparison test as they employ a very different [MEV classification methodology](https://eigenphi-1.gitbook.io/classroom/eigenphis-methodologies/how-eigenphi-identifies-mev/recognizing-atomic-mev-transactions/abstract-approach) to mev-inspect-py and zeromev
- as can be seen below, the sandwich attacks recalculated by zeromev produce similar results to Eigenphi.
![sandwich data comparison (eigenphi vs zeromev)](https://i.imgur.com/mT7nV77.png)
- mev-inspect-py arbitrage classification is not yet recalculated by zeromev and misses around 64% of instances compared to Eigenphi at time of writing.
![arbitrage data comparison (eigenphi vs zeromev)](https://i.imgur.com/Yn0DDvI.png)

## data revision policy

- data will be subject to change as MEV classification improves.
- please bear this in mind when referencing our data and consult our [change log](https://info.zeromev.org/change) for details of any revisions.
