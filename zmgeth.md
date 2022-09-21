# solution for validators

The Ethereum protocol currently allows validators to frontrun users for profit and to censor transactions arbitrarily.

This is worsened by MEV auction schemes such as [MEV-Boost](https://ethresear.ch/t/mev-boost-merge-ready-flashbots-architecture) which aggregate this power to [centralized builders](https://ethresear.ch/t/two-slot-proposer-builder-separation/10980/10).

[Zeromev-Geth](https://github.com/zeromev/zeromev-geth) is a fully decentralized solution for Ethereum validators wishing to: 
- protect users from [frontrunning](https://info.zeromev.org/terms#frontrunning) and [censorship](https://info.zeromev.org/terms#censorship)
- protect the network from [builder centralization](https://ethresear.ch/t/two-slot-proposer-builder-separation/10980/10) and network censorship under [MEV-Boost](https://ethresear.ch/t/mev-boost-merge-ready-flashbots-architecture)
- protect Ethereum from reduced adoption due to [toxic MEV](https://info.zeromev.org/terms.html#toxic-mev)
- protect themselves from the moral and [legal jeopardy](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4187752) of frontrunning Ethereum users (not legal advice- please consult a lawyer!)
- preserve the opportunity to extract neutral MEV themselves by backrunning
- generally [do the right thing](https://youtu.be/739XYgoA-x8?t=31) :)

Please see the Zeromev-Geth [readme](https://github.com/zeromev/zeromev-geth/blob/master/README.md) for more details and read our [proposal document](https://info.zeromev.org/zmgeth-proposal.html).

If you are a validator wishing to run Zeromev-Geth, you can find the [source code](https://github.com/zeromev/zeromev-geth) here.
