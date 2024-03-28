# MINIMAL ENSHRINED OPERATOR DELEGATOR SEPARATION (meODS)
## Relevant context 
Principal–Agent problem, in which the interests of the Principal are not aligned with the interests of the Agent, is part of any delegation, and even more so present in today's staking design. Outside protocol level, staking has split naturally into two classes of participants:

||current natural separation|
|:---:|:----:|
|Delegators tier|ETH stakers, with no minimum commitment and no strict requirement to participate in any other way beyond bringing in their principal|Capital delegators (stakers)|
|Operators tier|proffesional node operators providing sophisticated services, with their reputation or some fixed amount of capital of their own at risk


## What is meODS?

meODS is ePBS's Consensus Layer sibling as both propose a better separation of roles in general to be implemented at protocol level, as a reaction of the protocol to some economical separation already naturaly established off-protocol. 
It implies enshrining further down into the protocol a separation of stakers roles in 2 tiers, based on the Principal-Agent relationship.

The "minimal" means that probably healthier to just enshrine right away a minimum set of measures that could be implemented at protocol level in a short period of time (preferably in parallel with other congruent upgrades being developed and evaluated for inclusion in Pectra hard fork), and leave some parts to be handled off protocol.
It is the quasi-equivalent of Level 1/3 as per the [Rainbow Staking POC](https://ethresear.ch/t/unbundling-staking-towards-rainbow-staking/18683/8) - Enshrined Operator-Delegator separation:

```
[...]enshrining some separation between operator and delegator[...] might be ok with some level of complexity. We could call a basic operator/delegator separation Level 1 [...]
```
```
The protocol would give powers to these two keys, but the mechanism for choosing the second key in each slot could be left to staking pool protocols.
```
[[1]](#resources)


## Roadmap tracker

|Upgrade|URGE|Track|Item|Cross-references|
|:---:|:---:|:---:|:---:|:---:|
|eODS|the Scourge|Staking economics|Solutions to liquid staking centralization|ILs, ePBS, SSF, Light Clients|

## Enshrinement of liquid staking research

### Social layer leverage

### The role of delegators
Calculus V

### Protocol functionality

There are pertinent [ideas](https://vitalik.eth.limo/general/2023/09/30/enshrinement.html#enshrining-liquid-staking) and [arguments](https://www.reddit.com/r/ethereum/comments/191kke6/comment/kh7piys/?utm_source=share&utm_medium=mweb3x&utm_name=mweb3xcss&utm_term=1&utm_content=share_button) around capping penalties (slashing and leaking) to a certain ratio of the minimum_balance

However, this only relates to the first of the two classes of solutions to increase the [meaningfulness of stakers](https://notes.ethereum.org/@vbuterin/staking_2023_10#If-delegators-can-have-a-meaningful-role-what-might-that-role-be):

 - Delegate selection
    - More competition between pools
        - improve liquidity and trustlessness of small staking pools

 - Consensus participation

Ethereum is constantly improving and growing on its way to becoming the envisioned global-scale network. In this scenario, single-slot finality and an increased validator count is not only desirable but most likely mandatory.

Looking at Ethereum roadmap from a collaborative and participatory approach to research and development,  we can structure a interdependence weight table to have a clearer view of the technical directions and social dilemas that might worth community's engagement to reach the envisaged goals:
![image](/docs/images/research/weight_table.png)

### Enabling stronger forms of consensus participation.

This research / proposal is about enabling stronger forms of consensus participation for delegators.

**Why separate?**
- Enabling stronger forms of consensus participation.
- Reduce the number of signatures
    - EIP-7251 [[4]](#resources) will allow a single message to carry more stake; enshrining the operator delegator separation would provide a way for the protocol to functionally distinguish “operator stake” from “delegator stake” on such a message, unlocking level 2 of the rainbow tier system -> further separation of each tier in heavy services providers and light services providers.

## Feasibility 
* Necessity 
    - There are risks in relying too much on the social layer and morality to protect the protocol against centralization in the staking scene and countering the emergence of a dominant LST with its associated perils
    -  We need an interface to integrate further “protocol services” in a plug-and-play manner
    - Limitations of current staking-design to ensure future competitive participation of solo stakers in different categories of protocol services (i.e. economic value and/or agency)
    - Ethereum needs good trade-offs to SSF
* Opportunity 
    - enshrining a variant of the already established staking model with two classes of participants: delegators (stakers) and node operators
    - enshrining some measure of operator–delegator separation concomitant with other EIPs that are debated and developed right now, could leverage a lot of the work currently done towards specifying these EIPs:
        - EIP-6110 [[5]](#resources) allows for an in-protocol mechanism of deposit processing on the Consensus Layer. Also it will add in-protocol mechanism by which large node operators can combine validators without cycling through the exit and activation queues.
        - EIP-7251 [[4]](#resources) will allow a single message to carry more stake; enshrining the operator delegator separation would provide a way for the protocol to functionally distinguish “operator stake” from “delegator stake” on such a message.

## Level1 (meODS) Feature set

| **FEATURE** | **title** | **description** | expected results|
| :----------: | :-----------: | :-----------: |:----:|
|Feature 1|enshrine Quick Staking Key (`Q key`)|Allow validators to provide two staking keys: the persistent key (P key) and the quick staking key (Q key) - address of a  contract that, when called, outputs a secondary staking key during each slot|Protocol can functionally distinguish `operator stake message` from `delegator stake message`|
|Feature 2|minimally enshrine LSM|adds Principal - Agent relations at protocol level|Operator stake and Delegator stake can exchange `Claim` and `Liability` messages|

[[2]](#resources)

## Feature 1 specification
A good starting point could be ammending the structure denoting new deposit operation under EIP-6110. This EIP is now [included in the next hard-fork](https://github.com/ethereum/EIPs/commit/810c347a48052ab36a53a6aa684737ce386f6093), so the proposed specification takes the following into account:
 - validator deposit is appended to EL's block structure
 - deposit inclusion and validation responsability is passed to the EL  - no need for deposit data voting from the Consensus Layer

```
class DepositReceipt(Container):
    pubkey: BLSPubkey
    qkey_generator: ExecutionAddress #added line
    withdrawal_credentials: Bytes32
    amount: Gwei
    signature: BLSSignature
    index: uint64
```

OPERATOR - `operator stake message`

`DepositReceipt` needs to be signed with the depositor's private key (for rogue key attacks reasons) and the pubkey is added to the deposit data, so the protocol "sees" who the Depositor is. 
Considering permissionless staking pools will most likely always use pool-specific withdrawal addresses, the pool Operator can be considered the Depositor, and because (even in single-slot finality scenario) validator deposits are a core component of PoS consensus, the protocol will be able to distinguish Operator stake message this way.

DELEGATOR - `delegator stake message`

The protocol could map Principal - Agent relation by the logic contained in the smart contract provided by the Operator during deposit process eg. "Y delegated stake to X and X deposited that stake in protocol". So Y is the capital provider (Delegator), while X is the Operator.

## Feature 2
In a semi-enshrining of LSM scenario, having Feature 1 implemented would allow the protocol to map relation or claim and liability messages between Operators and Delegator.

Light Validator clients can then provide light services to the Execution payload and delegator stake message could then used for *light certificate* issuance, restaking, etc. as per Level2 criteria.

## Level 2
The separation between heavy services providers and light services providers could be done in-protocol, after increasing the MAX_EFFECTIVE_BALANCE([EIP-7251](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-7251.md)), and later implementing a balance threshold (eg. 2048 ETH) to determine which existing validators enter which complexity tier.


While a full enshrinement of the 2by2 tiered staking (rainbow staking) and Strong coupling mandating the *light certificate* for block validity is the course to be taken imo, there can be value in [enshrining some things outright and leaving some things to the users](https://vitalik.eth.limo/general/2023/09/30/enshrinement.html#enshrining-liquid-staking) (i.e. staking pools) approach + a weak coupling approach under the staus qvo(staking pools get to op-in), otherwise, we risk not having any in-protocol Operator-Delegator separation for the ~ next two years.

```
The protocol would give powers to these two keys, but the mechanism for choosing the second key in each slot could be left to staking pool protocols - V.B.
```

## Resources
[[1] Unbundling staking](https://ethresear.ch/t/unbundling-staking-towards-rainbow-staking/18683)

[[2] Protocol and staking pool changes that could improve decentralization and reduce consensus overhead](https://notes.ethereum.org/@vbuterin/staking_2023_10)

[[3] Should Ethereum be okay with enshrining more things in the protocol?](https://vitalik.eth.limo/general/2023/09/30/enshrinement.html#what-do-we-learn-from-all-this)

[[4] EIP-7251](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-7251.md)

[[5] EIP-6110](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-6110.md)

[[7] Slashing penalty analysis](https://ethresear.ch/t/slashing-penalty-analysis-eip-7251/16509)
