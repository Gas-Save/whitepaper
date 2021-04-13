# 🛢️ GasSwap Whitepaper 🛢️

👷⚠️ **GASSWAP IS A WORK IN PROGRESS - ASPECTS ARE SUBJECT TO CHANGE!** ⚠️👷

# Introduction

GasSwap is a gas saving protocol for Binance Smart Chain and Ethereum. It is designed to be protocol agnostic, easy to use, well tested and efficient. It is useful to blockchain users and developers alike, providing a useful hedge against future gas price increases from network traffic (ethereum) and validator gas voting (binance smart chain).

A Gas Token is a commodification of Gas fees. The aim of such a token is to frontload gas fees by paying for long term blockchain storage when gas is cheaper. The EVM provides a gas rebate mechanism for freeing up this storage, which reduces the gas cost of the entire transaction. The existing gas tokens, [GST1/GST2](https://gastoken.io/) and [CHI](), are limited in scope and application, and can only be used in scenarios where the rebate mechanism has been called from another smart contract. 

GasSwap widens the scope of transactions where Gas Token rebates can occur. Doing so by providing a universal transaction wrapper, that can be used to provide rebates without requiring smart contract developers to reference the protocol directly.

The overal aims of the GasSwap protocol is to; 
* Enable speculative gas investment
* Reduce long-term gas-price exposure for the individual
* Provide a source of fees to miners and validators during periods where blockchain activity is low (ie bear markets)
* Provide a vehicle for individuals to accrue gas.

This document outlines the core mechanics and technical details for GasSwap. Some code is simplified for readability. The full source code of the project will be availible on GitHub.  

**[WIP]Protocol Website:** 
https://www.GasSwap.finance

**[WIP] Documentation:** 
https://www.GasSwap.finance/docs

**Code:** 
github.com/GasSwap

# Fee Structure

| Token | Burning | Burning (Stakers)  | Minting | Minting (Stakers)|
|----------------------|---------|-------------|---------|------------------|
|SG1 & SG2| No Fee Ever | No Fee Ever |6 Tokens| 3 Tokens|
|GST1 & GST2| 0.02 Tokens| 0.01 Tokens| Refer to Token Specific Documentation| Refer to Token Specific Documentation|
|Chi| 2 Tokens | 1 Tokens| Refer to Token Specific Documentation| Refer to Token Specific Documentation|

Eventually minting and burning fees will be decided by GasSwap token holders using a DAO voting mechanism. This will allow holders to decide on setting the fee between 0 (no fee) and an upper cap of 10, where the real upper cap value is upper cap / 10^ token decimals.

# Gas Swap Token Incentives

The Gas Tokens collected as SG1/SG2 minting fees, and GST1/2/Chi burning fees are redistributed to GasSwap token holders. This redistribution is done via a staking pool, where gas is distributed to stakers proportional to the size of their stake.

Users can reduce mint and burn fees by staking GasSwap tokens, and can eliminate fees entirely by burning GasSwap during the transaction.

# Gas Benchmarks 
