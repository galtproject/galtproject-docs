<!--- 
 * Copyright ©️ 2018 Galt•Core Blockchain Company
  [Basic Agreement](ipfs/QmaCiXUmSrP16Gz8Jdzq6AJESY1EAANmmwha15uR3c1bsS).

--->

# Galt Project Whitepaper

"Civil government, so far as it is instituted for the security of property, is in reality instituted for the defense of the rich against the poor, or of those who have some property against those who have none at all. 

(A fair governance and justice systems will ensure that both the rich and the poor have property rights.)"

– Adam Smith, Wealth of Nations, Book V, Chapter I, Part II On the Expence of Justice

## Abstract

Galt Project is international decentralized land and real estate property registry, governed by DAO (Decentralized autonomous organization) and self-governance protocol for communities of homeowners built on top of Ethereum blockchain. Unlike the state property registries, the Galt Project is managed by a decentralized community of property owners using smart contracts. 
Property records creation, resolution of disputes between owners, trading, mortgage, title insuranse and many other operations are performed on smart contracts. Also property owners can unite in communities for voting, fundraising and managing common property.

## Introduction
At the heart of any modern society or state lies three social contracts:
- A set of laws and rules, that define the relationships of members of that society.
- Private property and the procedure for its accounting i.e. property registries.
- Community budgets, designed to protect property and society Rules.

This system of those basic contracts has several fundamental problems:
- Private property registries are not secured, they are stored in centralised databases or paper archives. Owners doesn’t control those registries so society need a vast judicial branch to resolve disputes. 
- Access to the Community budgets can be usurped.
- Proccess of creation of Rules is difficult and also can be easily usurped.

In this paper, we propose a mechanism for registering property, creating public budgets for its protection and laws using smart contracts on the Ethereum blockchain. Proposed mechanism is blockchain agnostic and can be implemented simultaneously on several blockchains with the ability to exchange state.

## Property accounting on Smart contracts

### Property Token
The core entity of project is a NFT [ERC721 standart Ethereum token](http://erc721.org/). 
Each Token cointains geospatial data and represents particular land plot, whole building, room or several rooms. 

There are four types of tokens:
- land plots tokens - represent particular land plot with unique geographical coordinates. Each token stores information about the boundaries of the land plot in smart contract in the form of coordinates of the vertices of the plot. Token contains accurate coordinates in different form: Latitide and Longitude, UTM or Universal Transverse Mercator and Geohash. Coordinates are three-dimensional. Every point of land plot has an Altitude coordinate. All this information is stored on Ethereum blockchain;
![Accurate land plots coordinates in smart contract](https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-2.2-vector-08-big.png)
- whole building tokens  - represents whole bulding and contains it's geographical coordinates and other identification data. Information of bulding topology is stored in IPLD by using IPFS protocol;
![Accurate Buildings coordinates and topology in smart contract](https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-2.2-6-vector-06-big.png)
- room tokens - are same as Land plot tokens, except that each of them do not represent a land plot, but a specific area of a building. As Land plot tokens, they store geographical coordinates. Information of room topology is stored in IPLD by using IPFS protocol;
![Accurate Rooms coordinates and topology in smart contract](https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-2.2-vector-09-big.png)
- package tokens - represents one or several Room tokens, united by the owner;

Land or real estate objects, unlike other real assets, such as cars, art objects and others, have the mathematical property of uniqueness. They physically occupy an unambiguous position in space and can be uniquely determined only by their geographic coordinates. Two land plots, houses or rooms cannot physically have the same geographical coordinates. This means that an algorithm can be created that will ensure absolute data consistency on these objects.
 
### Geospatial Data Management
The presence of a consistent registry of land plots, buildings and rooms objects allows owners to split and unite such objects without involving third parties. Owner can split and merge object's geospatial data within its original boundaries. If token contains geographic coordinates of land plot, owner can split initial plot for any amount of land plots within initial boundaries. On other way if owner has two tokens of two bordering land plots, he can merge them into one. This principle works the same with Rooms. For those operations computational geometry algorithms are used: Weiler–Atherton clipping algorithm, Martinez-Rueda clipping algorithm, Sweep line algorithm, Ray casting algorithm and others.
![Smart contract Land surveying](https://github.com/galtspace/galtproject-docs/blob/master/images/key%20features%201.2%20vector-03.png)
If Owner wants to change original boundaries of land plot or Room, he must use the Oracles. In both cases all changes to geospatial data can be made only by token owner himself. 
There are likely cases in which the initial recording of geographical coordinates occurred with an error and the owner of the token does not want to change them for personal gain. In such cases, a claim may be created. Claims are resolved by the Arbitrators. This will be described in more detail below.

### Double ownership problem and its solutions
We define "Land and Real estate double ownership" as the impossibility of simultaneously owning the same geographic coordinates. Unfortunately, existing centralized registries do not have built-in independent automated solutions to block the creation of new records in cases where a record already exists that conflicts with the created one. 
For example, when you try to create a new record about the boundaries of the land plot in the state registry, such a record can be created. Since the decision to create a record is made by a specific person authorized fo that. There will be two conflicting entries in the registry, and resolving the conflict will require the use of a state judicial system.

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
Anyone can put a deposit in GALT tokens into a smart contract to become Oracle and run the script. The script checks applications with new polygons one by one. Applicant pays for the Oracles in Eth. To verify each application requires several independent Oracle. If all the Oracles confirm that there is no intersection, then they withdraw the reward. If part of the Oracles confirmed that there is no intersection and at least one Oracle has provided the ID of the token with which there is intersection into the smart contract. Smart contract automatically rejects the application, pays all the reward to the honest Oracle and removes the deposit from dishonest ones.

![Off-chain double ownership check when creating Token for Land plot, Building or Room](https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-2.2-vector-07-big.png)

Smart contract uses three methods to uniquely verify the intersection of polygons:
-  "ray casting algorithm" to determine the occurrence of one of the vertices of the polygon in another polygon;
-  intersection of two lines in the plane to determine the fact of intersection of the edges of the polygons;
- occurrence of a point along the height coordinate in the interval.

#### Sidechain sollution
The problem can be solved completely on-chain. In this case, the initial creation of tokens of land plots and real estate objects occurs on the sidechain, in which a large volume of calculations can be performed. Such a sidechain could be the blockchain on Parity Substrate. During the initial creation of the token, the Validator nodes check for intersections and confirm the creation of the token.

![Sidechain double ownership check when creating Token for Land plot, Building or Room](https://github.com/galtproject/galtproject-docs/blob/master/images/key-features-1.2-vector-11-big.png)
 
## Types of property ownership - "with State" / "with out State"

In modern world there is land (and real estate objects) that is divided between owners on the basis of state registers. Recording in these registers and protection of the rights of owners is the responsibility of a state located in a particular territory. There are also territories that are not controlled by states and, accordingly, do not have their own registries and formal guarantors of rights. Examples of such territories are Bir Tawil[1] and Antarctica[2]. The proposed system of smart contracts allows one to register ownership of land and real estate, both in the first type of territories, and in the second.

## Creating property records, commercial operations, property protection and disputes resolution on the territories of existing States

### Creating property records

In Galt Project any property owners with the help of decentralized community of cadastral engineers and notaries can create their property token. Each token represents property rights record for land or real estate. Anyone can pay a commission in ETH or GALT ERC20 and apply through a smart contract for creating a token. The application is taken into work by the Cadastral Engineer and the Notary. They verify the correctness of the data in the application and the ownership of the applicant for a fee. After the application is approved, the new object is tested for the absence of dual ownership and a token is created.

After that Property Owner can:
- perform commercial opeations with his property on Ethereum smart contracts;
- split and merge token's geospatial data;
- unite in community of homeowners for self-governance. 

### Economic agents necessary for operations with land and real estate in the territory of existing States

#### Oracles
If someone wants to create a token of land plot or building floor, there should be decentralized self-governed mechanism for checking property rights and geographic coordinates. In Galt Project this function perfom Oracles. They are independent economic agents, who approve new token creation for reward. Also they perform different operations: valuation, custodian service etc. Oracles have a deposit, which can be written of.
To be able to earn reward they buy and deposit protocol governance token - ERC20 GALT Token. This deposit can be written of by governance mechanism described below.

#### Custodians
For operations like land and real easte trading and p2p loans (with land and real estate as collateral) on Ethereum, Property owners in some jurisdictions need a decentralized third party - Custodians. Custodians are legal entities in reliable jurisdictions. They are temporary owners of land or real estate and are legally obliged to re-register these rights in the state registry to the owner of the token. Also, they can convert fiat income from real estate to Ether or Stablecoins and transfer them to token owners. To provide paid services they need a security deposit, blocked in the smart contract. In case of an error or fraud, the deposit will be written off and used for prosecution and damages cover.  Custodians get a reward from token holders for interaction with government agencies and like other Oracles. They act like a supranational property guarantor.
To reduce the risks of fraud each property is divided between 2-3 Custodians. In case of dishonest behavier their deposits will be fully withdrawn and used to retrieve property to their real owners.

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

#### Governance groups
In general there are technological limits in current Ethereum that restricts a maximum number of Arbitrators. Also there is a limit of number of claims, that can be considered by Arbitrators. So to make this system scalable and be able to work with large number of users, we should divide Property Owners, Arbitrators and Oracles in groups. The most obvious solution is to combine them geographically. In each geographical group Property Owners and Oracles will vote to elect Arbitrators. Arbitrators will deposit GALT as a deposit and will provide their service in this group.

#### Arbitrators elections

To make governance system more reliable Arbitrators should be easily elected and re-elected, they should have ecomomic incentive to honestly resolve disputes and they should represent all the participants of the Protocol - both property owners and oracles. To do that they should be elected among protocol participants. There is a two main roles of Users in Protocol - property owners and Oracles. In some cases their goals can be opposite, so they should have equal rights to become Arbitrators and to Vote. 
Property owners have ERC721 tokens. Each token has its area in square meters. This is a basic variable for voting. The more land or real estate you have - more votes. 
Oracles have deposits in GALT. Deposits also can be used as a Voting variable. Votes of both User's groups (Oracles and Property owners) should be equal, so voting power of Oracles and Property owners must be converted to one unit, as it described on scheme.

#### Possible Attack - Property owners and Arbitrators conspiracy 
There is a chance that part of Arbitrators and Property owners or Oracles will conspire. Property owners will create unfounded claims and Arbitrators will approve them and will write off deposits from Oracles to Arbitrators and Property owners benefit. If this will take massive character, then the hole governance system will be disrupted. Which is not beneficial to all participants of the Protocol. Majority of Property Owners and Oracles will change their vote and Arbitrators will lose their votes and deposits. The only question if those deposits would be enough to cover loses.
The are several solutions to avoid this attack:
- Arbitrators should be public persons;
- an ammount of GALT, which can be written of from contract should be limited for particular period of time.
- summ of all Arbitrators deposit should be more then that ammount;
- Arbitrators should be elected both by Property owners and Oracles;
- There should be a fast mechanism for casting votes and reelection of Arbitrators.

If part of Arbitrators will try to withdraw GALT from contract, this will be noticed by the community and all Arbitrators or a part of them will be reelected. The loses will be covered by dishonest Arbitrators deposits.
 
### Commercial operations with property
With a consistent registry of property rights a various operations can be performed like trading, loans, CDP's creation and others. The guarantor of rights in such transactions can be the State directly (if a particular state accepts such transactions), international nominal owners - Custodian (and a State which they interact with) or Property owners self-governance system (if there is no State).

#### Property trading with Custodians
It's very important to be able to perform fast international tranding transactions with land and real estate tokens. The easiest way is to use Custodians service. 
If Seller wants to sell his token, he needs to create a market order in smart contract. Buyer can make his offer. When buy and sell price are equal, seller can transfer token to escrow smart contract and buyer can transfer Ether or any other ERC20 tokens, including Stable Coins.
Both parties can withdraw their tokens only if they will confirm the deal and if land and real estate token have one or more Custodians. If there are no Custodian for token, Seller should register them, sign all necessary legal agreements and transfer
land or real estate to Custodian. After that both parties can confirm the deal and withdraw tokens.

If at any stage of the deal buyer or seller wants to cancel it. He can make a cancellation request. Cancellation request are reviewed by Oracles. They can apply penalty on buyer or seller.

#### Property trading with State registration
In this case Galt Protocol should be integrated with Government property registry. After both seller's and buyer's tokens were transfered to escrow contract, state representetive (notary, judge or state registrator) registers deal in government registry. After property rights were transefered from buyer to seller, he confirms the deal in smart contract.

#### Property protection

## Creating property records, commercial operations, property protection and disputes resolution on the territories without existing states

### Creating property records

### Commercial operations with property
Since the guarantor of the property rights are the owners themselves, in this case, commercial operations do not require Custodians. Ownership is transferred only through a smart contract.

### Property protection

## Governance

## Communities of Property Owners

In both types of territories property owners can unite in communities for self-governance.

### General community architecture

### Community creation and entry

### Reputation

### Community Laws

### Community Budget

## ERC20 GALT Token
As was written above Oracles should deposit ammount of governance tokens to be able to provide service and be rewarded. For that purpose we use ERC20 standart utility token GALT. First of all Galt Project is a community project. And it's ultimate goal is to create a new way of property accounting and self-governance and not to create another useless ICO. According to that all fixed initial supply will be diveded in three parts: part will be used as a deposit to create first Oracles, part will take Galt Project team, part will be sold on open EOS-like auction and final part will be sold by automatic marketmaking contract, forked from Bancor.
All GALT from an auction will be transfered to participants and all ETH will be transfered to Marketmaking contract.

## Project commission distrubution


