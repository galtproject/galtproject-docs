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
Version 0.2

Civil government, so far as it is instituted for the security of property, is in reality instituted for the defense of the rich against the poor, or of those who have some property against those who have none at all. 

(A fair justice system will ensure that both the rich and the poor have property rights.)

– Adam Smith, Wealth of Nations, Book V, Chapter I, Part II On the Expence of Justice



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
Each Token cointains geospatial data and represents particular land plot or building floor. 
![Consistent Geospatial Registry](https://github.com/galtspace/galtproject-docs/blob/master/images/key%20features%201.2%20vector-01.png)

There are three types of tokens:
- land plots tokens - represent particular land plot with unique geographical coordinates. Each token stores information about the boundaries of the land plot in smart contract in the form of coordinates of the vertices of the plot. Token contains accurate coordinates in different form: Latitide and Longitude, UTM or Universal Transverse Mercator and Geohash. Coordinates are three-dimensional. Every point of land plot has an Altitude coordinate in metres above sea level. All this information is stored on Ethereum blockchain;
- building areas tokens - are same as Land plot tokens, except that each of them do not represent a land plot, but a specific area of a building. As Land plot tokens, they store geographical coordinates. Unlike Land plot tokens, Building area tokens store Altitude coordinate as a Height above ground in meters;
- pre-defined real-estate tokens - sometimes it's not necessary to store information about precise coordinates for part of the building. In that case it's enought to store building address and appartment number or any other identification data;

Token Owner can split and merge that geospatial data in the original boundaries without a third party. But if Owner want's to change original boundaries he must use the Oracles service. In both cases all changes to geospatial data can be made only by token owner himself.
![Property Token - ERC721 SPACE Token](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20Property%20Token%20-%20ERC721%20SPACE%20Token.png)

### Geospatial Data Management
Token owner can manage his token geospatial data. If token contains geographic coordinates of land plot, owner can split initial plot for any amount of land plots within initial boundaries. On other way if owner has two tokens of two bordering land plots, he can merge them into one. This principle works the same with floors of buildings.
![Smart contract Land surveying](https://github.com/galtspace/galtproject-docs/blob/master/images/key%20features%201.2%20vector-03.png)
![Geo Data Management](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20GeoData%20Management.png)

## Oracles
If someone wants to create a token of land plot or building floor, there should be decentralized self-managing mechanism for checking property rights and geographic coordinates. In Galt Protocol this function perfom Oracles. They are independent economic agents, who approve new token creation for reward. Also they perform different operations: valuation, custodian service etc. Oracles have a deposit, which can be written of.
To be able to earn reward they buy and deposit protocol governance token - ERC20 GALT Token.
Property owners and Oracles elect among themselves Arbitrators - special governance role. Any Property owner or Oracle or Arbitrator can create a claim about Oracles, Arbitrators or Property owners dishonest behavior or mistake. If claim would be approved, than deposit will be written of. Arbitrators are elected dynamically by Property Owners and Oracles.
![Oracles](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20Oracles%20Governance%20Model.png)

### Limitations and User Groups
In general there are technological limits in current Ethereum that restricts a maximum number of Arbitrators in Multisig and Voting process. Also there is a limit of number of claims, that can be considered by Arbitrators. So to make this system scalable and be able to work with large number of users, we should divide Property Owners, Arbitrators and Oracles in groups. The most obvious solution is to combine them geographically. In each geographical group of Property Owners and Oracles will vote to elect among themselves. Arbitrators and Oracles will deposit funds in group Multisig and will provide their service in this group.

![Oracles Groups](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20MultiOracles.png)

### Possible Attack - Property owners and Arbitrators conspiracy 
There is a chance that part of Arbitrators and Property owners or Oracles will conspire. Property owners will create unfounded claims and Arbitrators will approve them and will write off deposits from Oracles to Arbitrators and Property owners benefit. If this will take massive character, then the hole governance system will be disrupted. Which is not beneficial to all participants of the Protocol. Majority of Property Owners and Oracles will change their vote and Arbitrators will lose their votes and deposits. The only question if those deposits would be enough to cover loses.
The are several solutions to avoid this attack:
- Arbitrators should be public persons;
- an ammount of GALT, which can be written of from multisig should be limited for particular period of time.
- summ of all Arbitrators deposit should be more then that ammount;
- Arbitrators should be elected both by Property owners and Oracles;
- There should be a fast mechanism for casting votes and reelection of Arbitrators.

If part of Arbitrators will try to withdraw GALT from multisig, this will be noticed by the community and all Arbitrators or a part of them will be reelected. The loses will be covered by dishonest Arbitrators deposits.

### Arbitrators Voting
To make governance system more reliable Arbitrators should be easily elected and re-elected, they should have ecomomic incentive to honestly resolve disputes and they should represent all the participants of the Protocol - both property owners and oracles. To do that they should be elected among protocol participants. There is a two main roles of Users in Protocol - property owners and Oracles. In some cases their goals can be opposite, so they should have equal rights to become Arbitrators and to Vote. 
Property owners have ERC721 tokens. Each token has its area in square meters. This is a basic variable for voting. The more land or real estate you have - more votes. 
Oracles have deposits in GALT. Deposits also can be used as a Voting variable. Votes of both User's groups (Oracles and Property owners) should be equal, so voting power of Oracles and Property owners must be converted to one unit, as it described on scheme.

![Arbitrators Voting](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20Arbitrators%20Voting.png)

### Custodians
For operations like land and real easte trading and p2p loans (with land and real estate as collateral) on Ethereum, Property owners in some jurisdictions need a decentralized third party - Custodians. Custodians here perform the role of nominal owners for property. It's a company or a public person with good reputation and his own assets. Custodians hold property until SPACE Token holder will come and ask to register property rights in the state register to him. Custodians get a reward from token holders for interaction with government agencies and like other Oracles, deposit pledges in GALT. They act like a supranational property guarantor.
To reduce the risks of fraud each property is divided between 5-7 Custodians. In case of dishonest behavier their deposits will be fully withdrawn and used to retrieve property to their real owners.

In some cases Custodians are not necessary, because state accepts blockchain transactions or there is no state at all and the community of property owners themselves act as guarantor of their rights.

![Custodians management](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20Custodians%20Management.png)

## Governance Utility Token - ERC20 GALT Token
As was written above Oracles should deposit ammount of governance tokens to be able to provide service and be rewarded. For that purpose we use ERC20 standart utility token GALT. First of all Galt Project is a community project. And it's ultimate goal is to create a new way of property accounting and self-governance and not to create another useless ICO. According to that all fixed initial supply will be diveded in three parts: part will be used as a deposit to create first Oracles, part will take Galt Project team, part will be sold on open EOS-like auction and final part will be sold by automatic marketmaking contract, forked from Bancor.
All GALT from an auction will be transfered to participants and all ETH will be transfered to Marketmaking contract. 

![Governance ERC20 GALT Token ](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20Governance%20Token%20-%20ERC20%20GALT%20Token.png)

## Operations with property
With a consistent registry of property rights a various operations can be performed like trading, loans, CDP's creation and others. The guarantor of rights in such transactions can be the State directly (if a particular state accepts such transactions), international nominal owners - Custodian (and a State which they interact with) or Property owners self-governance system (if there is no State).
![Real Estate operations on Ethereum ](https://github.com/galtspace/galtproject-docs/blob/master/images/key%20features%201.2%20vector-07.png)

## Property trading with Custodians
If seller and buyer want to make a fast transactions or want to stay anonimous or if the particular State doesn't accepts blockchain transaction, they can 
![Trading with Custodians](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20Land%20and%20Real%20Estate%20Trading%20Without%20State%20Registration.png)

## Property trading with State registration

![Trading with State](https://github.com/galtspace/galtproject-docs/blob/master/images/GP%20Land%20and%20Real%20Estate%20Trading%20With%20State%20Registration.png)

## About Copyright and Software licenses
The main purpose of Galt Protocol is to create open and reliable instrument for self-government communities of Property Owners. According to that, one of our main goals in Galt Project is to create pure community driven and open software product. For now Galt Project if fully self-funded, we have certain vision and we want to implement it. To ensure the achievement of our vision, before the launch, protocol is open-sourced, but it is and it will be our intellectual property. You need to ask us, if you want to participate or use our code. We will decide if it's possible at that moment.
