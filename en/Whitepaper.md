<!--- 
 * Copyright ©️ 2018 Galt•Core Blockchain Company
  Nikolai Popeka [Basic Agreement](ipfs/QmaCiXUmSrP16Gz8Jdzq6AJESY1EAANmmwha15uR3c1bsS).

--->

# Galt Project Whitepaper
Nikolai Popeka @npopeka

"Civil government, so far as it is instituted for the security of property, is in reality instituted for the defense of the rich against the poor, or of those who have some property against those who have none at all. 

(A fair governance and justice systems will ensure that both the rich and the poor have property rights.)"

– Adam Smith, Wealth of Nations, Book V, Chapter I, Part II On the Expence of Justice

## Abstract
Galt Project is an international decentralized land and real estate property registry governed by DAO (Decentralized autonomous organization) and self-governance protocol for communities of homeowners built on top of Ethereum blockchain. Unlike the state property registries, the Galt Project is managed by a decentralized community of property owners using smart contracts. Creation of property records, resolution of disputes between owners, trading, mortgage, title insurance, and many other operations are performed on smart contracts. Also, property owners can unite in communities for voting, fundraising, and managing the common property.

## Introduction
At the heart of any society or state lies three social contracts:
- a set of laws and rules, that define the relationships of members of that society;
- private property and the procedure for its accounting i.e. property registries;
- community budgets, designed to protect property and society laws.

This system of those basic contracts has several fundamental problems:
- private property registries are not secured. They're stored in centralized databases or paper archives. Owners have no control over those registries. So, society needs a large and complex judicial branch to resolve disputes;
- different national registries use different geodetic datums;
- access to the Community budgets can be usurped by corrupt executive, judicial, and legislative branches;
- process of creation of Rules is challenging and also can be easily seized as well.

In this paper, we propose a mechanism for registering property, creating public budgets for its protection and laws with the help of smart contracts on the Ethereum blockchain. The proposed mechanism is blockchain-agnostic and can be implemented simultaneously on several blockchains with the capability of exchanging blockchain states. This document describes only general principles. A detailed description of the algorithms and logic of smart contracts is described in the documentation. Decentralized applications are a living organism, constantly changing and developing. Therefore, the principles described, documentation, and code are subject to change.

## Consistent property accounting on smart contracts

### Property Token
Land or real estate objects, unlike other real assets, like cars, art objects, and others, have the mathematical property of uniqueness. They physically occupy a specific position in space and can be uniquely determined only by their geographic coordinates. Two land plots, houses, or rooms can't physically have the same geographical coordinates. This means that an algorithm can be created that will ensure absolute data consistency on these objects. The core entity of the project is the NFT [ERC721 standart Ethereum token](http://erc721.org/). Each Token contains geospatial data and represents a particular land plot, whole building, room, or several rooms. We employ World Geodetic System (WGS84) as a primary Geodetic datum. Its measure of inaccuracy is believed to be less than 2 centimeters to the center mass, making it far more precise than any other datums.

There are four types of tokens:

- land-plot tokens represent a particular land plot with its unique geographical coordinates. Each token stores details on the boundaries of the land plot in the smart contract. They're set in the form of coordinates of the vertices of the plot. The token contains accurate coordinates in a different form: Latitude and Longitude, UTM (Universal Transverse Mercator), Geohash, and other Geodetic datums. Coordinates are three-dimensional. Every point of the land plot has its Altitude coordinate (also in different Geodetic datums). All this information is kept in blockchain;<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard7.png" alt="Accurate land plots coordinates in smart contract" width="700"/></p>
- whole-building tokens. They represent a whole building and contain its geographical coordinates, topology, and other identification data. The data regarding the topology of the building (wall and roof geometry) is stored in IPLD with the help of IPFS protocol;<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard8.png" alt="Accurate Buildings coordinates and topology in smart contract" width="700"/></p>
- room tokens - are similar to land-plot tokens, with the difference that each of them represents a specific area of a building rather than a land plot. Just as land-plot tokens, room tokens store geographical coordinates. The information about room topology (wall and ceiling geometry) is kept in IPLD with the help of IPFS protocol;<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard9.png" alt="Accurate Rooms coordinates and topology in smart contract" width="700"/></p>
- package tokens represent one or several room tokens united by their Owner.

### Token Ownership
We define a land or real-estate token ownership as the ability to transfer, sell, and perform various operations with a token in smart contracts using a private key. The token owner can be an external Ethereum address or an internal one, i.e., a smart contract. If a land or real-estate token is a joint property, then its owner is a multi-signature wallet. That said, a decentralized autonomous organization (DAO) or other smart contracts can own a token.
 
### Geospatial Data Management
The existence of a consistent registry of land plots, building and room objects enables owners to split and unite objects of the kind without involving any third parties. An owner can split and merge the geospatial data of the object within its original boundaries. If the token contains geographic coordinates of the land plot, the owner can split the initial plot for any amount of land plots within initial boundaries. Another case is if the owner has two tokens of two bordering land plots – in this circumstance, the owner can merge them into one. This principle is also applicable to Rooms. For such operations, computational geometry algorithms are used: the Weiler–Atherton clipping algorithm, Martinez-Rueda clipping algorithm, Sweep line algorithm, Ray casting algorithm, and many others.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard2.png" alt="Smart contract Land surveying" width="700"/></p>
If an Owner wants to change the original boundaries of a Land Plot or Room, they must make use of the Oracles. In both cases, all changes to geospatial data can be made only by a token owner themselves. There are likely cases, in which the initial recording of geographical coordinates occurred with an error and the owner of the token doesn’t want to change them for personal gain. In such cases, a claim may be created. Claims are resolved by the Arbitrators. This will be described in more detail below.

### Double ownership problem and its solutions
By "Land and Real estate double ownership", we mean the impossibility of sharing the same geographic coordinates at the same time. Unfortunately, the existing centralized registries aren't equipped with built-in independent automated solutions to block the creation of new records. In cases where there already is a record, it conflicts with a created one. For instance, when you try to create a new record regarding the boundaries of a land plot in the state registry, such a record can be created. Since the decision to create a record is settled by a specific authorized person – not a code, there will be two conflicting entries in the registry. Resolving this conflict will require the use of the state judicial system.

#### The algorithm for solving the problem
Each land plot, building, or room has a polygonal representation. The vertices of a polygon have coordinates in the [WGS84 standart](https://en.wikipedia.org/wiki/World_Geodetic_System#A_new_World_Geodetic_System:_WGS_84) — latitude, longitude, and altitude. Thereby, the task is reduced to mathematical verification of the new polygon intersecting with the already existing ones in the three-dimensional space. For consistency purposes, the calculation of intersections in the three-dimensional space is too complicated and can be reduced to checking intersections in a rectangular coordinate system in the Mercator projection considering altitude.
![Polygon intersection](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard16.png)

The task of checking the intersection of polygons for land plots and buildings comes down to checking the intersection on a plane in the Mercator projection excluding the altitude. 
The task of checking the intersection of the polygons of Rooms is reduced to checking the intersection on the plane in the Mercator projection, taking into account the minimum and maximum heights of the room.

![Polygon intersection](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard14.png)

To determine the fact of the intersection of polygons and intersection points, we use the following algorithms:
- Weiler–Atherton clipping algorithm; 
- Martinez-Rueda clipping algorithm.

#### Off-chain and on-chain hybrid sollution with Oracles when creating tokens
Checking the intersection of two polygons is feasible on the Ethereum blockchain and doesn't require substantial gas costs. At the same time, checking the intersection of one polygon with an unlimited number of polygons is impossible due to limitations in the number of calculations per block. Based on this, the intersection of the new polygon with all those written earlier must is a subject to an off-chain check. Anyone can put a deposit in the GALT tokens into a smart contract to become "Polygon intersection verification Oracle" and run the script. The script checks applications with new polygons one by one. The applicant pays for the Oracles in ETH. Verification of each application requires several independent Oracles. If all Oracles confirm that there is no intersection, then they withdraw the reward. If a part of the Oracles confirms there is no intersection and at least one Oracle provides the ID of the token, with which there is an intersection, the smart contract automatically rejects the application, pays all the reward to the honest Oracles and removes the deposit from dishonest ones in favor of the honest.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard10.png" alt="Off-chain double ownership check when creating Token for Land plot, Building or Room"/></p>
The smart contract employs three methods to uniquely verify the intersection of polygons:

- "ray casting algorithm" to determine the occurrence of one of the vertices of the polygon in another polygon;
- the intersection of two lines in the plane to determine the fact of the intersection of the edges of the polygons;
- the occurrence of a point along the height coordinate in the interval.

#### Off-chain and on-chain hybrid sollution with Deposits after creating tokens
To guarantee 100% impossibility of double ownership, the following mechanics can be used as an alternative or addition to the one described above. When creating a token of land plot or real estate, the Owner of the token must make a deposit in GALT ERC20 tokens. The deposit is stored in a contract that has the rights to create and destroy tokens. A deposit can be withdrawn by the Owner only if the land or real estate token is voluntarily destroyed. 
Anyone can provide the ID of two tokens that intersect to this contract. The contract verifies on-chain that the intersection exists. If it really is, token with last creation timestamp is destroyed, and the one who provided information to the contract receives deposit.

#### Sidechain sollution
The problem of checking the intersection of one polygon with an unlimited number of polygons is completely on-chain solvable. In this case, the initial creation of tokens of land plots and real estate objects occurs on the sidechain, in which a large volume of calculations can be made. Such a sidechain could be the blockchain on Parity Substrate or Cosmos SDK or any other. During the initial creation of the Token, the Validator nodes check for intersections and confirm the creation of the Token.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard11.png" alt="Sidechain double ownership check when creating Token for Land plot, Building or Room"/></p>
 
## Types of property ownership - "with State" / "with out State" / Private Registry

In the modern world, there is land (and real estate objects) divided between owners according to state registers. Recording in these registers and protecting the rights of owners is the responsibility of a state located in a particular territory. There are also territories not controlled by states. Correspondingly, they lack their registries and formal guarantors of the rights. Examples of such territories are Bir Tawil and Antarctica. The proposed system of smart contracts allows one to register ownership of land and real estate, in both types of territories.

Registration of such rights can be made in a single decentralized registry or many registries that have an Owner who can initially create tokens.
Some states are currently transferring land and real estate accounting functions to private companies. In this way, any private company can create its own registry for this purpose. Also Trust fund or any other legal entity can create its own registry in which it will be a guarantor of rights. This registry can be used for transactions and collective investment in real estate.

Thus, we define the following types of registries:
- single consistent decentralized property registry;
- private property registries.

## Creating property records, disputes resolution and use cases in Private property registries

### Creating Private property registry
Private property registry is ERC721 Ownable Smart contract on Ethereum. Anyone can create a private registry using the smart contract Factory by paying a fee in ETH or GALT and become its owner. The private registry Owner has the ability to create tokens with geographic coordinates and other linked data(address, floor, apartment or room number, photo and video, etc.) without any restriction and double ownership check. Tokens can be created for commercial purposes, as digital objects representing the right of ownership, lease rights, leasing agreements, shares in co-op, membership rights, etc. As well as for the self-government of property owners. In this case, the token gives the right to make a decision and vote in the created Community of Homeowners. 
The purpose and legal meaning of the token is fully determined by agreement with the Owner of the Private registry, as an individual or legal entity.

### Private property registry Owner
The Owner of a private registry is an address in the Ethereum blockchain, which can create tokens, change the parameters of registry contracts, change and destroy tokens with the approve of token holders, and also perform other operations. The owner may be an individual, legal entity, or DAO (for example Aragon organisation). In the last case, such a registry is decentralized since all operations are carried out by voting of DAO participants.

### Creating property records
In the case of using a private registry, operations to create token for land plot, house, appartment or office is carried out by the Owner of the registry or by those who have been given the corresponding rights by the Owner. Once created, the token can be transferred.

### Updating property records
In this case, the geographical and other data of the token are changed by the approval of the changes by the Token Holder and the Owner of the private registry. In the same way, if necessary, the token can be destroyed(burned).

### Private registries general architecture
![Private registries general architecture](https://github.com/galtproject/galtproject-docs/blob/master/images/Artboard22.jpg)

### Private registries Governance
![Private registries Governance](https://github.com/galtproject/galtproject-docs/blob/master/images/Artboard24.jpg)

### Private registries Commission
![Private registries Commission](https://github.com/galtproject/galtproject-docs/blob/master/images/Artboard23.jpg)

### Communities of Property owners in Private property registries
Creating Communities of homeowners in this case is no different from creating them in a Single consistent decentralized registry. Anyone can create a community and add members to it by voting of existing members. One community may contain tokens from different private registries. And at the same time, the owner of one token can be simultaneously in several communities(community of residents of one house, street, district or the whole city, etc.). More details are in "Communities of Property Owners" section. 
Since the community is a set of smart contracts, it itself can be the Owner of a private registry contract thus ensuring its decentralization.

## Creating property records, disputes resolution and use cases on the territories of existing States in single decentralized registry

### Creating property records

In Galt Project, any land and real-estate property owners can create their property tokens with the help of the decentralized community of cadastral engineers and notaries. Each Token represents property rights record for land or real estate. Anyone can pay a commission in ETH or GALT ERC20 and apply for creating a token through a smart contract. The application contains the geographical coordinates of the object, topology, IPFS media hashes (photos, video, point cloud file, Building Information Model, etc.), additional identification data (address, area, floor, room ID, etc.). The application is taken into work by the Cadastral Engineer and the Notary. They verify the correctness of the data and the applicant's property rights in a particular jurisdiction for a fee. With the application approved, a new object is checked for dual ownership. After that, a token is created.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard12.png" alt="A decentralized community of Cadastral engineers and Notaries"/></p>
This done, a Property Owner can:

- perform commercial operations with their property on the Ethereum smart contracts;
- split and merge the geospatial data of their tokens;
- unite in a community of homeowners and ensure self-governance;
- transfer property token to personal locker smart contract, stake Reputation from token, participate in governance and get part of the commission from all future registrations of new land plots and real estate and other contracts (see "Governance" and "Commission distribution" sections).

### Updating property records
In some cases, it may be necessary to update the data of land or real-estate token. This may happen if:
- while creating a token, geographic coordinates weren't defined correctly;
- media data (photos, video, point cloud file, etc.) or object parameters (area, number of rooms, parameters used in the sale, etc.) are outdated;
- the room in a building or the whole building was destroyed;
- the geographical coordinates of the building or room have changed due to the movement of the Earth's crust.

In this case, the data change occurs in the same way as the initial creation of the Token specified above. The owner submits an application in a smart contract, pays a commission. The Oracles check it and approve changes.

### Economic agents necessary for operations with land and real estate in the territory of existing States

#### Oracles
If someone wants to create a token of a land plot, building or room, there should be a decentralized self-governed mechanism for checking property rights and geographic coordinates. In Galt Project, this function is fulfilled by the Oracles. They're independent economic agents, who approve new token creation for a reward. Moreover, they perform a wide range of different operations: valuation, custodian service, etc. The Oracles have a deposit, which can be written off. To be able to earn the reward, they buy and deposit protocol governance token - ERC20 GALT Token. This deposit can be written off by the governance mechanism described below.

#### Custodians
In some jurisdictions, to make operations like land and real estate trading and p2p loans (with land and real estate as collateral) on Ethereum, Property owners need a decentralized third-party - the Custodians. The Custodians are legal entities in reliable jurisdictions. They're temporary owners of land or real estate and are legally obliged to re-register these rights in the state registry to the token owner. Also, they can convert their income from real estate to Ether or Stablecoins and transfer it to token owners. To provide paid services, they need a security deposit blocked in the smart contract. In case of an error or fraud, the deposit will be written off and used for prosecution and damages cover. The Custodians get a reward from token holders for interaction with government agencies and other Oracles. They act as a supranational property guarantor. For reducing the risks of fraud, each property is divided between 2-3 Custodians. If dishonest behavior is detected, their deposits will be fully withdrawn and used to retrieve property to their real owners.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard13.png" alt="custodians"/></p>
Each Custodian has a unique address. This way, the very Custodian can be a DAO – decentralized autonomous organization. In some cases, the Custodians are not necessary, if a state accepts blockchain transactions or there is no state at all, and the community of property owners itself acts as the guarantor of their rights.

#### Disputes resolution
Operations with land and real estate may lead to disputes and disagreements both between owners and professional participants: cadastral engineers, notaries, appraisers, custodians, etc. Here are some examples of such disputes:
- the initial creation of tokens contains an error. Geographic coordinates or property rights weren't determined correctly. The owner of the token wants to receive compensation from the Cadastral engineer;
- an error in geographic coordinates while applying for token creation. The landowner can't create a token since the land intersects with the land that was originally created incorrectly;
- when making a purchase and sale transaction, one of the parties wants to cancel it. For example, due to the fact that the seller withheld significant information;
- the Custodian committed fraud and sold the property. The owner of the token wants to receive the compensation necessary for the return of ownership through a state court.

The solution to these problems comes down to three types of operations:
- the possibility to write off the Oracle's deposit;
- the ability to block the work of a dishonest Oracle;
- the possibility of forcibly changing the geographical boundaries of a land plot or property. 

Their fulfillment requires the presence of a special elective role of a judge, who will act impartially in the interests of all parties in the dispute – the Arbitrator. 

#### GALT token Holders and their role
GALT Token Holders are the third force designed to balance the interests of Property owners and Oracles. Since one of the most effective decision-making systems is even-numbered odd vote (2 to 3, 4 to 7, etc.). They are protocol developers, enthusiasts and, possibly, speculators who are financially interested in the protocol developing, and the market price of the token increasing. The GALT token is described in more detail in the corresponding section.

#### Arbitrators 
Property owners, the GALT token holders, and the Oracles elect the Arbitrators, which is a special governance role. Each Arbitrator has a deposit in the GALT token. Any Property owner or Oracle or Arbitrator himself can create a claim about the Oracles, Arbitrators or Property owners dishonest behavior or mistake and pay the fee in ETH in the smart contract. Several Arbitrators take this claim for consideration. Each of them can create a proposal on what is to be done:

- what the size of the deposit is;
- from whom it should be written off;
- how the coordinates are meant to be changed;
- to apply a penalty or not on the Buyer or Seller according to the escrow smart contract terms;
- etc.

After that, they vote on each proposal. If the claim is approved, the deposit will be written off, the geographical coordinates will be changed, or the escrow contract will be canceled, etc. That said, the Arbitrators will also get their reward. If the decision isn't made on time, the Arbitrators will receive no reward, lose their deposits, and the claim can be taken up by another set of the Arbitrators. If the applicant is dissatisfied with the decision of the Arbitrators, he or she can create a new claim or ask the community to re-elect the Arbitrators.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard1.png" alt="Arbitrators"/></p>

#### Arbitrators Governance groups
In general, there are some technological restrictions in the current Ethereum that limit a possible maximum number of the Arbitrators. Also, there is a limit on the number of claims that can be considered by the Arbitrators during a specific period of time. So, to make this system scalable and facilitate operation with a large number of users, we should divide GALT Holders, Property Owners, Arbitrators, and Oracles into separate groups. The most obvious solution is to combine according to the geographical principle. There can be an unlimited number of Governance groups. In each group, the GALT holders, Property Owners, and Oracles vote to elect the Arbitrators. The Arbitrators deposit GALT as a deposit and provide their service in this group.
![Governance groups](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard17.png)
In addition to voting for the Arbitrators, by voting, the members of the group determine such parameters as:

- the size of the Oracles and Arbitrators deposits;
- the minimum amount of payment for the Oracle by role;
- the total number of Arbitrators in the group;
- the number of Arbitrators who consider the claim;
- the required number for making a decision
- etc.

#### Arbitrators elections
To make the governance system more reliable, the Arbitrators should be easily elected and re-elected, they should have economic incentive to honestly resolve disputes and they should represent all the participants of the Protocol – the property owners, Oracles and GALT token holders. In some cases, the goals of the property owners, Oracles and GALT token holders may not meet. So, they should have equal voting rights. The Property owners have the ERC721 tokens. Each token has its area in square meters. This is a basic variable for voting. The more land or real estate you have, the more votes you have. The Oracles have deposits in GALT. Deposits are used as a Voting variable. For the Galt tokens holders, the balance of tokens locked in a personal smart contract is used as voting power. 
![Arbitrators elections](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard15.png)
Each of these groups has only 1/3 оf the total Votes. The property owners, Oracles and GALT token holder get rewarded for staking reputation from protocol commission. We will describe it in the "Commission distribution" section. Also, the reputation accounting scheme is more complex – you can find more details below.

#### Possible Attack - Property owners and Arbitrators conspiracy 
There is a chance that a part of the Arbitrators and Property owners will conspire. The Property owners will create baseless claims, and the Arbitrators will approve them and write off deposits from the Oracles to the Arbitrators' and Property owners' benefit. If this will take mass proportions, the whole governance system will be disrupted, which isn't beneficial to all the participants. The majority of the Property Owners, Oracles, and GALT holders will change their vote and the Arbitrators will lose their votes and deposits. The only question is whether those deposits would be enough to cover the losses. 
There are several ways to avoid this attack:

- the Arbitrators should be public persons;
- the amount of GALT, which can be written off from a contract, should be limited for a particular period of time.
- the sum of all the Arbitrators deposits should be more than that amount;
- there should be a fast mechanism for casting votes and re-electing the Arbitrators. 

If a part of the Arbitrators will try to withdraw GALT from a contract, this will be noticed by the community, and all the Arbitrators or a part of them will be re-elected. The losses will be covered by the dishonest Arbitrators deposits.
 
### Use cases
With a consistent registry of property rights, various operations can be performed, like trading, collective investments, insurance, mortgages, and others. The guarantor of rights in such transactions can be the State itself (if a particular state accepts such transactions), international nominal owners – the Custodian (and the State they interact with) or the Property owners’ self-governance system (if there is no State).

#### Property trading with Custodians
It's essential to be able to perform fast international trading transactions with land and real estate tokens. The easiest way here is to use the Custodians' service. If the Sellers want to sell their token, they need to create a market order in a smart contract. The Buyers can make their offers. When buy and sell price are equal, the Seller can transfer the token to the escrow smart contract, and the Buyer can transfer ETH or other ERC20 tokens, including Stable Coins. Both parties can withdraw their tokens only if they confirm the deal and if the land and real-estate token has one or more Custodians. If there are no Custodian for the token, the Seller should register them, sign all necessary legal agreements and transfer the land or real estate to the Custodian. After that, both parties can confirm the deal and withdraw tokens. If at any stage of the deal the Buyer or Seller wants to cancel it, it's possible to make a cancellation request. Cancellation requests are reviewed by Arbitrators. They can apply a penalty on the Buyer or Seller according to the smart contract terms.

#### Property trading with State registration
In this case, Galt Protocol should be integrated with the Government property registry. After both Seller and Buyers tokens are transferred to the escrow contract, the State representative (a notary, judge, or state registrator) registers the deal in the government registry. After property rights were transferred from the Buyer to the Seller, he or she confirms the deal in the smart contract.

#### Collective investment in real estate
Today, investment in Land and Real Estate can only be made through an inefficient process involving a lot of useless intermediaries and lots of paperwork. For many people, it's too complicated and expensive. One of the reasons is that most REITs (Real Estate Investment Trusts) have restrictions on the minimum amount of investment, which makes it unaffordable for most people. The second main reason is that they don't accept cryptocurrencies as payment, which makes a quick cross-border purchase impossible. As a result, a large number of retail investors don't have access to Real Estate investments, which are the safest way to build long term savings.

Any Land or Real estate token can be blocked in the smart contract, as collateral. At the same time, a fixed number of the ERC20 tokens is issued and can be sold to investors. Each token represents a share in a specific property. The Custodian manages the property and converts property rental income (if rental income comes in fiat currencies) minus his commission into ETH or Stable Coins. The ERC20 token holders can withdraw this income from the smart contract with their ERC20 token balance. Also, if they are no longer satisfied with the Custodian, they will be able to change it to another by voting. As a result, anyone, from a New York student to Jakarta fruit seller can invest 20 dollars a month in a real estate object using their smartphones and get income.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard6.png" alt="Collective investment in real estate"/></p>

#### Property protection from Custodian malicious behavior
One of the main risks is dishonest actions of the Custodians, who, in the eyes of the state, are the owners of real estate. The Custodian may violate the legal agreement and sell the property or restrict access to it from the token owner. In this case, the token owner will be forced to go to the court to cancel the transaction and terminate the agreement with the Custodian. Such a legal procedure is costly and time-consuming. The solution to this problem is insurance of the risk of the Custodians' dishonest behavior. The real-estate token holders unite into small groups (300 - 500 owners) and regularly send ETH or Stable Coin, like DAI, to an insurance smart contract. If one of the token holders has a problem with a dishonest Custodian, they may receive a payment from the smart contract equivalent to the value of their property. The token itself is transferred to a smart contract and becomes the common property of other participants of the insurance fund. To return their property, the participants may allocate funds from the fund by voting. After the property is returned, the token can be sold by the fund to its original owner or put up for sale on the market.

#### Other use cases
The consistent global registry also makes it possible to perform the following range of operations:
- short or long term rental;
- mortgage. It can be issued in Stablecoins. The calculation of payments and the procedure for transferring a real estate token in case of violation of the payment schedule is determined by a smart contract;
- real-estate insurance;
- collective investment and construction management. For the construction of the property, a DAO can be created. The DAO Token Holders vote for contractor selection and construction financing. After the construction is completed, they receive shared ownership of the property;
- use ERC20 tokens as shares in co-op. Token holders can vote and decide on a board.

## Creating property records, property protection and use cases on the territories without existing states in single decentralized registry
There are the territories that are out of a state's sovereignty and the territories the rights to which were renounced by the state. They're called "Terra nullius" or "nobody's land". Examples of such territories are Bir Tawil in Africa and Marie Byrd Land in Antarctica, to name a few. Due to their isolated geographical position, associated risks, and harsh climate conditions, the settlement of such territories implies substantial financial expenses and a high likelihood of losing investments. Neither states themselves, nor private enterprises and investors are ready to do this. However, with sufficient financial resources, it's possible to create anything one could imagine in these territories: cities, industries, commercial centers, tax-free areas, etc.

An effective solution to the settlement problem may be crowdfunding with a large number of backers supporting the project through smart contracts. A particular territory can be divided into land plots. Potential buyers would participate in auctions that sell those land plots. All the funds collected from selling them would be passed to the community fund that is used for developing the infrastructure and serves as a guarantee of physical protection and legal recognition (if needed). Several billion dollars collected in cryptocurrency by a strong community of like-minded people would make it possible to build an airport, energy and transportation infrastructure, hire a private military company, and get other states' support.

This approach can be used both on Earth and beyond it. For example, on Moon on Mars. In the near future, the cost of a flight to Mars may amount 100,000 dollars at most. Just as in the Age of Discovery, hundreds and thousands of explorers will rush to those new worlds trying to find a better life and opportunities. With smart contracts, such a settler community will be able to unite, gather necessary funds, and build the society devoid of the imperfections of the existing state systems.

### Creating an updating property records for land
In this case, the auction mechanics are used for creating land-plot tokens. Anyone can pay a fee in ETH or GALT and create a Proposal to start an auction for land plots located on an unclaimed or disputed territory. The creator of the proposal creates Community of Homeowners in advance, to which all funds from the auction will be transferred, as well as the smart auction contract itself. The auction type is defined by the code of a smart contract (English auction ,Dutch auction, Sealed first-price auction, Vickrey auction and others). The proposal contains the geographical coordinates of the land and auction parameters, such as Min. number of Land Plots to sell to create tokens, Auction duration, Min. goal for crowdfunding, Address of Community of Homeowners contract, Auction currency ETH/ERC20 and others.

Protocol participants vote on the Proposal through Global Governance Voting Contract. If it is accepted, then the auction begins. Anyone can bet on the land plot. If the bet is won, as well as the minimum required number of plots is sold or the goal of raising funds is achieved, new tokens of land plots are created. The tokens are transferred to new owners, and all received funds are sent to Community Multisig. Unsold land plots may be sold later.

The participants in the new community choose managers who will manage the funds – to pay for the construction of infrastructure, physical protection of property, etc. They also vote for the adoption of laws and the collection of additional funds(a detailed description of the Communities is provided in the corresponding section).
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard21.png" alt="Creating property records, property protection and use cases on the territories without existing states"/></p>
Unlike land plots in the territories of existing states, these land plots are unchanged. Their geographical coordinates (latitude and longitude) can't be changed. The altitude coordinates can be changed by Cadastral engineers.

### Creating and updating property records for Real estate
Unlike land plots that are unchanged, buildings are created and destroyed. Thus, the creation of such tokens requires Cadastral engineers and Notaries. It happens the same way as in the territory of existing states. Anyone can pay a commission in ETH or GALT ERC20 and apply for creating or updating a token through a smart contract (as described in the "Creating property records, disputes resolution and use cases on the territories of existing States" section).

### Commercial operations with property
Since the guarantor of the property rights are the owners themselves, in this case, commercial operations don't require the Custodians participation. Ownership is transferred only through a smart contract. Such transactions should be accepted by all property owners in these territories.

### Property protection
In the territories not related to existing states, owners must provide protection of property themselves. For this purpose, they must create Homeowners Community (a detailed description of the communities is provided in the corresponding section). The owners create a regular tariff in the community and replenish the multisig with ETH, DAI, or any ERC20. These funds are used to pay for the services of the private police or army that provides physical protection for land and real estate.

## Decentralized registry Governance
The described system of smart contracts has a large number of parameters that require changes (depending on the current situation) as well as updating the code. These actions should be as decentralized as possible and at the same time carried out in the interests of the majority of participants.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard5.png" alt="Decentralized governance"/></p>
There are two levels of Governance:

- Arbitrators Governance groups;
- Global governance;

On the "Arbitrators Governance groups" level, the protocol participants (the Property owners, Oracles, Galt Holders) elect the Arbitrators and determine the Group parameters such as:

- the Oracles and Arbitrators Deposit amounts;
- the Oracles and Arbitrators minimum fee;
- voting thresholds;
- the total number of the Arbitrators in the group;
- the number of the Arbitrators who consider the claim;
- the required number for making a decision;
- and others.

Also they upgrade group contracts. 

On the "Global governance" level, the protocol participants (Property owners, Oracles, Galt Holders) determine global parameters such as:

- size of the general protocol commission and commision for particular smart contracts;
- commission distribution between GALT Auto buyback Contract and Reputation Staking Reward Contract (This is described in the "Commission distribution" section);
- upgrade contracts; 
- start Auctions for unclaimed territories (This is described in the "Creating property records, property protection and use cases on the territories without existing states" section);
- others.

### Reputation in Decentralized registry
The Property owners, GALT holders, and Oracles have Reputation, through which they manage the protocol. They elect the Arbitrators, determine protocol parameters, and upgrade smart contracts. The Property owners and GALT holders create a personal locker smart contract. They can transfer a Property token or GALT tokens to this contract and create Reputation in the Global Reputation contracts proportionally to the area of their property or the balance of the GALT tokens. From the global Reputation contracts, they create an additional Reputation in the Arbitrators Governance Group. The Oracles place a deposit in the GALT tokens in the Governance group and receive Reputation in exchange. All of the described roles stake Reputation on the Arbitrators and receive the reward from the general commission of the protocol.
![Reputation](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard18.png)
The Property owners and GALT holders create voting proposals in Global Governance and vote for them. The Oracles have Reputation only in the Governance groups, so they vote using it. 
For voting in a particular Governance Group, all the participants use their Reputation in this group.

### Staking rewards in Decentralized registry
Protocol participants are rewarded for choosing the Arbitrators. The reward is proportional to how much Reputation staked on the Arbitrators in a particular group. The Reward is given to:

- the GALT token holders for locking GALT and staking Reputation on the Arbitrators;
- the Property owners for locking a land plot or real estate token and staking Reputation on the Arbitrators;
- the Oracles for depositing GALT and staking Reputation on the Arbitrators.

We provide the opportunity to receive rewards not only to the GALT holders to encourage people to become the Oracles and register their property (a land and real estate). For example, the Property owners participating in the election of the Arbitrators will receive a part of the commission from all future registrations of new land plots and real estate and other contracts.

### Commission distribution in Decentralized registry
Most of the smart contracts have a commission in Ether and GALT for land and real estate tokens registration, tokens trading, Creating smart contracts with Factories (communities of homeowners, personal lockers, etc.), and so on. Commission amounts for different operations, and its distribution is set by voting. Commission from all contracts goes to Commission distribution Contract, which distributes it between GALT Auto buyback Contract and Reputation Staking Reward Contract in proportion set by the Global governance. Reputation Staking Reward Contract distribute ETH and GALT to the GALT holders, Property owners, and Oracles proportionally to their Reputation stakes. The GALT Auto buyback Contract uses the ETHs received to automatically purchase GALT from the GALT Automated Market Maker Contract, thereby increasing their price. The GALT tokens purchased and received from the commission are locked forever in the GALT Auto buyback Contract.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard19.png" alt="Commission distribution" width="700"/></p>

## Communities of Property Owners
In both types of the territories in Decentralized registry ("with State" / "with out State") or in any Private property registries, the Property owners can unite in communities for self-governance. The main goal of such a community is to unite owners in a specific territory, enact laws, and raise funds in ETH, DAI or any ERC20 to achieve common goals (physical protection of property, management of common property, construction of common infrastructure, etc.). In fact, the Community is a decentralized autonomous organization (DAO) of Property owners and may be an alternative to the municipal government. Such a system is devoid of the shortcomings of the existing public administration system since it can't be taken over by corrupt officials. 

Communities of Property Owners can be as small as an apartment house, or several neighboring houses, or as big as a whole city or region. Imagine a city where all residents (tenants and homeowners) can use their smartphone to raise funds to the budget in ETH or any ERC20, vote on important issues and choose city managers. All operations are performed on smart contracts and therefore cannot be blocked, restricted, or tampered.

### General community architecture
Each community is a set of smart contracts created with a factory. The Property owners create their personal Locker smart contract and transfer the token of the land plot or real estate to it. With this contract, they can create Reputation in proportion to the number of square meters of property. The opportunity to join the community is determined by voting of existing members. Owners use their Reputation to create Proposals and vote on them in Voting smart contract.

Voting smart contract can:
- approve new community members;
- change community parameters;
- enable and disable community Laws;
- choose professional managers, who manage the community budget;
- apply fines and exclude members from the community;
- set tariffs for regular and one-time fundraising in the community budget.

<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard20.png" alt="General community architecture" width="700"/></p>

### Community Reputation
Every member of a Community has Reputation. This is the number that determines the weight of the vote of each participant in the voting for decisions. Alice can have Reputation 45, Bob 52. In other words, Bob has more influence in Community, then Alice. A community member gets a reputation for:
- the number of square meters of his or her property(own or rented);
- by voting of other members for Community service;
- through a financial contribution to the community budget;
- for voting on important topics.

<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard4.png" alt="Reputation"/></p>

### Liquid democracy
If a Community member doesn't participate in the voting, they can pass their vote to another trusted member of the Community. In turn, the latter can give his or her votes to another trusted member of the Community. As a result, the votes of the passive "majority" will be transferred to the expert and the active "minority." Each Community member can get the vote back instantly whenever he or she wants. This way we solve the “apathy of voting” and “usurpation of power” problems.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Artboard3.png" alt="Liquid democracy" width=700/></p>

### Community Laws
Community members can pass and repeal laws by Voting. Each law is a record in a smart contract that contains the name of the law and the IPFS hash of a detailed document. Adopted laws are binding on all community members. Violating them may result in a community member being fined or expelled. The decision to impose a fine or exclusion is made by voting in Voting smart contract.

### Community Budget
Community Budget is stored on a Multisig wallet in the ETH and ERC20 tokens. It's replenished by community members through several Tariff smart contracts, which determine how and with what regularity community members should send ETH or ERC20 to Budget. 
There are several types of Tariffs:
- regular – community members regularly send funds in ETH or ERC20, for example, to pay for garbage collection or for the police services;
- one-time – community members send their funds once in ETH or ERC20 to achieve a common goal, such as building a road;
- mandatory – community members are required to send funds. If a member of the community doesn't fulfill his or her obligations to the community, he or she will receive a fine and can be excluded;
- voluntary - community members can voluntarily replenish the budget and receive rewards in the form of additional Reputation. For example, part of the community may pay for the construction of a new playground and get Reputation.

The spending of funds is controlled by professional managers, which are selected by voting. Each manager must have a deposit in ETH or ERC20, as a guarantee. The total amount of funds that can be paid from the budget for a period of time (week, month, or year) is equal to the total deposit of managers. Thus, in case of suspicion of corruption, Managers can be quickly re-elected, and deposits will remain in the community and cover all losses. Managers are rewarded from Community budget.

### GeeSome - An unstoppable social network protocol on top of IPFS
We've created the GeeSome protocol for Communities to freely communicate in encrypted chat groups, share images, video, text, or any data without risk of censorship or blocking.

### Compatibility with different frameworks for DAO
To create communities of homeowners, Property owners can use not only the Galt Project Community Framework, but also other frameworks for DAO’s such as DAOStack or Aragon.

## ERC20 GALT Token
GALT token is the ERC20 standard Ethereum utility token with a fixed supply of 42 mln. All 100% of GALT is distributed by means of the Automated Market Maker contract with Bonding curve. The project team receives GALT tokens by buying them from a contract.

### Token purpose
By issuing a token, we pursue four main goals:
- to create a single base for accounting the Oracles' deposits;
- to create a strong community of the Property owners, Oracles, Custodians, and sofware developers by incentive systems that enable coordination of network participants to achieve shared goals. Tokens incentivize them in an economic game towards an outcome that are mutually beneficial;
- create an incentive for the Arbitrators elections. The Galt holders can stake tokens to elect the Arbitrators and get the reward from protocol commission;
- create an incentive for protocol governance;
- create an incentive to spread information about the project. The GALT token holders will distribute information about the project, as each subsequent buyer of tokens increases their value.

### Token distribution
The GALT token is distributed by means of the Automated Market Maker contract with a Bonding curve. A bonding curve is a mathematical curve that defines a relationship between price and token supply or in our case the number of sold tokens. When a person purchases the token, each subsequent buyer has to pay a slightly higher price for each token, generating a potential profit for the earliest buyer. As more people find out about the project and buying continues, the value of each token gradually increases along the bonding curve. Early buyers who find Galt Project promising earlier, buy the curve-bonded GALT token, and then they can sell their token back and earn a profit in the future.

The Automated Market Maker contract (forked from Bancor) holds a balance of ETH and all fixed supply of the GALT Tokens. To buy GALT, the buyer sends some amount of ETH to a bonding curve contract’s Buy function which calculates the price of the token in a ETH and send the correct amount of GALT to the buyer. The Sell function works in reverse: The contract will calculate the GALT’s current selling price and will send the correct amount of ETH to seller. All GALT tokens are backed by ETH on 100% at any moment and forever.

Automated Market Maker contract has a CW=20% in Bancor Formula.

#### GALT token Price by GALT sold
This chart describes how the price of the token changes depending on how many tokens are purchased from the contract. With each purchase, the price increases along the curve, and with the sale decreases.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Price-by-TotalSupply.png" alt="GALT Price by TotalSupply" width="700"/></p>

#### GALT token Price by ETH balance
This chart describes how the price of the token changes depending on the ETH balance on the contract. The buyer sends ETH to the contract and receives GALT back, while the contract balance in ETH increases, and in GALT decreases. The seller, on the contrary, sends GALT and receives ETH back. The GALT balance increases, and the ETH balance decreases.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Price-by-ETH-on-contract.png" alt="GALT Price by ETH on contract" width="700"/></p>

#### Galt sold by ETH received
This chart describes how the amount of GALT sold by the contract depends on its ETH balance. To buy all total supply (42 million GALT), it will take 10 million ETH.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/images/Galt-sold-by-ETH-received.png" alt="GALT sold by ETH received" width="700"/></p>

### Economic model
The token model assumes a constant increase in its value due to the following factors:
- a part of the protocol commission in ETH automatically goes to buy the GALT tokens in the Automated Market Maker contract which continually increases the price;
- a part of the protocol commission is distributed as a reward for staking the GALT tokens on the Arbitrators. This makes the GALT token a source of income and stimulates demand for it;
- to become an Oracle, you need to place a deposit in the GALT tokens. The world has millions of land and real estate objects that can be tokenized. All of them will require thousands of Cadastral engineers, Notaries, and Custodians, which will increase the demand for GALT and its price.

### Risk of strong price reduction due to token sale by holders through Automated Market Maker contract
In the case of simultaneous sale of a large number of tokens through the Automated Market Maker contract, the price of the token can significantly decrease. What is not profitable for token holders, who will primarily try to sell the token through decentralized or centralized exchanges at a price equal to or slightly below the contract. Thus, the market price of the token on the exchanges will be almost equal to the current price of the contract.

## Protocol interoperability
The set of smart contracts described above can be executed in any Turing-complete virtual machine. Thus, the same or different version of contracts can simultaneously work on different blockchains with a different set of the Oracle and Arbitrators. Thus, tokens of land and real estate can be simultaneously created in the main chain of Ethereum, Polkadot or in TON. Each chain will have its own set of the Oracles and Arbitrators. Tokens with their geospatial data can be transferred by owners from one chain to another.

## Conclusion
The proposed mechanism can completely change the way people own and carry out operations with land and real estate as well as unite them to create public budgets for its management and protection. All data on property, transactions, votings, etc. will be stored forever on millions of computers in blockchain, can't be faked and can't be changed.
Using the Galt Project, people will be able to instantly and globally make property transactions without third parties, resolve disputes, perform other operations (rental, insurance, mortgage, etc.) and unite in Communities of Homeowners.

## References
- [DAOs, DACs, DAs and More: An Incomplete Terminology Guide
Posted by Vitalik Buterin on May 6, 2014](https://blog.ethereum.org/2014/05/06/daos-dacs-das-and-more-an-incomplete-terminology-guide/)
- [Mean Sea Level, GPS, and the Geoid By Witold Fraczek, Esri Applications Prototype Lab](https://www.esri.com/news/arcuser/0703/geoid1of3.html)
- [DAOstack. An Operating System for Collective Intelligence](https://daostack.io/wp/DAOstack-White-Paper-en.pdf)
- [Aragon Network](https://github.com/aragon/whitepaper)
- [Bancor Protocol Continuous Liquidity for Cryptographic Tokens through their SmartContracts by Eyal Hertzog, Guy Benartzi, Galia Benartzi](https://storage.googleapis.com/website-bancor/2018/04/01ba8253-bancor_protocol_whitepaper_en.pdf)
- [Bonding Curves Explained By Yos Riady](https://yos.io/2018/11/10/bonding-curves/)
- [Introducing Continuous Organizations by @thibauld](https://hackernoon.com/introducing-continuous-organizations-22ad9d1f63b7)
- [Bonding Curves In Depth: Intuition & Parametrization by Slava Balasanov](https://blog.relevant.community/bonding-curves-in-depth-intuition-parametrization-d3905a681e0a)
- [Weiler, Kevin and Atherton, Peter. "Hidden Surface Removal using Polygon Area Sorting", Computer Graphics, 11(2):214-222, 1977.](https://www.cs.drexel.edu/~david/Classes/CS430/HWs/p214-weiler.pdf)
- [A new algorithm for computing Boolean operations on polygons (2008, 2013) by Francisco Martinez, Antonio Jesus Rueda, Francisco Ramon Feito (and its C++ code)](http://www.cs.ucr.edu/~vbz/cs230papers/martinez_boolean.pdf)

## Appendix A: Bonding curve JS model

    const n = 4;
    const GaltTotalSupply = 42000000;
    const ethPaidPerIteration = 20;
    const iterationsCount = 2000000;
    const InitialGaltTokenSold = 4200000;
    const InitialEth = 100;

    const CW = 1 / (n + 1);

    let EthCollateral = InitialEth;
    let galtTokenSold = InitialGaltTokenSold;

    let galtPriceBefore;
    for (let round = 0; round < iterationsCount; round++) {
      let buyAmount = galtTokenSold * ((1 + ethPaidPerIteration / EthCollateral) ** CW - 1);
      galtTokenSold += buyAmount;
      EthCollateral += ethPaidPerIteration;
      const GaltBalance = GaltTotalSupply - galtTokenSold;
      const galtPriceAfter = (EthCollateral / (galtTokenSold * CW));

      if (GaltBalance < 0) {
        break;
      }
    }
