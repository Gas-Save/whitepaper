# 🛢️ GasSave Whitepaper 🛢️

👷🛢️⚠️ **GasSave IS A WORK IN PROGRESS - ASPECTS ARE SUBJECT TO CHANGE!** ⚠️🛢️👷

# Introduction

GasSave is a gas saving protocol for Binance Smart Chain and Ethereum. It is designed to be protocol agnostic, easy to use, well tested and efficient. It is useful to blockchain users and developers alike, providing a useful hedge against future gas price increases from network traffic (Ethereum) and validator gas voting (Binance Smart Chain).

A Gas Token is a commodification of Gas fees. The aim of such a token is to frontload gas fees by paying for long term blockchain storage when gas is cheaper. The EVM provides a gas rebate mechanism for freeing up this storage, which reduces the gas cost of the entire transaction. The existing gas tokens, [GST1/GST2](https://gastoken.io/) and [CHI](https://blog.1inch.io/1inch-introduces-chi-gastoken-d0bd5bb0f92b), are limited in scope and application, and can only be used in scenarios where the rebate mechanism has been called from another smart contract. 

GasSave widens the scope of transactions where Gas Token rebates can occur. Doing so by providing a universal transaction wrapper, that can be used to provide rebates without requiring smart contract developers to reference the protocol directly.

The overall aims of the GasSave protocol is to; 
* Reduce long-term gas-price exposure for the individual
* Enable speculative gas investment
* Provide a source of fees to miners and validators during periods where blockchain activity is low (bear markets)
* Provide a vehicle for individuals to store and reuse gas.

This document outlines the core mechanics of GasSave. Full Technical details will be available on protocol release, which is currently on track for 30 April 2021. The full source code of the project will be available on protocol release.

**[WIP]Protocol Website:** 
https://www.GasSave.org

**[WIP] Documentation:** 
https://www.GasSave.org/docs

**Code:** 
https://www.github.com/Gas-Save


# Gas Save Protocol

GasSave introduces a number of tokens to the . Two Gas tokens, 3 wrappers for existing gas tokens and A protocol token used for staking, fee savings and voting. 

## Gas Tokens and Gas Savings
There are two Gas Save native gas tokens, Stored Gas v1 and v2. As well as wrappers that unify interfaces of the existing GST and Chi tokens.

### Stored Gas V1 
Stored Gas v1 (SG1), largely inspired by the gas storage method presented in GST1. This method relies upon writing values in storage, and then freeing up these values when a rebate is required. SG1 Improves upon the ideas presented in GST, as well as formalising the asset as an ERC20 compliant token. SG1 uses a less efficient storage method than the one presented in GT2/Chi, and by extension SG2. Please refer to gas benchmarks for further information.

### Stored Gas V2 
Stored Gas v2 (SG2), uses the method presented in GST2 and Chi. This method stores gas by creating empty child contracts, and then self destructs these children when a rebate is required. SG2 is essentially the GasSave version of CHI, with a number of adaptations and GasSave specific improvements. The method used by SG2 is the current best-known method in terms of efficiency. Please refer to gas benchmarks for further information.

### Gas Token Wrappers
GST and Chi tokens do not have a common interface or standard. GasSave introduces wrapper tokens that formalises the calls to these tokens. This allows the tokens to be used natively within the Gas Save protocol. These formal wrapped tokens introduce full ERC20 compatibility as well as the underlying minting fee mechanism.

### Transaction Wrapper
The transaction wrapper is the transaction agnostic part of the Gas Save protocol which facilitates gas saving by wrapping an existing transaction with the token burning and gas saving elements of the gas tokens. The transaction wrapper comes in two flavors. Proxy and Embeddeded, 

### UI

A UI will be available on MVP launch that will facilitate the ability to wrap transactions, mint new tokens, claim community rewards, stake and vote. Additionally, In order to help users store the optimal number gas tokens before  a given transaction, the UI will include an optimal token burn calculator.

## GasSave Token and Incentives

The GasSave token (GSVE) is the native token for the protocol. It bestows a few benefits to the holder. Some of these benefits are given when holders of the token can stake their tokens within a pool.

### Fee Pool

The fees collected by the protocol will be routed to a protocol pool. GSVE token holders will have the ability to burn the GSVE token in order to claim some of these pooled fees. The ratio of tokens burned to gas tokens given to the user is 0.1:1. Where burning 0.1 GSVE gives the user 1 gas token of their choice, from the gas fee pool. 

There is no way for fees to be taken from the protocol other than than this gas burning rebate.

### Voting

Stakers can vote on changing the fees. Where a vote is allocated for each token staked. Voting allows users to adjust the minting fee for new SG tokens, and wrapping fee of non-protocol gas tokens. The stakers can choose to reduce fees entirely down to the lowest non-zero value, or change them to a valid value up to a upper cap of 4. Where upper cap/10^token decimals. So for chi and SG tokens, this upper cap would be 10, and for GST it would be 0.1, and the lower cap would be 1 and 0.1 respectively.

### Fee Reduction

If a user has staked tokens, they reduce minting and burning fees for themselves. This saving is initially half the non-staked value. Stakers can choose to adjust this value via voting. The user has the option to burn tokens, which removes the fee entirely, so long as this GasSave burn occurs as part of a token minting or gas saving event.

# Gas Token Fee
Gas swap has no fee when it comes to using the protocol in gas saving transaction. The fee is paid by the user upfront in the form of a gas token fee. This fee is introduced in wrapping and minting operations for the SG gas tokens and wrapper GST/Chi tokens. 

The gas token fee is designed to be regressive as the fee is constant. This means that the fee as a percentage of tokens minted/wrapped goes down as the number of tokens created in the transaction goes up.

## Gas Token Fee Structure
| Token | Burning | Burning (Stakers)  | Minting | Minting (Stakers)|Wrapping | Wrapping (Stakers)|
|----------------------|---------|-------------|---------|------------------|---------|------------------|
|SG1 & SG2| No Fee Ever | No Fee Ever |2 Tokens| 1 Tokens|-|-|
|Wrapped GST1 & GST2| No Fee Ever | No Fee Ever |-| -|0.03 Tokens|0.02 Tokens|
|Wrapped Chi| No Fee Ever  | No Fee Ever |-|-|3 tokens|2 tokens|

Eventually minting and wrapping fees will be decided by GasSave token holders using the DAO voting mechanism. 

# Benefits & Opportunities

The existence of Gas Save creates a number of interesting opportunities. This section aims to highlight them.

## Gas Reduction
The most obvious benefit of the protocol is it's ability to offset the price of a high gas price transaction, by paying for gas when prices are lower. For instance, the average gas price on BSC is currently 15 gwei, whilst the minimum is 3gwei. It is entirely possible for individuals to passively mint SG gas tokens at 3gwei when the network is quiet. In order to benefit from time-sensitive transactions at a price of 15gwei. Making such an action profitable.

## Protocol Agnosticism
The benefit of current gas-tokens to the lay person is limited. A deep technical knowledge is required to create a solidity smart contract that utilizes gas token mechanics. Users only benefit when the contract they are using integrates gas tokens, such as seen in 1inch with it's chi integration.

Gas Save reduces this hurdle by wrapping essentially any transaction in a specific manner. This wrapping procedure is relatively low-skill. Which reduces this existing barrier to gas-economics.

## Flash Gas
It is entirely possible for arbitragers to utilize this protocol in combination with Flash-Swap mechanics to execute time critical/high gas-price transactions, at a large discount. This would foreseeably be facilitated by the flash swap functionality that AMM's offer. Liquidity providers in these AMM pools would benefit from a spike in price, and a portion of that arbitragers provide.

## Gas Token Mining
AMM liquidity pools of Gas Tokens provide a floating exchange rate for gas. When the floating exchange rate is lower than the current gas price, individuals can benefit by buying up gas tokens and using them to reduce transaction cost. Conversely, when the exchange rate is higher than the gas price, individuals can mint new tokens and sell them to liquidity pools in order to pocket the difference. This adds a completely new dimension for gas-economics.  

# Gas Savings & Benchmarks 

TODO - Awaiting a large, automated test net 

# Tokenomics

## Community distibution and Incentives

A number of community events and token distributions are planned as a means of encouraging the adoption of the Gas swap protocol. These events will aim to distribute a large portion of tokens in a fair manner. Allowing the DAO to be fair in its decision making process.

### Air Drop
An Air Drop is planned on BSC where the users that use the most gas during a certain period will be given tokens. This will be to raise awareness of the protocol.

### Minting and Wrapping Event
Community rewards of GSVE tokens will be rewarded to minters and wrappers as an incentive to use SG gas tokens over existing tokens. These will only be awarded in a scenario where GSVE has not been burned in the transaction.

### First Use Allocation
An allocation of GSVE tokens will be alotted to a user when they first invoke a transaction wrapper type, regardless of if the wrapper is Lite or Proxy.

## GSVE Token Allocation BSC

|Distribution|Tokens|%|
|-|-|-|
|Total|100 000 000|-|
|Foundation|30 000 000|30%|
|Team|15 000 000|15%|
|Advisors|5 000 000|5%|
|Initial Dex Offering|35 000 000|35%|
|Air Drop|5 000 000|5%|
|Community|10 000 000|10%|

## GSVE Token Allocation ETH

|Distribution|Tokens|%|
|-|-|-|
|Total|100 000 000|-|
|Foundation|30 000 000|30%|
|Team|15 000 000|15%|
|Advisors|5 000 000|5%|
|Initial Dex Offering|35 000 000|35%|
|Community|15 000 000|15%|

## Supply

The supply of SG1, SG2 and wrapped GST/Chi is entirely dictated by market forces and the underlying appetite for gas storage. There is no way to pre-allocate these tokens as this would result in non-existent gas being stored. Which would result in the protocol.

The supply of the GasSave Swap token is protocol dependant. For instance, users on BSC may choose to burn more GSVE than Ethereum users.

For each platforms GSVE allocations. The entirety of team funds, as well as half of the foundation and advisor funds will be vested in time lock contracts. This will reduce the number of tokens circulating from the 100 000 000 max supply, down to 67 500 000. A Half of the total token supply will be offered to the community via various promotions and the IDO's.

**note:** As users are encouraged to burn GSVE in order to save on protocol fees and withdraw from protocol gas pools, the protocol expects a long term decrease in the token supply.