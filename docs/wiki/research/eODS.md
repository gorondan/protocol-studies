# enshrined OPERATOR-DELEGATOR SEPARATION (eODS)
## Roadmap tracker

| Upgrade |    URGE     |       Track       |                    Item                    |       Cross-references        |
| :-----: | :---------: | :---------------: | :----------------------------------------: | :---------------------------: |
|  eODS   | the Scourge | Staking economics | Solutions to liquid staking centralization | ILs, ePBS, SSF, Light Clients |
## Relevant context 
Principal–Agent problem, in which the interests of the Agent are not aligned with the interests of the Principal, is part of any delegation, and even more so present in today's staking scene[^1].

Regarding the staking economy, specific market structures have naturally developed, after the Merge, inherited from the perennial distinction between labor and capital.
Thus, staking has split naturally in two classes of participants, outside protocol level[^2]:

|    Tier    |                                                        Current natural separation                                                        | Slashing risk |
| :--------: | :--------------------------------------------------------------------------------------------------------------------------------------: | :-----------: |
| Delegators |   ETH stakers, with no minimum commitment and no strict requirement to participate in any other way beyond bringing in their principal   |   Slashable   |
| Operators  | Proffesional node operators providing sophisticated services, with their reputation or some fixed amount of capital of their own at risk |   Slashable   |

The two tiers are closely interlinked, as liquid staking protocols are not credible if LST holders do not believe that the operators holding their principal are good agents. The risk of slashing, coupled with the high amount of revenue paid out in aggregate to Gasper service providers via issuance, results in intermediated chains of principal-agent relationships[^3] , with delegators providing capital (Principal) to operators who participate in Gasper on their behalf.


## What is eODS?

eODS is a (relatively new) design philosophy[^4] within Ethereum, proposing an even further separation of the role of **Validator** (unbundling), to be implemented at protocol level, closing the loop in the Staking economics track of the Scourge, between ePBS and Execution tickets.

| Upgrade | Separation type    |
| ------- | ------------------ |
| ePBS    | proposer-builder   |
| ET      | validator-proposer |
| eODS    | operator-delegator |

This separation addresses various inefficiencies associated with the limits of what the protocol sees[^5], and its capacity to react with automated defence systems, in the context of ETH staking.

## The layers of Operator-Delegator Separation
Operator-Delegator Separation taken in isolation, enshrines the separation, but brings no improvement to the existing entrenched structure:
| 1D-eODS   |           |
| --------- | --------- |
| OPERATOR  | DELEGATOR |
| slashable | slashable |

In order for eODS to be relevant, it must be considered holistically, together with other relevant, proposed, protocol changes:

* Capping pennalties:
    | 1D-eODS + capping penalties |             |
    | --------------------------- | ----------- |
    | OPERATOR                    | DELEGATOR   |
    | slashable                   | unslashable |

* Introduction of two distinct types of protocol services:
    * *Heavy Services*
    * *Light Services*
  
    This *design philosophy* produces a separation of the role of Validator in 2 dimensions (2D Operator-Delegator Separation):

    | 2D-eODS        |                 |               |
    | -------------- | --------------- | ------------- |
    | Light OPERATOR | Light DELEGATOR | non-slashable |
    | Heavy OPERATOR | Heavy DELEGATOR | slashable     |
  
## The role of Delegators

## Beyond the basics (why separate?)

### Social layer leverage
There are risks in relying too much on the social layer and morality to protect the protocol against centralization in the staking scene and countering the emergence of a dominant LST with its associated perils

### Already an established model
eODS would mean enshrining a variant of the already established staking model with two classes of participants: delegators (stakers) and node operators

### Enabling stronger forms of consensus participation.
This research / proposal is about enabling stronger forms of consensus participation for delegators.

Ethereum is constantly improving and growing on its way to becoming the envisioned global-scale network. In this scenario, single-slot finality and an increased validator count is not only desirable but most likely mandatory.

### Reduce the number of signatures (SSF scenario)
Ethereum needs good trade-offs to SSF

calculating large number of BLS - technical limitations

### Systematic censorship from identifiable validators
Inclusion lists prepared by honest validators function as censorship signals and defences. A censoring validator always has the option to not propose a block in case they do not wish to respect the inclusion list, or artificially stuff their block to satisfy the inclusion list fallback requirement. In both cases, the censoring validator profit is hurt, even when the cost of stuffing the block is higher than the revenue received by censoring validators from private order flow. Attesters uphold the validity and the satisfaction of an inclusion list, via the fork choice.

### Future protocol services
We need an interface to integrate further “protocol services” in a plug-and-play manner

EIP-7251 will allow a single message to carry more stake; enshrining the operator delegator separation would provide a way for the protocol to functionally distinguish “operator stake” from “delegator stake” on such a message, unlocking level 2 of the rainbow tier system -> further separation of each tier in heavy services providers and light services providers.

### Limitations of current staking-design 
There are limitations to the current staking-design to ensure future competitive participation of solo stakers in different categories of protocol services (i.e. economic value and/or agency)

## [Referenes]

[^1]: https://eprint.iacr.org/2023/605

[^2]: https://notes.ethereum.org/@vbuterin/staking_2023_10#Protocol-and-staking-pool-changes-that-could-improve-decentralization-and-reduce-consensus-overhead

[^3]: https://mirror.xyz/barnabe.eth/v7W2CsSVYW6I_9bbHFDqvqShQ6gTX3weAtwkaVAzAL4

[^4]: https://ethresear.ch/t/unbundling-staking-towards-rainbow-staking/18683#operatordelegator-separation-2

[^5]: https://barnabe.substack.com/i/95811604/case-studies-in-upgrading-the-fence


[[1] Unbundling staking]-(https://ethresear.ch/t/unbundling-staking-towards-rainbow-staking/18683)

[[2] Protocol and staking pool changes that could improve decentralization and reduce consensus overhead]- (https://notes.ethereum.org/@vbuterin/staking_2023_10)

[[3] Should Ethereum be okay with enshrining more things in the protocol?]-(https://vitalik.eth.limo/general/2023/09/30/enshrinement.html#what-do-we-learn-from-all-this)

[[4] EIP-7251]-(https://github.com/ethereum/EIPs/blob/master/EIPS/eip-7251.md)

[[5] EIP-6110]-(https://github.com/ethereum/EIPs/blob/master/EIPS/eip-6110.md)

[[7] Slashing penalty analysis]-(https://ethresear.ch/t/slashing-penalty-analysis-eip-7251/16509)

