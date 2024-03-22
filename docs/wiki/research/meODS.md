# MINIMAL ENSHRINED OPERATOR DELEGATOR SEPARATION (meODS)
## Relevant context 
Principal–Agent problem, in which the interests of the Principal are not aligned with the interests of the the Agent, is part of any delegation, and even more so present in today's staking design. Outside protocol level, staking has split naturally into two classes of participants:

||current natural separation|
|:---:|:----:|
|Delegators tier|ETH stakers, with no minimum commitment and no strict requirement to participate in any other way beyond bringing in their principal|Capital delegators (stakers)|
|Operators tier|profesional node operators providing sophisticated services, with their reputation or some fixed amount of capital of their own at risk


## What is meODS?

meODS is ePBS's Consensus Layer sibling as both propose a better separation of roles in general to be implemented at protocol level, as a reaction of the protocol to some economical separation already naturaly established off-protocol. 
It implies enshrinig further down into the protocol a separation of stakers roles in 2 tiers, based on the Principal-Agent relationship.

The "minimal" means that probably healthier to just enshrine right away a minimum set of measures that could be implemented at protocol level in a short period of time (preferably in parallel with other congruent upgrades being developed and evaluated for inclusion in Pectra hard fork), and leave some parts to be handled off protocol.
It is the quasi-equivalent of Level 1/3 as per the [Rainbow Staking POC](https://ethresear.ch/t/unbundling-staking-towards-rainbow-staking/18683/8) - Enshrined Operator-Delegator separation:

```
[...]enshrining some separation between operator and delegator[...] might be ok with some level of complexity. We could call a basic operator/delegator separation Level 1 [...]
```
[[1]](#resources)


## Roadmap tracker

|Upgrade|URGE|Track|Item|Cross-references|
|:---:|:---:|:---:|:---:|:---:|
|eODS|the Scourge|Staking economics|Solutions to liquid staking centralization|ILs, ePBS, SSF, Light Clients|

## meODS Research

### What is the perception of what enshrinement of liquid staking 
There are pertinent [ideas](https://vitalik.eth.limo/general/2023/09/30/enshrinement.html#enshrining-liquid-staking) and [arguments](https://www.reddit.com/r/ethereum/comments/191kke6/comment/kh7piys/?utm_source=share&utm_medium=mweb3x&utm_name=mweb3xcss&utm_term=1&utm_content=share_button) arround capping penalties (slashing and leaking) to a certain ratio of the minimum_balance

but this only answers/relates to one(delegate selection) of the two classes of solutions to increase the meaningfulness of stakers in Vitalik Buterin's paper on [envisioned staking improvements.](https://notes.ethereum.org/@vbuterin/staking_2023_10#If-delegators-can-have-a-meaningful-role-what-might-that-role-be)

 - Delegate selection
    - More competition between pools
        - improve liquidity and trustlesness of small staking pools

 - Consensus participation

By taking a [thought experiment](https://notes.ethereum.org/@vbuterin/staking_2023_10#The-role-of-delegators), Vitalik *conchides* (e corect? sau  sinonim cu ajunge la concluzia ca) that:
```
The purpose of this argument[...] is to point out a key property that a well-functioning staking system should have: namely, delegators should be doing something that actually matters.
``````
Vitalik underlines the native staking-stage being split between 2 roles: 
- delegators (stakers) and  
- node operators. 

Capping penalties [EIPs??] would definitely be an improvment to the status qvo and would only put at stake the NOs stake share, amking the delegator's (stakers's share unslashabe/ risk free). That would allow staking pools to go full trustless and uncensorable stablecoins like a fork of RAI to onboard risk-free staked eth and cover some of [the opportunity cost RAI minters pay](). 

The conclusion is that we could think of better ways *still*

## Enabling stronger forms of consensus participation.

This research / proposal is about the second, more meaningfull for delegators way of seing what meODS should be and that is enabling stronger forms of consensus participation for delegators

 
* the 2 classes of answers are complementary so judging by that rationale, capping penalties should not be incompatible with increasing delegators participation in consensus. more studies? 

**why separate?**
- Enabling stronger forms of consensus participation.
 - Reduce the number of signatures
    - EIP-7251 [[4]](#resources) will allow a single message to carry more stake; enshrining the operator delegator separation would provide a way for the protocol to functionally distinguish “operator stake” from “delegator stake” on such a message, unlicking level 2 of the rainbow tier system -> further separation of each tier in heavy services provider and light services provider.

## Feasibility 
* Necessity 
    - There are risks in relying too much on the social layer and morality to protect the protocol against centralization in the staking scene and countering the emergence of a dominant LST with its afferent perils
    -  We need an interface to integrate further “protocol services” in a plug-and-play manner
    - Limitations of current staking-design to ensure future competitive participation of solo stakers in different categories of protocol services (i.e. economic value and/or agency)
    - Ethereum needs good trade-offs to SSF
* Opportunity 
    - enshrining a variant of the already established staking model with two classes of participants: delegators (stakers) and node operators
    - enshrining some measure of operator–delegator separation concomitant with other EIPs that are debated and developed right now, could leverage a lot of the work currently done towards specifying these EIPs:
        - EIP-6110 [[5]](#resources) allows for an in-protocol mechanism of deposit processing on the Consensus Layer. Also it will add in-protocol mechanism by which large node operators can combine validators without cycling through the exit and activation queues.
        - EIP-7251 [[4]](#resources) will allow a single message to carry more stake; enshrining the operator delegator separation would provide a way for the protocol to functionally distinguish “operator stake” from “delegator stake” on such a message.

## Feature set

| **FEATURE** | **title** | **description** | expected results|
| :----------: | :-----------: | :-----------: |:----:|
|Feature 1|enshrine Quick Staking Key (`Q key`)|Allow validators to provide two staking keys: the persistent key (P key) and the quick staking key (Q key) - a smart contract that, when called, outputs a secondary staking key during each slot|Protocol can functionally distinguish `operator stake message` from `delegator stake message`|
|Feature 2|enshrine LSM|adds Principal - Agent relations at protocol level|Operator stake and Delegator stake can exchange `Claim` and `Liability` messages.

```
The protocol would give powers to these two keys, but the mechanism for choosing the second key in each slot could be left to staking pool protocols.
```
[[2]](#resources)
## Implementation POC
MVE-LS POC can be done on top of EIP-6110 specification for future validator deposits and of EIP-7251 for backward compatibility (hard fork) 

## Resources
[[1] Unbundling staking](https://ethresear.ch/t/unbundling-staking-towards-rainbow-staking/18683)

[[2] Protocol and staking pool changes that could improve decentralization and reduce consensus overhead](https://notes.ethereum.org/@vbuterin/staking_2023_10)

[[3] Should Ethereum be okay with enshrining more things in the protocol?](https://vitalik.eth.limo/general/2023/09/30/enshrinement.html#what-do-we-learn-from-all-this)

[[4] EIP-7215](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-7251.md)

[[5] EIP-6110](https://github.com/ethereum/EIPs/blob/master/EIPS/eip\-6110.md)

