# 🛢️ GasSwap Whitepaper 🛢️

👷🛢️⚠️ **GASSWAP IS A WORK IN PROGRESS - ASPECTS ARE SUBJECT TO CHANGE!** ⚠️🛢️👷

# Introduction

GasSwap is a gas saving protocol for Binance Smart Chain and Ethereum. It is designed to be protocol agnostic, easy to use, well tested and efficient. It is useful to blockchain users and developers alike, providing a useful hedge against future gas price increases from network traffic (Ethereum) and validator gas voting (Binance Smart Chain).

A Gas Token is a commodification of Gas fees. The aim of such a token is to frontload gas fees by paying for long term blockchain storage when gas is cheaper. The EVM provides a gas rebate mechanism for freeing up this storage, which reduces the gas cost of the entire transaction. The existing gas tokens, [GST1/GST2](https://gastoken.io/) and [CHI](https://blog.1inch.io/1inch-introduces-chi-gastoken-d0bd5bb0f92b), are limited in scope and application, and can only be used in scenarios where the rebate mechanism has been called from another smart contract. 

GasSwap widens the scope of transactions where Gas Token rebates can occur. Doing so by providing a universal transaction wrapper, that can be used to provide rebates without requiring smart contract developers to reference the protocol directly.

The overall aims of the GasSwap protocol is to; 
* Enable speculative gas investment
* Reduce long-term gas-price exposure for the individual
* Provide a source of fees to miners and validators during periods where blockchain activity is low (bear markets)
* Provide a vehicle for individuals to accrue gas.

This document outlines the core mechanics of GasSwap. Full Technical details will be available on protocol release, which is currently on track for 30 April 2021. The full source code of the project will be available on protocol release.

**[WIP]Protocol Website:** 
https://www.GasSwap.finance

**[WIP] Documentation:** 
https://www.GasSwap.finance/docs

**Code:** 
https://www.github.com/GasSwap


# Gas Swap Protocol

GasSwap introduces three tokens. Two Gas tokens and A protocol staking, savings and voting token. 

## Gas Tokens and Gas Savings
There are two gas swap native gas tokens, Stored Gas v1 and v2. As well as wrappers that unify interfaces of the existing GST and Chi tokens.

### Stored Gas V1 
Stored Gas v1 (SG1), largely inspired by the gas storage method presented in GST1. This method relies upon writing values in storage, and then freeing up these values when a rebate is required. SG1 Improves upon the ideas presented in GST, as well as formalising the asset as an ERC20 compliant token. SG1 uses a less efficient storage method than the one presented in GT2/Chi, and by extension SG2. Please refer to gas benchmarks for further information.

### Stored Gas V2 
Stored Gas v2 (SG2), uses the method presented in GST2 and Chi. This method stores gas by creating child contracts, and then self destructs these children when a rebate is required. SG2 is essentially the GasSwap version of CHI, with a number of adaptations and GasSwap specific improvements. The method used by SG2 is the current best-known method in terms of efficiency. Please refer to gas benchmarks for further information.

### Gas Token Wrappers
GST and Chi tokens do not have a common interface or standard. GasSwap introduces a wrapper that formalises the method calls. This allows the tokens to be used natively within the gas swap protocol. These formal wrappers introduce compatibility as well as the underlying fee mechanism.

### Transaction Wrapper
The transaction wrapper is the transaction agnostic part of the gas swap protocol which facilitates gas saving by wrapping an existing transaction with the token burning and gas saving elements of the gas tokens.

### UI

A UI will be available on MVP launch that will facilitate the ability to wrap transaction, Mint new tokens, Stake and vote. Additionally, In order to help users pick the correct number of gas tokens for a given transaction, the UI will include an optimal token burn calculator.

## GasSwap Token and Incentives

The GasSwap token (GSWAP) is the native token for the protocol. It bestows a few benefits to the holder. Some of these benefits are given when holders of the token can stake their tokens within a pool.

### Fee Redistribution

Whilst staked, holders benefit from the gas token fees that the protocol has accrued. This includes the tokens collected as SG1/SG2 minting fees, and GST1/2/Chi burning fees. 

The tokens are distributed to stakers proportional to the size of their stake. Due to Gas tokens using a non-standard decimal count, stakers will only be able to withdraw their accrued tokens when their pay out is above the minimal denomination of the underlying asset.

### Voting

Stakers can vote on changing the fees. Where a vote is allocated for each token staked. Voting allows users to adjust the minting fee for new SG tokens, and burning fee of non-protocol gas tokens. The stakers can choose to reduce fees entirely down to the lowest non-zero value, or change them to a valid value up to a upper cap of 10. Where upper cap/10^token decimals. So for chi and SG tokens, this upper cap would be 10, and for GST it would be 0.1, and the lower cap would be 1 and 0.1 respectively.

### Fee Reduction

If a user has staked tokens, they reduce minting and burning fees for themselves. This saving is initially half the non-staked value. Stakers can choose to adjust this value via voting. The user has the option to burn tokens, which removes the fee entirely, so long as this GasSwap burn occurs as part of a token minting or gas saving event.

# Fee Structure

| Token | Burning | Burning (Stakers)  | Minting | Minting (Stakers)|
|----------------------|---------|-------------|---------|------------------|
|SG1 & SG2| No Fee Ever | No Fee Ever |6 Tokens| 3 Tokens|
|GST1 & GST2| 0.02 Tokens| 0.01 Tokens| Refer to Token Specific Documentation| Refer to Token Specific Documentation|
|Chi| 2 Tokens | 1 Tokens| Refer to Token Specific Documentation| Refer to Token Specific Documentation|

Eventually minting and burning fees will be decided by GasSwap token holders using the DAO voting mechanism. 

# Benefits & Opportunities

The existence of Gas Swap creates a number of interesting opportunities. This section aims to highlight them.

## Gas Reduction
The most obvious benefit of the protocol is it's ability to offset the price of a high gas price transaction, by paying for gas when prices are lower. For instance, the average gas price on BSC is currently 15 gwei, whilst the minimum is 3gwei. It is entirely possible for individuals to passively mint SG gas tokens at 3gwei when the network is quiet. In order to benefit from time-sensitive transactions at a price of 15gwei. Making such an action profitable.

## Protocol Agnosticism
The benefit of current gas-tokens to the lay person is limited. A deep technical knowledge is required to create a solidity smart contract that utilizes gas token mechanics. Users only benefit when the contract they are using integrates gas tokens, such as seen in 1inch with it's chi integration.

Gas Swap reduces this hurdle by wrapping essentially any transaction in a specific manner. This wrapping procedure is relatively low-skill. Which reduces this existing barrier to gas-economics.

## Flash Gas
It is entirely possible for arbitragers to utilize this protocol in combination with Flash-Swap mechanics to execute time critical/high gas-price transactions, at a large discount. This would foreseeably be facilitated by the flash swap functionality that AMM's offer. Liquidity providers in these AMM pools would benefit from a spike in price, and a portion of that arbitragers provide.

## Gas Token Mining
AMM liquidity pools of Gas Tokens provide a floating exchange rate for gas. When the floating exchange rate is lower than the current gas price, individuals can benefit by buying up gas tokens and using them to reduce transaction cost. Conversely, when the exchange rate is higher than the gas price, individuals can mint new tokens and sell them to liquidity pools in order to pocket the difference. This adds a completely new dimension for gas-economics.  

# Gas Savings & Benchmarks 

TODO - Awaiting a large, automated test net 

# Tokenomics

The supply of SG1 and SG2 is dictated by market forces and the demand for gas. There is no way to pre-allocate these tokens as this would result in non-existent gas being stored. Which would eventually result in the protocol not working as no savings can be made.

The supply of the GasSwap Swap token is protocol dependant. For instance, users on BSC may choose to burn more GSWAP than Ethereum users, which would throw each protocols total supply out of sync. 

An Air Drop is planned on BSC where the users that use the most gas will be given tokens. This will be to raise awareness of the protocol.

Community rewards of GSwap tokens will be rewarded to minters as an incentive to use SG gas tokens over the others.

For each platforms GSwap allocations. The entirety of team funds, as well as half of the foundation and advisor funds will be vested in time lock contracts. This will reduce the number of tokens circulating from the 100 000 000 max supply, down to 67 500 000. Half of the token supply will be offered to the community via various promotions and IDO's.

**note:** As users are encouraged to burn GSwap in order to save on protocol fees, the protocol expects a long term inflationary response in its price action.

## GSwap Token Allocation BSC

|Distribution|Tokens|%|
|-|-|-|
|Total|100 000 000|-|
|Foundation|30 000 000|30%|
|Team|15 000 000|25%|
|Advisors|5 000 000|5%|
|Initial Dex Offering|35 000 000|35%|
|Air Drop|5 000 000|5%|
|Community|10 000 000|10%|

## GSwap Token Allocation ETH

|Distribution|Tokens|%|
|-|-|-|
|Total|100 000 000|-|
|Foundation|30 000 000|30%|
|Team|15 000 000|25%|
|Advisors|5 000 000|5%|
|Initial Dex Offering|40 000 000|40%|
|Community|10 000 000|10%|