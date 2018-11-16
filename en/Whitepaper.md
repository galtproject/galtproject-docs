<!--- Copyright ©️ 2018 Galt•Space Society Construction and Terraforming Company
 * (Founded by [Nikolai Popeka](https://github.com/npopeka),
 * [Dima Starodubcev](https://github.com/xhipster),
 * [Valery Litvin](https://github.com/litvintech) by
 * [Basic Agreement](http://cyb.ai/QmSAWEG5u5aSsUyMNYuX2A2Eaz4kEuoYWUkVBRdmu9qmct:ipfs)).
 *
 * Copyright ©️ 2018 Galt•Core Blockchain Company
 * (Founded by [Nikolai Popeka](https://github.com/npopeka) and
 * Galt•Space Society Construction and Terraforming Company by
 * [Basic Agreement](http://cyb.ai/QmaCiXUmSrP16Gz8Jdzq6AJESY1EAANmmwha15uR3c1bsS:ipfs)).

--->
# Galt Protocol Whitepaper
Version 0.1
## Abstract
At the heart of any modern society or state lies three social contracts:
1. A set of laws and rules, that define the relationships of members of that society.
2. Private property and the procedure for its accounting.
3. Community budgets, designed to protect property and society Rules.

This system of those basic contracts has several fundamental problems:
1. Private property registries are not secured, they are stored in centralised databases or paper archives. Owners doesn’t control those registries so society need a vast judicial branch to resolve disputes. 
2. Access to the Community budgets can be usurped.
3. Proccess of creation of Rules is difficult and also can be easily usurped.

By creating a Galt Protocol we are trying to solve those problems. 
Galt Protocol is 
- a consistent geospatial registry of land and real estate (which can be used for trading, rental, creating CDP's or taking loans ); 
- system of multisigs for storing and managing community budgets; 
- voting system to define society rules by direct or delegative voting. 

## Protocol Overview
Galt Protocol is open - source software powered by Ethereum Blockchain. In Galt Protocol any property owners with the help of  protocol Oracles can create their property token - ERC721 SPACE Token. Each token represents land plot or a part of the building floor and contains geospatial data. Property Owners can:
- create community; 
- create one or several Delegative Community Multisigs; 
- elect multisigs managers; 
- create a set of Community Rules by direct or delegative voting
- make an operations with their property (buy, sell, rent, create CDP, take loans). 

![gp galt protocol essentials](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20Galt%20Protocol%20Essentials_Part_1.png)

## Property Token - ERC721 SPACE Token
The core entity of protocol is a ERC721 standart Ethereum token. Any property owners can pay comission to protocol and Oracles and create his SPACE Token.
Each Token cointains geospatial data and represents particular land plot or building floor. Token Owner can split and merge that geospatial data in the original boundaries without a third party. But if Owner want's to change original boundaries he must use the Oracles service. In both cases all changes to geospatial data can be made only by token owner himself.
![Property Token - ERC721 SPACE Token](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20Property%20Token%20-%20ERC721%20SPACE%20Token.png)

### Geospatial Data Management
Token owner can manage his token geospatial data. If token contains geographic coordinates of land plot, owner can split initial plot for any amount of land plots within initial boundaries. On other way if owner has two tokens of two bordering land plots, he can merge them into one. This principle works the same with floors of buildings.
![Geo Data Management](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20GeoData%20Management.png)

## Oracles
If someone wants to create a token of land plot or building floor, there should be decentralized self-managing mechanism for checking property rights and geographic coordinates. In Galt Protocol this function perfom Oracles. They are independent economic agents, who approve new token creation for reward. Also they have a deposit, which can be written of.
To be able to earn reward they buy and deposit protocol governance token - ERC20 GALT Token.
Property owners elect among themselves Arbitrators - special governance role. Any property owner can create a claim about Oracles dishonest behavior or mistake. If claim would be approved, than deposit will be written of. Arbitrators are elected dynamically. Voting is proportional to area of tokens in square meters.
![Oracles](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20Oracles%20Governance%20Model.png)

## Governance Utility Token - ERC20 GALT Token
As was written above Oracles should deposit ammount of governance tokens to be able to provide service and be rewarded. For that purpose we use ERC20 standart utility token GALT. First of all Galt Project is a community project. And it's ultimate goal is to create a new way of property accounting and self-governance and not to create another useless ICO. According to that all fixed initial supply will be diveded in three parts: 10% will be used as a deposit to create first Oracles, 10% will be sold on open auction and 80% will be sold by automatic marketmaking contract.
All GALT from an open auction will be transfered to participants and all ETH will be transfered to Marketmaking contract. The Galt Project will take 1% to cover development costs. Also Galt Project will get 1% from all buy and sell operations from DEX to be able to make further development. 5% of all Protocol commission will be automaticaly transfered to DEX. Thanks to this GALT price in ETH guaranteed to grow. 

Auction will start only after first version of protocol will be completely developed and fully audited.
![Governance ERC20 GALT Token ](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20Governance%20Token%20-%20ERC20%20GALT%20Token.png)
