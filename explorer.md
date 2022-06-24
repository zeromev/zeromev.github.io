# zeromev frontrunning explorer

Ethereum miners and validators have unchecked power to take money from you by [frontrunning](/terms#frontrunning) and [censoring](/terms#censorship) your transactions.

The zeromev frontrunning explorer gives clear and detailed visibility of [Miner Extractable Value](/terms#miner-extractable-value) (MEV) and [transaction reordering](/terms#transaction-reordering) ([frontrunning](/terms#frontrunning) and [censorship](/terms#censorship)) on the Ethereum network.

All dates and times on the site are in UTC (Coordinated Universal Time).

## walkthrough

Watch this walkthrough of all the main features of the zeromev frontrunning explorer:

<iframe
    width="640"
    height="480"
    src="https://www.youtube.com/embed/zkrrZZj_Oic"
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
*    hover over arrival time to see the first time each zeromev node saw this transaction when it was pending

### heatmap (+2 mins)

*    look at the multi-coloured heatmap on the left under the 'block order' button
*    it is a summary of the colours down the side of each transaction in the transaction table
*    the colours are all mixed up because the time order of transactions in the block is mixed up too
*    this is bad news because toxic MEV happens when miners order transactions by self-interest and not by time
*    click on 'fair order'
*    the heatmap now shows that transactions have been sorted in time order with the oldest first (light/yellow), and the most recent last (dark/black)
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
*    that the fair order of transactions in a p2p network like the one used by Ethereum is usefully knowable

Now try putting your wallet address into the search box at the top, and seeing if you have been the victim of toxic MEV.

## contents
* TOC
{:toc}

## search bar

At the top of each page is a search box.

As with most blockchain explorers, you can search for a block by Ethereum:
*   block number
*   transaction hash
*   address

Having searched by transaction hash or via the address page, a 'Jump To Tx' button allows you to quickly find the transaction of interest in the block.

## home page

This shows recent user losses due to MEV in realtime. Figures are shown for ['toxic' MEV](/terms#toxic-mev), which is harmful to users, and ['other' MEV](/terms#unclassified-mev) which is [unclassified MEV](/terms#unclassified-mev) that has not yet been differentiated into [toxic](/terms#toxic-mev) or [neutral](/terms#neutral-mev) MEV.

Click on 'Refresh' to get the most recent data available. It is normal for there to be a lag of a few minutes while blocks are processed and classified by the system.

Click on any block number to drill down into the details.

## block page

The block page is the heart of the zeromev frontrunning explorer.

The view it gives of [transaction reordering](/terms#transaction-reordering) and [Miner Extractable Value](/terms#miner-extractable-value) is unparalleled by other blockchain explorers.

See [walkthrough](#walkthrough) for more.

### heatmap

The time order heatmap is a key innovation of the zeromev frontrunning explorer. It lays bare the [transaction reordering](/terms#transaction-reordering) that underlies [toxic MEV](/terms#toxic-mev).

Light (yellow) indicates transactions that would have been included first in a block had it been ordered by time (fair ordered), while dark (black) transactions would have been included last in a block.

Try clicking between the 'block order', 'gas order' and 'fair order' buttons to see the impact that different ordering schemes have on a block. The 'fair order' button usually seperates attacking transactions from their victim transactions, which would have rendered them ineffective.

See [heatmap walkthrough](#heatmap-2-mins) for more.

#### heatmap calculation

The arrival time column shows the time at which a pending transaction was first seen by any one of the globally distributed zeromev nodes.

The delay is the difference between the time a transaction was first seen, and when it was included in the Ethereum blockchain.

From this we get the time column, which is the index of where the transaction would have come in the block order had it been ordered by time.

A colour is given to each transaction based on the time column, with low numbers being light (yellow) and high numbers dark (black).

See [heatmap walkthrough](#heatmap-2-mins) for more.

### block box

Shows the block number along with a summary of MEV in the block, a transaction count, and the Eth price in USD at the time the block printed.

### delay box

Shows the average and maximum amount the transactions were delayed before being included in this block.

Hover over to see block arrival times for each zeromev node.

See [network performance](#network-performance-1-min) in the [walkthrough](#walkthrough) for more.

### network box

Shows the performance of the Ethereum peer-to-peer network and includes a count of the number of nodes used to collect the sample.

Hover over to see individual measurements for each zeromev node, as well as average and standard deviation calculations.

See [network performance](#network-performance-1-min) in the [walkthrough](#walkthrough) for more.

### ordering buttons

The ordering buttons allow you to try out different what-if orderings of transactions in a block, along with the original block order chosen by the miners.

#### block order

The original order of the block as determined by the miner.

#### gas order

The order of the block if sorted by gas price.

#### fair order

The order of transactions in the block if sorted by the first-seen arrival time of the globally distributed zeromev nodes.

It is an approximation of objectively fair send time order (see [transaction reordering](/terms#transaction-reordering)) and [heatmap walkthrough](#heatmap-2-mins) for more.

### filter buttons

Allow the user to filter which transactions are shown in the transaction table by different criteria.

#### all

Shows all transactions in the block.

#### info

Shows only transactions which zeromev has classified in some way.

As well as MEV types such as sandwiches, arbs and liquidations, this includes distributed exchange swaps and NFTs purchases.

#### toxic

Shows only transactions which are the victim of [toxic MEV](/terms#toxic-mev) attacks and their attacking transactions.

#### other

Currently shows all [unclassified MEV](/terms#unclassified-mev) transactions.

### transaction table

The transaction table shows every transaction in the block on a single page, or optionally a [filtered selection](#filter-buttons) of them.

If you searched for a specific transaction or clicked on one from the [address page](#address-page), a 'Jump To Tx' button allows you to quickly find the transaction in question in the block.

Each column in the table is described below.

#### time

The index position of a transaction in the block when ordered by first seen arrival time.

See [heatmap calculation](#heatmap-calculation) for more.

#### delay

The delay between when a transaction was first seen by any of the zeromev nodes and when it was executed and published in the block.

Hover over to see the delay measured by each individual zeromev node.

'miner' means that the transaction was not seen in the mempool of any of the zeromev nodes, and was likely inserted by the miner when they created the block.

#### mev

This gives details of MEV and other information.

*   [Toxic MEV](/terms#toxic-mev) is in red (hover over for details).
*   [Unclassified MEV](/terms#unclassified-mev) is in grey (hover over for details).
*   Non MEV such as straightforward swaps and NFT trades are shown in light blue.

#### impact

Summarizes the loss to the user of a MEV instance, or in the case of liquidations, the negative of the transaction profit for consistency. Where both user loss and miner profit can be calculated, such as for [sandwich attacks](/terms#sandwich-attacks), user loss is shown.

#### action

Gives information about the execution of the transaction, not just those related to an instance of MEV. Examples include swaps, liquidations and NFT trades.

#### flashbots bundle

This column has a robot icon in the header.

When populated, it shows that the transaction was inserted by the miner having been bribed for inclusion in a [Flashbots Bundle](https://docs.flashbots.net/flashbots-auction/searchers/advanced/understanding-bundles).

The first number is the Flashbots bundle number and the second is the index of the transaction within the bundle.

Examples:
2.1 is the first transaction in bundle 2.
4.6 is the sixth transaction in bundle 4.

Please note that while Flashbots bundles start from 0 in their API, zeromev starts bundles from 1 as this is also the behaviour of the official [Flashbots Bundle Explorer](https://flashbots-explorer.marto.lol/).

#### transaction hash

An abbreviated hash of the Ethereum transaction. Hover over for the full hash. Click to link to it on Etherscan.

#### arrival time

The arrival time column shows the time at which a pending transaction was first seen by any one of the globally distributed zeromev nodes.

Hover over a delay value to see the arrival times measured by each individual zeromev node.

#### from

The abbreviated originating address of the Ethereum transaction. Hover over for the full address. Click to link to it on Etherscan.

#### to

The abbreviated destination address of the Ethereum transaction. Hover over for the full address. Click to link to it on Etherscan.

#### value

The value in Eth of the transaction.

#### gas price

The bribe to the miner to include the transaction in the chain. The miner may also have been bribed for inclusion and priority in a [Flashbots Bundle](#flashbots-bundle) or by any other route.

Denominated in Gwei.

## address page

You can navigate to the address page by searching for a valid Ethereum address in the [search bar](#search-bar)

You can then page through all the transactions performed by this address. This is useful for seeing if you have been the victim of [toxic MEV](/terms#toxic-mev)

Clicking on a transaction hash from here drills down into the block containing that transaction. A 'Jump To Tx' button will then allow you to quickly find the transaction in question in the block.
