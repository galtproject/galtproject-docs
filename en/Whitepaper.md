<!--- 
 * Copyright ©️ 2018 Galt•Core Blockchain Company
  [Basic Agreement](ipfs/QmaCiXUmSrP16Gz8Jdzq6AJESY1EAANmmwha15uR3c1bsS).

--->

# Galt Project Whitepaper
Nikolai Popeka @npopeka

"Civil government, so far as it is instituted for the security of property, is in reality instituted for the defense of the rich against the poor, or of those who have some property against those who have none at all. 

(A fair governance and justice systems will ensure that both the rich and the poor have property rights.)"

– Adam Smith, Wealth of Nations, Book V, Chapter I, Part II On the Expence of Justice

## Abstract

Galt Project is international decentralized land and real estate property registry, governed by DAO (Decentralized autonomous organization) and self-governance protocol for communities of homeowners built on top of Ethereum blockchain. Unlike the state property registries, the Galt Project is managed by a decentralized community of property owners using smart contracts. 
Property records creation, resolution of disputes between owners, trading, mortgage, title insuranse and many other operations are performed on smart contracts. Also property owners can unite in communities for voting, fundraising and managing common property.

## Introduction
At the heart of any society or state lies three social contracts:
- a set of laws and rules, that define the relationships of members of that society;
- private property and the procedure for its accounting i.e. property registries;
- community budgets, designed to protect property and society laws.

This system of those basic contracts has several fundamental problems:
- private property registries are not secured, they are stored in centralised databases or paper archives. Owners doesn’t control those registries so society need a vast judicial branch to resolve disputes. 
- different national registries use different geodetic datums;
- access to the Community budgets can be usurped by corrupt executive, judicial and legislative branches;
- proccess of creation of Rules is difficult and also can be easily usurped.

In this paper, we propose a mechanism for registering property, creating public budgets for its protection and laws using smart contracts on the Ethereum blockchain. Proposed mechanism is blockchain agnostic and can be implemented simultaneously on several blockchains with the ability to exchange blockchain states. This document describes only the general principles. A detailed description of the algorithms and logic of smart contracts is described in the documentation. Decentralized applications - a living organism, changing and developing. Therefore, the principles described, documentation and code are subject to change.

## Consistent property accounting on Smart contracts

### Property Token
Land or real estate objects, unlike other real assets, such as cars, art objects and others, have the mathematical property of uniqueness. They physically occupy an unambiguous position in space and can be uniquely determined only by their geographic coordinates. Two land plots, houses or rooms cannot physically have the same geographical coordinates. This means that an algorithm can be created that will ensure absolute data consistency on these objects.
The core entity of project is a NFT [ERC721 standart Ethereum token](http://erc721.org/). Each Token cointains geospatial data and represents particular land plot, whole building, room or several rooms. We use World Geodetic System (WGS84) as a main Geodetic datum. Its error is believed to be less than 2 centimeters to the center mass, making it far more accurate than any other datums.

There are four types of tokens:
- land plots tokens - represent particular land plot with unique geographical coordinates. Each token stores information about the boundaries of the land plot in smart contract in the form of coordinates of the vertices of the plot. Token contains accurate coordinates in different form: Latitide and Longitude, UTM(Universal Transverse Mercator), Geohash and other Geodetic datums. Coordinates are three-dimensional. Every point of land plot has an Altitude coordinate (also in defferent Geodetic datums). All this information is stored in blockchain;
<p align="center"> <img src="https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-2.2-vector-08-big.png" alt="Accurate land plots coordinates in smart contract" width="700"/></p>
- whole building tokens  - represents whole bulding and contains it's geographical coordinates, topology and other identification data. Information of bulding topology (wall and roof geometry) is stored in IPLD by using IPFS protocol;
<p align="center"> <img src="https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-2.2-6-vector-06-big.png" alt="Accurate Buildings coordinates and topology in smart contract" width="700"/></p>
- room tokens - are same as Land plot tokens, except that each of them do not represent a Land plot, but a specific area of a building. As Land plot tokens, they store geographical coordinates. Information of room topology (wall and ceiling geometry) is stored in IPLD by using IPFS protocol;
<p align="center"> <img src="https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-2.2-vector-09-big.png" alt="Accurate Rooms coordinates and topology in smart contract" width="700"/></p>
- package tokens - represents one or several Room tokens, united by their Owner;

### Ownership
We define Land or real estate token ownership as the ability to transfer, sell and perform various operations with token in smart contracts using one's private key. Token owner can be an external Ethereum address or internal i.e Smart contract. If the Land or Real estate token is a joint property, then its owner is multisignature wallet. In addition, a decentralized autonomous organization (DAO) or other smart contracts can own a token.
 
### Geospatial Data Management
The presence of a consistent registry of land plots, buildings and rooms objects allows owners to split and unite such objects without involving third parties. Owner can split and merge object's geospatial data within its original boundaries. If token contains geographic coordinates of land plot, owner can split initial plot for any amount of land plots within initial boundaries. On other way if owner has two tokens of two bordering land plots, he can merge them into one. This principle works the same with Rooms. For those operations computational geometry algorithms are used: Weiler–Atherton clipping algorithm, Martinez-Rueda clipping algorithm, Sweep line algorithm, Ray casting algorithm and others.
<p align="center"> <img src="https://github.com/galtproject/galtproject-docs/blob/master/images/key%20features%201.2%20vector-03.png" alt="Smart contract Land surveying" width="700"/></p>
If Owner wants to change original boundaries of land plot or Room, he must use the Oracles. In both cases all changes to geospatial data can be made only by token owner himself. 
There are likely cases in which the initial recording of geographical coordinates occurred with an error and the owner of the token does not want to change them for personal gain. In such cases, a claim may be created. Claims are resolved by the Arbitrators. This will be described in more detail below.

### Double ownership problem and its solutions
We define "Land and Real estate double ownership" as the impossibility of simultaneously owning the same geographic coordinates. Unfortunately, existing centralized registries do not have built-in independent automated solutions to block the creation of new records in cases where a record already exists that conflicts with the created one. 
For example, when you try to create a new record about the boundaries of the land plot in the state registry, such a record can be created. Since the decision to create a record is made by a specific person authorized for that, not a code. There will be two conflicting entries in the registry, and resolving the conflict will require the use of a state judicial system.

#### The algorithm for solving the problem
Each land plot, building or room has a polygon representation. The vertices of the polygon have coordinates in the [WGS84 standart](https://en.wikipedia.org/wiki/World_Geodetic_System#A_new_World_Geodetic_System:_WGS_84) — latitude, longitude, and altitude. Thus, the task is reduced to mathematical verification that the new polygon does not intersect with those already existing in three-dimensional space. For consistency purposes, the calculation of intersections in three-dimensional space is too complicated and can be reduced to checking intersections in rectangular coordinate system in Mercator projection considering Altitude. 
![Polygon intersection](https://github.com/galtproject/galtproject-docs/blob/master/images/Galt_Polygon_intersection_02.png)

The task of checking the intersection of polygons for land plots and buildings comes down to checking the intersection on a plane in the Mercator projection excluding altitude. The task of checking the intersection of the polygons of Rooms is reduced to checking the intersection on the plane in the Mercator projection, taking into account the minimum and maximum heights of the room.

![Polygon intersection](https://github.com/galtproject/galtproject-docs/blob/master/images/Galt_Polygon_intersection_01.png)

For the task of determining the fact of the intersection of polygons and intersection points, the following algorithms are used:
- Weiler–Atherton clipping algorithm; 
- Martinez-Rueda clipping algorithm.

#### Off-chain and on-chain hybrid sollution
Checking the intersection of two polygons is feasible on the Ethereum blockchain and does not require large gas costs. At the same time, checking the intersection of one polygon with an unlimited number of polygons is impossible due to limitations in the number of calculations per block. Based on this, the intersection of the new polygon with all the ones written earlier must be checked off-chain. 
Anyone can put a deposit in GALT tokens into a smart contract to become "Polygon intersection verification Oracle" and run the script. The script checks applications with new polygons one by one. Applicant pays for the Oracles in ETH. To verify each application requires several independent Oracle. If all the Oracles confirm that there is no intersection, then they withdraw the reward. If part of the Oracles confirmed that there is no intersection and at least one Oracle has provided the ID of the token with which there is intersection into the smart contract. Smart contract automatically rejects the application, pays all the reward to the honest Oracle and removes the deposit from dishonest ones in favor of honest.
<p align="center"> <img src="https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-2.2-vector-07-big.png" alt="Off-chain double ownership check when creating Token for Land plot, Building or Room" width="700"/></p>
Smart contract uses three methods to uniquely verify the intersection of polygons:

- "ray casting algorithm" to determine the occurrence of one of the vertices of the polygon in another polygon;
- intersection of two lines in the plane to determine the fact of intersection of the edges of the polygons;
- occurrence of a point along the height coordinate in the interval.

#### Sidechain sollution
The problem can be solved completely on-chain. In this case, the initial creation of tokens of land plots and real estate objects occurs on the sidechain, in which a large volume of calculations can be performed. Such a sidechain could be the blockchain on Parity Substrate or Cosmos SDK or any other. During the initial creation of the token, the Validator nodes check for intersections and confirm the creation of the token.
<p align="center"> <img src="https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-1.2-vector-11-big.png" alt="Sidechain double ownership check when creating Token for Land plot, Building or Room" width="600"/></p>
 
## Types of property ownership - "with State" / "with out State"

In modern world there is land (and real estate objects) that is divided between owners on the basis of state registers. Recording in these registers and protection of the rights of owners is the responsibility of a state located in a particular territory. There are also territories that are not controlled by states and, accordingly, do not have their own registries and formal guarantors of rights. Examples of such territories are Bir Tawil[1] and Antarctica[2]. The proposed system of smart contracts allows one to register ownership of land and real estate, both in the first type of territories, and in the second.

## Creating property records, commercial operations, property protection and disputes resolution on the territories of existing States

### Creating property records

In Galt Project any property owners of land and real estate with the help of decentralized community of cadastral engineers and notaries can create their property token. Each token represents property rights record for land or real estate. Anyone can pay a commission in ETH or GALT ERC20 and apply through a smart contract for creating a token. The application contains the geographical coordinates of the object, topology, IPFS media hashes (photos, video, point cloud file, Building Information Model, etc.), additional identification data (address, area, floor, room ID etc.). Application is taken into work by the Cadastral Engineer and the Notary. They verify the correctness of the data and the property rights of the applicant in a particular jurisdiction for a fee. After the application is approved, the new object is tested for the absence of dual ownership and a token is created.
<p align="center"> <img src="https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-1.2-vector-14-big.png" alt="A decentralized community of Cadastral engineers and Notaries" width="700"/></p>
After that Property Owner can:

- perform commercial opeations with his property on Ethereum smart contracts;
- split and merge token's geospatial data;
- unite in community of homeowners for self-governance.

### Updating property records
In some cases, it may be necessary to update the data of land or real estate token:
- when creating a token, geographic coordinates were not defined correctly;
- media data (photos, video, point cloud file, etc.) or object parameters (area, number of rooms, parameters used in the sale, etc.) are out of date;
- the room in the building or the whole building were destroyed;
- the geographical coordinates of the building or room have changed due to the movement of the earth's crust.

In this case, the data change occurs in the same way as the initial creation of the token described above. The owner submits an application in a smart contract, pays a commission, and the Oracles check it and approve changes.

### Economic agents necessary for operations with land and real estate in the territory of existing States

#### Oracles
If someone wants to create a token of land plot or building floor, there should be decentralized self-governed mechanism for checking property rights and geographic coordinates. In Galt Project this function perfom Oracles. They are independent economic agents, who approve new token creation for reward. Also they perform different operations: valuation, custodian service etc. Oracles have a deposit, which can be written of.
To be able to earn reward they buy and deposit protocol governance token - ERC20 GALT Token. This deposit can be written of by governance mechanism described below.

#### Custodians
For operations like land and real easte trading and p2p loans (with land and real estate as collateral) on Ethereum, Property owners in some jurisdictions need a decentralized third party - Custodians. Custodians are legal entities in reliable jurisdictions. They are temporary owners of land or real estate and are legally obliged to re-register these rights in the state registry to the owner of the token. Also, they can convert fiat income from real estate to Ether or Stablecoins and transfer them to token owners. To provide paid services they need a security deposit, blocked in the smart contract. In case of an error or fraud, the deposit will be written off and used for prosecution and damages cover.  Custodians get a reward from token holders for interaction with government agencies and like other Oracles. They act like a supranational property guarantor.
To reduce the risks of fraud each property is divided between 2-3 Custodians. In case of dishonest behavier their deposits will be fully withdrawn and used to retrieve property to their real owners.
<p align="center"> <img src="https://github.com/galtproject/galtproject-docs/blob/master/images/custodians_01.jpeg" alt="custodians" width="700"/></p>
Each custodian has his own address. In this way, the custodian himself can be a DAO - decentralized autonomous organization.
In some cases Custodians are not necessary, because state accepts blockchain transactions or there is no state at all and the community of property owners themselves act as guarantor of their rights.

#### Disputes resolution
Operations with land and real estate will cause disputes and disagreements both between owners and professional participants: cadastral engineers, notaries, appraisers, custodians, etc. Here are some examples of such disputes:
- the initial creation of tokens contains an error. Geographic coordinates and / or property rights were not determined correctly. The owner of the token wants to receive compensation from the Cadastral engineer;
- the initial creation of tokens contains an error in geographic coordinates. The owner of the land cannot create a token, since his land intersects with the land that was originally created incorrectly.
- when making a purchase and sale transaction, one of the parties wants to cancel it. For example, due to the fact that the seller withheld significant information;
- Custodian committed a fraud and sold the property. The owner of the token wants to receive the compensation necessary for the return of ownership through a state court.
The solution to these problems comes down to three types of operations:
- possibility to write off deposit from oracle;
- the ability to block the work of a dishonest oracle;
- the possibility of forcibly changing the geographical boundaries of a land plot or property.
Fulfillment of them requires the presence of a special elective role of a judge, who will act impartially in the interests of all parties to the dispute - Arbitrator. 

#### Arbitrators 
Property owners, GALT token holders and Oracles elect Arbitrators - special governance role. Each Arbitrator has deposit in GALT token. Any Property owner or Oracle or Arbitrator himself can create a claim about Oracles, Arbitrators or Property owners dishonest behavior or mistake and pay fee in ETH in smart contract. 
Several arbitrators take a claim for consideration. Each of them can create a proposal on what should be done. What is the size of the deposit and from whom should be written of, how should the coordinates be changed, etc. After that they vote on each proposal. If claim would be approved, than deposit will be written of, geographical coordinates will be changed or escrow contract will be canceled, etc. Also Arbitrators get their reward. If the decision is not made on time, the Arbitrators do not receive a reward, lose their deposits, and the claim can be taken up by another set of Arbitrators. If the applicant is dissatisfied with the decision of the Arbitrators, he can create a new claim or ask the community to re-elect the Arbitrators.
<p align="center"> <img src="https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-1.2-vector-20-big.png" alt="Arbitrators" width="600"/></p>

#### Arbitrators Governance groups
In general there are technological limits in current Ethereum that restricts a maximum number of Arbitrators. Also there is a limit of number of claims, that can be considered by Arbitrators. So to make this system scalable and be able to work with large number of users, we should divide GALT Holders, Property Owners, Arbitrators and Oracles in groups. The most obvious solution is to combine them geographically. There can be unlimited number of Governance groups. In each group GALT holders, Property Owners and Oracles vote to elect Arbitrators. Arbitrators deposit GALT as a deposit and provide their service in this group.
![Governance groups](https://github.com/galtproject/galtproject-docs/blob/master/images/Governance_group_01.png)
In addition to voting for Arbitrators, members of the group by voting determine such parameters as the size of the Oracles and Arbitrators deposits, the minimum amount of payment for the Oracle by role, the total number of Arbitrators in the group, the number of Arbitrators who consider the claim, the required number for making a decision, etc.

#### Arbitrators elections
To make governance system more reliable Arbitrators should be easily elected and re-elected, they should have ecomomic incentive to honestly resolve disputes and they should represent all the participants of the Protocol - property owners, Oracles and GALT token holders. In some cases goals of property owners, oracles and GALT token holders can be opposite, so they should have equal voting rights. 
Property owners have ERC721 tokens. Each token has its area in square meters. This is a basic variable for voting. The more land or real estate you have - more votes. Oracles have deposits in GALT. Deposits are used as a Voting variable. For Galt tokens holders the balance of tokens locked in a personal smart contract is used as a voting power. 
![Arbitrators elections](https://github.com/galtproject/galtproject-docs/blob/master/images/arbitrators_elect_01.png)
Each of the groups has only 1/3 оf total Votes. 
Property owners, oracles and GALT token holder get rewarded for staking reputation from protocol comission. We will describe it in "Project commission distrubution" section. Also, the reputation accounting scheme is more complex and is described in more details below.

#### Possible Attack - Property owners and Arbitrators conspiracy 
There is a chance that part of Arbitrators and Property owners or Oracles will conspire. Property owners will create unfounded claims and Arbitrators will approve them and will write off deposits from Oracles to Arbitrators and Property owners benefit. If this will take massive character, then the hole governance system will be disrupted. Which is not beneficial to all participants. Majority of Property Owners, Oracles and GALT holders will change their vote and Arbitrators will lose their votes and deposits. The only question if those deposits would be enough to cover loses.
The are several solutions to avoid this attack:
- arbitrators should be public persons;
- an ammount of GALT, which can be written of from contract should be limited for particular period of time.
- summ of all Arbitrators deposit should be more then that ammount;
- there should be a fast mechanism for casting votes and reelection of Arbitrators.
If part of Arbitrators will try to withdraw GALT from contract, this will be noticed by the community and all Arbitrators or a part of them will be reelected. The loses will be covered by dishonest Arbitrators deposits.
 
### Commercial operations with property
With a consistent registry of property rights a various operations can be performed like trading, collective investments, insurance,mortgage and others. The guarantor of rights in such transactions can be the State directly (if a particular state accepts such transactions), international nominal owners - Custodian (and a State which they interact with) or Property owners self-governance system (if there is no State).

#### Property trading with Custodians
It's very important to be able to perform fast international tranding transactions with land and real estate tokens. The easiest way is to use Custodians service. 
If Seller wants to sell his token, he needs to create a market order in smart contract. Buyer can make his offer. When buy and sell price are equal, seller can transfer token to escrow smart contract and buyer can transfer ETH or any other ERC20 tokens, including Stable Coins.
Both parties can withdraw their tokens only if they will confirm the deal and if land and real estate token have one or more Custodians. If there are no Custodian for token, Seller should register them, sign all necessary legal agreements and transfer
land or real estate to Custodian. After that both parties can confirm the deal and withdraw tokens.
If at any stage of the deal buyer or seller wants to cancel it. He can make a cancellation request. Cancellation request are reviewed by Arbitrators. They can apply penalty on buyer or seller due to smart contract terms.

#### Property trading with State registration
In this case Galt Protocol should be integrated with Government property registry. After both seller's and buyer's tokens were transfered to escrow contract, state representetive (notary, judge or state registrator) registers deal in government registry. After property rights were transefered from buyer to seller, he confirms the deal in smart contract.

#### Collective investment in real estate
Today investment in Land and Real Estate can only be made through inefficient process involving a lot of useless intermediates and paper works. For many people it’s too complicated and costly. One of the reasons is that most REITs (Real Estate Investment Trusts) have restrictions on the minimum amount of investment that is not accessible to most people. The second main reason is that they do not accept cryptocurrencies as payment, which makes a quick cross-border purchase impossible. As a result large number of retail investors do not have access to Real Estate investments, which are safest way to build long term savings. 

Any Land or Real estate token can be blocked in the smart contract, as a collateral. At the same time, a fixed number of ERC20 tokens is issued and can be sold to investors. Each token represents a share in a specific property. The custodian manages the property and converts property's rental income (if rental income comes in fiat currencies) minus his commission into ETH or Stable Coins. ERC20 token holders can withdraw this income from smart contract by their ERC20 token balance. Also, if they are no longer satisfied with the Custodian, they will be able to change it to another by voting. As a result, anyone, from student in New York to fruit seller in Jacarta can invest 20 dollars per month in real estate object from the convenience of their smartphones and get income.
<p align="center"> <img src="https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-1.2-vector-19-big.png" alt="Collective investment in real estate" width="600"/></p>

#### Property protection from Custodian malicious behavior
One of the main risks is dishonest actions of Custodians who, in the eyes of the state, are the owners of real estate. Custodian may violate the legal agreement and sell the property or restrict access to it from the owner of the token. 
In this case, the owner of the token will be forced to go to court in order to cancel the transaction and terminate the agreement with the custodian. Such a trial can be costly and time consuming. The solution to this problem is insurance of the risk of dishonest behavior of custodians. All real estate token holders regularly send ETH or Stable Coin like DAI to an insurance smart contract on a voluntary basis. If one of the token holders has a problem with the dishonest custodian, he may receive a payment from the smart contract equivalent to the value of his property. The token itself transfers to smart contract and becomes the common property of the other participants of the insurance fund.

#### Other operations
The consistent global registry makes it possible to perform also the following operations:
- mortgage. It can be issued in Stablecoins. The calculation of payments and the procedure for transferring a real estate token in case of violation of the payment schedule is determined by a smart contract;
- real estate insurance;
- collective investment and construction management. For the construction of the property, a DAO can be created. DAO Token Holders vote for contractor selection and construction financing. After the construction is completed, they receive shared ownership in the property.

## Creating property records, commercial operations, property protection and disputes resolution on the territories without existing states

### Creating property records

### Commercial operations with property
Since the guarantor of the property rights are the owners themselves, in this case, commercial operations do not require Custodians. Ownership is transferred only through a smart contract. Such updates should be accepted by majority of participants through governance mechanisms.

### Property protection

## Governance
The described system of smart contracts has a large number of parameters that require changes depending on the current situation, as well as updating the code. These actions should be as decentralized as possible and at the same time carried out in the interests of the majority of participants.
<p align="center"> <img src="https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-1.2-vector-15-big.png" alt="Decentralized governance" width="600"/></p>
There are two levels of Governance:

- Arbitrators Governance groups;
- Global governance;

On "Arbitrators Governance groups" level protocol participants(Property owners, Oracles, Galt Holders) elect Arbitrators and determine Group parameters such as Oracles and Arbitrators Deposit amounts, Oracles and Arbitrators minimum fee, voting thresholds, total number of Arbitrators in the group, the number of Arbitrators who consider the claim, the required number for making a decision and others. Also they upgrade group contracts. 

On "Global governance" level protocol participants (Property owners, Oracles, Galt Holders) determine by voting global parameters such as size of the general protocol commission and commision for particular smart contracts, upgrade contracts and start Auctions for unclaimed territories (This is described in "Creating property records, commercial operations, property protection and disputes resolution on the territories without existing states" section).

### Reputation
Property owners, GALT holders and Oracles have a Reputation through which they manage the protocol. They select Arbitrators, determine protocol parameters and upgrade smart contracts. Property owners and GALT holders create personal locker smart contract. They can transfer Property token or GALT tokens to this contract and create a Reputation in the Global Reputation contracts in proportion to the area of their property or the balance of GALT tokens. From global Reputation contracts, they create an additional Reputation in the Arbitrators Governance Group. The Oracles place a deposit in GALT tokens in the Governance group and also receive a Reputation in exchange for this. All described roles stake Reputation on Arbitrators 
and receive reward from the general commission of the protocol.
![Reputation](https://github.com/galtproject/galtproject-docs/blob/master/images/Reputation.png)
Property owners and GALT holders create voting proposals in Global Governance and vote on them. Oracles have Reputation only in Governance groups, so they vote using it.
For voting in particular Governance Group all participants use their Reputation in this group.

### Staking rewards

## Communities of Property Owners

In both types of territories property owners can unite in communities for self-governance.

### General community architecture

### Community creation and entry

### Reputation

### Community Laws

### Community Budget

## ERC20 GALT Token

## Interoperability
The set of smart contracts described above can be executed in any Turing-complete virtual machine. Thus, the same or different version of contracts can simultaneously work on different blockchains with a different set of Oracle and Arbitrators. Thus, tokens of land and real estate can be simultaneously created in the main chain of Ethereum, Polkadot or in TON. Each chain will have its own set of Oracles and Arbitrators. Tokens with their geospatial data can be transferred by owners from one chain to another.

## The Plan

## References
- [Mean Sea Level, GPS, and the Geoid By Witold Fraczek, Esri Applications Prototype Lab](https://www.esri.com/news/arcuser/0703/geoid1of3.html)
