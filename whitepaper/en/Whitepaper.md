<!--- 
 * Copyright ©️ 2018 Galt•Core Blockchain Company
  Nikolai Popeka [Basic Agreement](ipfs/QmaCiXUmSrP16Gz8Jdzq6AJESY1EAANmmwha15uR3c1bsS).

--->
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/logo-black-1.png" alt="logo-black-360" width="200"/></p>

# Galt Project Whitepaper
by Nikolai Popeka @npopeka

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

- land-plot tokens represent a particular land plot with its unique geographical coordinates. Each token stores details on the boundaries of the land plot in the smart contract. They're set in the form of coordinates of the vertices of the plot. The token contains accurate coordinates in a different form: Latitude and Longitude, UTM (Universal Transverse Mercator), Geohash, and other Geodetic datums. Coordinates are three-dimensional. Every point of the land plot has its Altitude coordinate (also in different Geodetic datums). All this information is kept in blockchain;<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard7.png" alt="Accurate land plots coordinates in smart contract" width="700"/></p>
- whole-building tokens. They represent a whole building and contain its geographical coordinates, topology, and other identification data. The data regarding the topology of the building (wall and roof geometry) is stored in IPLD with the help of IPFS protocol;<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard8.png" alt="Accurate Buildings coordinates and topology in smart contract" width="700"/></p>
- room tokens - are similar to land-plot tokens, with the difference that each of them represents a specific area of a building rather than a land plot. Just as land-plot tokens, room tokens store geographical coordinates. The information about room topology (wall and ceiling geometry) is kept in IPLD with the help of IPFS protocol;<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard9.png" alt="Accurate Rooms coordinates and topology in smart contract" width="700"/></p>
- package tokens represent one or several room tokens united by their Owner.

### Meaning of property ownership
What is the right of property? In a nutshell, it’s a social contract agreed upon by the individuals living in the same territory. This contract specifies who owns a property. It also represents the capability of these individuals to form a budget to protect the owned property and enforce a judicial system to adjudicate disputes.
Modern governments collect taxes, which helps to register and account property rights, protect property (with the police or the military) and litigate controversies. But is a government a safeguard of property rights? Yes and no at the same time. Any government is primarily a mechanism of collecting and managing money. If at some point of time people can’t pay taxes and fill the treasury, the state won’t be able to secure the rights of its citizens effectively.
It means but one thing. Only individual and his neighbors, living in the same house, on the same street, or in the same city, can warrant their rights on an apartment, land, or house. If they can form a strong union among themselves, then they can protect their rights. 

Thus, as in the case of any cryptocurrency or digital asset, land and real estate ownership can be taken into account and transferred using smart contracts without intermediaries and third parties on blockchain, if there is an agreement between a large number of people in a certain territory on the use of this technology.
Absolutely the same, the collection of public budgets for property protection and mechanisms for making joint decisions between owners can be implemented using smart contracts.

### Token Ownership
We define a land or real-estate token ownership as the ability to transfer, sell, and perform various operations with a token in smart contracts using a private key. The token owner can be an external Ethereum address or an internal one, i.e., a smart contract. If a land or real-estate token is a joint property, then its owner is a multi-signature wallet. That said, a decentralized autonomous organization (DAO) or other smart contracts can own a token.

### Token rental
We define a land or real-estate token rental as the ability to perform various operations with a token (right of use, sublease, participation in the community of homeowners and others) according to Smart contract between Token Owner and Token Tenant using their private keys.
 
### Geospatial Data Management
The existence of a consistent registry of land plots, building and room objects enables owners to split and unite objects of the kind without involving any third parties. An owner can split and merge the geospatial data of the object within its original boundaries. If the token contains geographic coordinates of the land plot, the owner can split the initial plot for any amount of land plots within initial boundaries. Another case is if the owner has two tokens of two bordering land plots – in this circumstance, the owner can merge them into one. This principle is also applicable to Rooms. For such operations, computational geometry algorithms are used: the Weiler–Atherton clipping algorithm, Martinez-Rueda clipping algorithm, Sweep line algorithm, Ray casting algorithm, and many others.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard2.png" alt="Smart contract Land surveying" width="700"/></p>
If a Token Owner wants to change the original boundaries of a land plot, building or room/apartment, he must use procedures defined by the code of the corresponding registry (Ownable Private property registry, Prof of Location Token Curated Property Registry, Oracles property registry, Dynamic Prof of Location Property Registry). This will be described in more detail below.

### Double ownership problem and its solutions
By "Land and Real estate double ownership", we mean the impossibility of sharing the same geographic coordinates at the same time. Unfortunately, the existing centralized registries aren't equipped with built-in independent automated solutions to block the creation of new records. In cases where there already is a record, it conflicts with a created one. For instance, when you try to create a new record regarding the boundaries of a land plot in the state registry, such a record can be created. Since the decision to create a record is settled by a specific authorized person – not a code, there will be two conflicting entries in the registry. Resolving this conflict will require the use of the state judicial system.

#### The algorithm for solving the problem
Each land plot, building, or room has a polygonal representation. The vertices of a polygon have coordinates in the [WGS84 standart](https://en.wikipedia.org/wiki/World_Geodetic_System#A_new_World_Geodetic_System:_WGS_84) — latitude, longitude, and altitude. Thereby, the task is reduced to mathematical verification of the new polygon intersecting with the already existing ones in the three-dimensional space. For consistency purposes, the calculation of intersections in the three-dimensional space is too complicated and can be reduced to checking intersections in a rectangular coordinate system in the Mercator projection considering altitude.
![Polygon intersection](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard16.png)

The task of checking the intersection of polygons for land plots and buildings comes down to checking the intersection on a plane in the Mercator projection excluding the altitude. 
The task of checking the intersection of the polygons of Rooms is reduced to checking the intersection on the plane in the Mercator projection, taking into account the minimum and maximum heights of the room.

![Polygon intersection](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard14.png)

To determine the fact of the intersection of polygons and intersection points, we use the following algorithms:
- Weiler–Atherton clipping algorithm; 
- Martinez-Rueda clipping algorithm.

#### Option 1: Off-chain and on-chain hybrid sollution with Oracles when creating tokens
Checking the intersection of two polygons is feasible on the Ethereum blockchain and doesn't require substantial gas costs. At the same time, checking the intersection of one polygon with an unlimited number of polygons is impossible due to limitations in the number of calculations per block. Based on this, the intersection of the new polygon with all those written earlier must is a subject to an off-chain check. Anyone can put a deposit in the GALT tokens into a smart contract to become "Polygon intersection verification Oracle" and run the script. The script checks applications with new polygons one by one. The applicant pays for the Oracles in ETH. Verification of each application requires several independent Oracles. If all Oracles confirm that there is no intersection, then they withdraw the reward. If a part of the Oracles confirms there is no intersection and at least one Oracle provides the ID of the token, with which there is an intersection, the smart contract automatically rejects the application, pays all the reward to the honest Oracles and removes the deposit from dishonest ones in favor of the honest.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard10.png" alt="Off-chain double ownership check when creating Token for Land plot, Building or Room"/></p>
The smart contract employs three methods to uniquely verify the intersection of polygons:

- "ray casting algorithm" to determine the occurrence of one of the vertices of the polygon in another polygon;
- the intersection of two lines in the plane to determine the fact of the intersection of the edges of the polygons;
- the occurrence of a point along the height coordinate in the interval.

#### Option 2: Off-chain and on-chain hybrid sollution with Deposits after creating tokens
To guarantee 100% impossibility of double ownership, the following mechanics can be used as an alternative or addition to the one described above. When creating a token of land plot or real estate, the Owner of the token must make a deposit in GALT ERC20 tokens. The deposit is stored in a contract that has the rights to create and destroy tokens. A deposit can be withdrawn by the Owner only if the land or real estate token is voluntarily destroyed. 
Anyone can provide the ID of two tokens that intersect to this contract. The contract verifies on-chain that the intersection exists. If it really is, token with last creation timestamp / block number is destroyed, and the one who provided information to the contract receives deposit. If the creation of the token was approved by the Oracles (Cadastral engineer and Notary), then they also lose their deposits.
![Polygon intersection](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard26.png)

#### Option 3: Sidechain sollution
The problem of checking the intersection of one polygon with an unlimited number of polygons is completely on-chain solvable. In this case, the initial creation of tokens of land plots and real estate objects occurs on the sidechain, in which a large volume of calculations can be made. Such a sidechain could be the blockchain on Parity Substrate or Cosmos SDK or any other. During the initial creation of the Token, the Validator nodes check for intersections and confirm the creation of the Token.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard11.png" alt="Sidechain double ownership check when creating Token for Land plot, Building or Room"/></p>

Unfortunately, checking intersections of a large number of polygons will still lead to a large load on the validator nodes and delays in creating blocks.

#### Conclusion
The simplest and most reliable verification method, which will be used primarily - Option 2: Off-chain and on-chain hybrid sollution with Deposits after creating tokens.
 
## Types of property ownership - "with State" / "with out State"
In the modern world, there is land (and real estate objects) divided between owners according to state registers. Recording in these registers and protecting the rights of owners is the responsibility of a state located in a particular territory. There are also territories not controlled by states. Correspondingly, they lack their registries and formal guarantors of the rights. Examples of such territories are Bir Tawil and Antarctica. The proposed system of smart contracts allows one to register ownership of land and real estate, in all types of territories.

## Types of registries and methods of initial creation of tokens
In previous sections, a description of Property token was given, as well as mechanisms to ensure its uniqueness. But the most important question is how the initial creation of the token occurs and how the Owners of the tokens reach a general consensus that the tokens are created correctly and really reflect ownership. Unfortunately, there is no single answer to this question.
We offer several theoretical methods, each of which has its advantages and disadvantages. 

But given the complexity of the question, a definite answer can only be obtained on a large number of real users. We assume that several competing registries that implement different methods of creating tokens and changing their data may exist simultaneously. In the end, one of the most reliable will be chosen by people. The rest will cease to be used as unnecessary.

### Ownable Property Registries (or Private Property Registries / Ownable Private property registries / OPPR)
Property tokens are initially created by single entity. Any individual, company or DAO can create property registry, verify geographic coordinates and ownership rights of land plot, house or room/apartment, create property tokens and distribute them. If necessary, ownership of the registry can be transferred to DAO of property token owners (or any other DAO). In this case property token owners create new tokens, approve data change or burn tokens by voting. There is an economic incentive to create new tokens and update data on them. Some states are currently transferring land and real estate accounting functions to private companies. In this way, private company can create its own registry for this purpose. Also Trust fund or any other legal entity can create its own registry in which it will be a guarantor of rights. A community of property owners living in the same territory can also create their own registry without any legal entities.

### Prof of Location Token Curated Property Registries (PoLTCPR) 
Anyone can put deposit in Registry's ERC20 tokens and create token for land plot, house or apartment / room without any verification or permission. Anyone can challenge token creation multiple times during challenging period (no more than one time per month, first 5 years) by submitting an equal amount of Registry's ERC20 tokens. This initiates a voting period among ERC20 token holders. If challenge is succeed, then Property token is burned and its deposit is distributed between Challenger and winning voters. On opposite if challenge failed, then Challenger deposit is distributed between Property token owner and winning voters. The verification itself can be quite simple, as the confirmation will be the location of the Owner within the geographical coordinates of the token.

We assume that there can be an unlimited number of such registries, each of which will use its own ERC20 token. For example, at the same time, there may exist a registry curated by the owners of the GALT token or any other ERC20 tokens.
<!--- 

### Dynamic Prof of Location Property Registry (DPoLPR) 

--->
### Oracles Property Registry (OPR)
Property tokens are initially created by decentralized community of Cadastral engineers and Notaries. Anyone can pay fee and create proposal to create token for his land plot, house or apartment. Also anyone can put deposit in GALT ERC20 tokens, become Oracle and approve property tokens creation for fee. Property token owners, oracles and Galt token holders elect Arbitrators. Anyone can create a claim on property token or Oracle. Arbitrators make decision on claims, slash deposits from oracles and change data or destroy property tokens.

### The impossibility of double ownership in different registries
All described registries can be used for property transactions, collective investment in real estate, self-governance and other purposes.

In order to ensure the overall consistency of described registries, they must voluntarily use the same "Double ownership verification" Сontract. When connecting this contract to the registry, Property Token Owners make a deposit in GALT ERC20 tokens. They must do this within a month. If, after the set deadline, the deposit is not placed, then the Property tokens can be automatically destroyed by contract. After placing a deposit, tokens can be tested for dual ownership, as described above in the section "Option 2: Off-chain and on-chain hybrid sollution with Deposits after creating tokens".

A situation may arise when a registry is created with tokens that occupy the real space, but are not created by the real owners. In this case, the new tokens in other registry will not be able to pass the double ownership test. 
GALT ERC20 token Holders may forcibly disconnect bad registry from contract by voting. In this case, deposits can be withdrawn by the owners. This is a squatting defense mechanism. 

Thus, we define the following types of registries:
- single consistent Oracles decentralized property registry;
- unlimited number of Ownable private property registries, governed by single entity or DAO;
- unlimited number of Prof of Location Token Curated Property Registries;
- single consistent Dynamic Prof of Location Property Registry.

## Communities of Property Owners
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard25.png" alt="Communities of Property Owners"/></p>
In both types of the territories and all types of Registries, the Property owners(or tenants) can unite in communities for self-governance. The main goal of such a community is to unite owners in a specific territory, enact laws, and raise funds in ETH, DAI or any ERC20 to achieve common goals (physical protection of property, management of common property, construction of common infrastructure, etc.). In fact, the Community is a decentralized autonomous organization (DAO) of Property owners and may be an alternative to the municipal government. Such a system is devoid of the shortcomings of the existing public administration system since it can't be taken over by corrupt officials. 

Communities of Property Owners can be as small as an apartment house, or several neighboring houses, or as big as a whole city or region. Imagine a city where all residents (tenants and homeowners) can use their smartphone to raise funds to the budget in ETH or any ERC20, vote on important issues and choose city managers. All operations are performed on smart contracts and therefore cannot be blocked, restricted, or tampered.

### The need to use Property token as a basis for community membership and voting
We suggest using a land plot or real estate token as a basis for the Community of Homeowners for the following reasons:
- each token is unique, two tokens in the general case cannot occupy the same geographical coordinates. The creation of non-existent tokens is easily revealed by the community and fake votes is almost impossible;
- each token is located in a specific geographic area. Token holders living in this place (property owners or tenants) are more than anyone else have the right and interest in the proper management of this area according to the right of residence. An individual who does not live in this area should not have the right to make decisions that determine the life of society;
- everyone knows their neighbors and where they live, which means that the process of verification of community members by members themselves is simple and reliable. Sybil attack on such a community is almost impossible.

### General community architecture
Each community is a set of smart contracts created with a Factory. The Property owners create their personal Locker smart contract and transfer the token of the land plot or real estate to it. With this contract, they can create Reputation in proportion to the number of square meters of property. The opportunity to join the community is determined by voting of existing members. Owners use their Reputation to create Proposals and vote on them in Voting smart contract.

Voting smart contract can:
- approve new community members;
- change community parameters;
- enable and disable community Laws;
- choose professional managers, who manage the community budget;
- apply fines and exclude members from the community;
- set tariffs for regular and one-time fundraising in the community budget.

<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard20.png" alt="General community architecture" width="700"/></p>

### Community Reputation
Every member of a Community has Reputation. This is the number that determines the weight of the vote of each participant in the voting for decisions. Alice can have Reputation 45, Bob 52. In other words, Bob has more influence in Community, then Alice. A community member gets a reputation for:
- the number of square meters of his or her property(own or rented);
- by voting of other members for Community service;
- through a financial contribution to the community budget;
- for voting on important topics.

<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard4.png" alt="Reputation"/></p>

### Liquid democracy
If a Community member doesn't participate in the voting, they can pass their vote to another trusted member of the Community. In turn, the latter can give his or her votes to another trusted member of the Community. As a result, the votes of the passive "majority" will be transferred to the expert and the active "minority." Each Community member can get the vote back instantly whenever he or she wants. This way we solve the “apathy of voting” and “usurpation of power” problems.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard3.png" alt="Liquid democracy" width=700/></p>

### Community Laws
Community members can pass and repeal laws by Voting. Each law is a record in a smart contract that contains the name of the law and the IPFS hash of a detailed document. Adopted laws are binding on all community members. Violating them may result in a community member being fined or expelled. The decision to impose a fine or exclusion is made by voting in Voting smart contract.

### Community Budget
Community Budget is stored on a Multisig wallet in the ETH and ERC20 tokens. It's replenished by community members through several Tariff smart contracts, which determine how and with what regularity community members should send ETH or ERC20 to Budget. 
There are several types of Tariffs:
- regular – community members regularly send funds in ETH or ERC20, for example, to pay for garbage collection or for the police services;
- one-time – community members send their funds once in ETH or ERC20 to achieve a common goal, such as building a road;
- mandatory – community members are required to send funds. If a member of the community doesn't fulfill his or her obligations to the community, he or she will receive a fine and can be excluded;
- voluntary - community members can voluntarily replenish the budget and receive rewards in the form of additional Reputation. For example, part of the community may pay for the construction of a new playground and get Reputation.

The spending of funds is controlled by professional managers (Multisig managers), which are selected by voting. Each manager must have a deposit in ETH or ERC20, as a guarantee. The total amount of funds that can be paid from the budget for a period of time (week, month, or year) is equal to the total deposit of managers. Thus, in case of suspicion of corruption, Managers can be quickly re-elected, and deposits will remain in the community and cover all losses. Managers are rewarded from Community budget.

### Many Multisig wallets in one Community
A community for different purposes can create several Multisig wallets and through direct elections set their Multisig managers. For example, one Multisig wallet can be created for road construction, and another for energy network maintenance.

### GeeSome - An unstoppable social network protocol on top of IPFS
We've created the GeeSome protocol for Communities to freely communicate in encrypted chat groups, share images, video, text, or any data without risk of censorship or blocking.

### Compatibility with different frameworks for DAO
To create communities of homeowners, Property owners can use not only the Galt Project Community Framework, but also other frameworks for DAO’s such as DAOStack or Aragon.

## Ownable property registries (or Private property registries)

### Creating Private property registry
Private property registry is ERC721 Ownable Smart contract on Ethereum. Anyone can create a private registry using the smart contract Factory by paying a fee in ETH or GALT and become its owner. The private registry Owner has the ability to create tokens with geographic coordinates and other linked data(address, floor, apartment or room number, photo and video, etc.) without any restriction and double ownership check. Tokens can be created for commercial purposes, as digital objects representing the right of ownership, lease rights, leasing agreements, shares in co-op, membership rights, etc. As well as for the self-government of property owners. In this case, the token gives the right to make a decision and vote in the created Community of Homeowners. 
The purpose and legal meaning of the token is fully determined by agreement with the Owner of the Private registry, as an individual or legal entity.

### Private property registry Owner
The Owner of a private registry is an address in the Ethereum blockchain, which can create tokens, change the parameters of registry contracts, change and destroy tokens with the approve of token holders, and also perform other operations. The owner may be an individual, legal entity, or DAO (for example Aragon organisation). In the last case, such a registry is decentralized since all operations are carried out by voting of DAO participants.

### Creating property records
In the case of using a private registry, operations to create token for land plot, house, apartment or office is carried out by the Owner of the registry or by those who have been given the corresponding rights by the Owner. Once created, the token can be transferred.

### Updating property records
In this case, the geographical and other data of the token are changed by the approval of the changes by the Token Holder and the Owner of the private registry. In the same way, if necessary, the token can be destroyed(burned).

### Private property registries general architecture
Anyone can choose a Private registry Factory contract from Approved Factories registry contract (a whitelist of contracts managed by a decentralized community), pay a commission, and create his own private registry. After creating the Private registry, its Owner can create tokens and transfer them to the Token owners. After the token has been transferred to the owner, a change in its geographical coordinates and data, as well as the destruction of the token, can only occur through the Token modification contract(Controller). For this, the Owner of the token or the Owner of the contract should create a proposal for changing the data. Proposal must be approved by the other party. After that, the Controller changes the data. In case of loss of the private key of the Token Owner, a "burn after timeout" procedure is provided. The token Owner can set the time after which the token can be destroyed by the private registry Owner. The registry owner in this case initiates the destruction of the token. After the time has expired(and the token Owner didn't cancel the destruction), the token is destroyed and the registry owner can issue a new token with same geographicall coordinates and data.
![Private registries general architecture](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard22.png)

### Economic incentives for Private property registry Owners
The simplest scenario for creating a private registry is as follows. 

An opinion leader in a certain territory decides to create his own private register for registering property rights and self-government. He creates a private registry, issues property tokens and distributes them to his neighbours. Together they create Community of Homeowners. After some time, he transfers the rights to manage the Private registry to Property token Owners. Such work requires a lot of effort and should be accompanied by economic benefits.

To do this, we have included the ability to set additional built-in fees. The Token Owner, when performing various operations with the token (changing token data, blocking the token for joining the community, placing an order to sell the token, executing a sale transaction, and others) pays a small commission to the Registry Owner. After decentralisation, the Token Owners themselves decide on the size of these commissions.
![conomic incentives for Private registry Owners](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard27.png)

### Decentralized governance for Private property registries
At some point, the rights to manage Private property registry contracts(create tokens, destroy tokens, change tokens data, set additional commissions, etc. ) should be decentralized. The most correct solution for this is to transfer those rights to the Property tokens Owners.

Property tokens Owners cache token area on particular block in smart contract. This value is used to vote on Proposals in Proposal Manager contract. For example, the owner of a token can create a proposal to issue a new token. After that, the remaining token holders vote. If the offer is accepted, then Controller contract creates a new token. Absolutely in the same way all other operations are performed.
 ![conomic incentives for Private registry Owners](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard28.png)

### Private registries System Governance
We want smart contracts and related software to be reliable and not require complex technical skills from ordinary users. To do this, we use the mechanism of Factories, when a user, paying a commission, creates a private registry, community (or other smart contracts) using an allredy existing, reliable contract on mainnet. Software development is a complex process in which probable errors and critical vulnerabilities. Thus, someone with technical skills and financial motivation should monitor the reliability of existing Factory contracts (or simple contracts), upgrade them and create new contracts and Factories that users need. And this should not be one person or a small group of people, but a decentralized community, where there will be no single point of failure. 

We lay it on the GALT ERC20 Token Holders. They stake tokens and can create proposals and vote for existing smart contracts upgrades, setting smart contracts commissions, setting commision distribution, approving new smart contracts and others. For this, they receive a percentage of the total commission of smart contracts in proportion to their stake. And they are interested in the long-term reliability of smart contracts, since their source of income is the commission from users.
![Private registries Governance](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard32.jpg)

### Private registries system Commission
Most of the smart contracts in Private registries have a commission in Ether and/or GALT ERC20 for tokens trading, creating smart contracts with Factories (Private registries, communities of homeowners, property token lockers, etc.), and so on. Commission amounts for different operations, and its distribution is set by voting. Commission from all contracts goes to Commission mixer Contract, which distributes it between GALT Auto buyback Contract and Staking Reward Contract in proportion set by the Governance voting contract. Staking Reward Contract distributes ETH and GALT to the GALT holders proportionally to their stakes. The GALT Auto buyback Contract uses the ETHs received to automatically purchase GALT from the GALT Automated Market Maker Contract, thereby increasing their price. The GALT tokens purchased and received from the commission are locked forever in the GALT Auto buyback Contract.
![Private registries Commission](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard23.jpg)

### Communities of Property owners in Private property registries
Creating Communities of homeowners in this case is no different from creating them in a Single consistent decentralized registry. Anyone can create a community and add members to it by voting of existing members. One community may contain tokens from different private registries. And at the same time, the owner of one token can be simultaneously in several communities(community of residents of one house, street, district or the whole city, etc.). More details are in "Communities of Property Owners" section. 
Since the community is a set of smart contracts, it itself can be the Owner of a private registry contract thus ensuring its decentralization.

## Oracles property registry (OPR)

### Creating property records

In Oracles property registry, any land and real-estate property owners can create their property tokens with the help of the decentralized community of cadastral engineers and notaries. Each Token represents property rights record for land or real estate. Anyone can pay a commission in ETH or GALT ERC20 and apply for creating a token through a smart contract. The application contains the geographical coordinates of the object, topology, IPFS media hashes (photos, video, point cloud file, Building Information Model, etc.), additional identification data (address, area, floor, room ID, etc.). The application is taken into work by the Cadastral Engineer and the Notary. They verify the correctness of the data and the applicant's property rights in a particular jurisdiction for a fee. With the application approved, a new object is checked for dual ownership. After that, a token is created.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard12.png" alt="A decentralized community of Cadastral engineers and Notaries"/></p>
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

### Oracles
If someone wants to create a token of a land plot, building or room, there should be a decentralized self-governed mechanism for checking property rights and geographic coordinates. In Oracles property registry, this function is fulfilled by the Oracles. They're independent economic agents, who approve new token creation for a reward. Moreover, they perform a wide range of different operations: valuation, custodian service, etc. The Oracles have a deposit, which can be written off. To be able to earn the reward, they buy and deposit protocol utility token - ERC20 GALT Token. This deposit can be written off by the governance mechanism described below.

### Disputes resolution
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

### Arbitrators 
The GALT token holders use their stake to elect the Arbitrators, which is a special governance role. Each Arbitrator has a deposit in the GALT token. Anyone can create a claim about the Oracles, Arbitrators or Property owners dishonest behavior or mistake and pay the fee in ETH in the smart contract. Several Arbitrators take this claim for consideration. Each of them can create a proposal on what is to be done:

- what the size of the deposit is;
- from whom it should be written off;
- how the coordinates are meant to be changed;
- to apply a penalty or not on the Buyer or Seller according to the escrow smart contract terms;
- etc.

After that, they vote on each proposal. If the claim is approved, the deposit will be written off, the geographical coordinates will be changed, or the escrow contract will be canceled, etc. That said, the Arbitrators will also get their reward. If the decision isn't made on time, the Arbitrators will receive no reward, lose their deposits, and the claim can be taken up by another set of the Arbitrators. If the applicant is dissatisfied with the decision of the Arbitrators, he or she can create a new claim or ask the community to re-elect the Arbitrators.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard31.png" alt="Arbitrators"/></p>

### Arbitrators Governance groups
In general, there are some technological restrictions in the current Ethereum that limit a possible maximum number of the Arbitrators. Also, there is a limit on the number of claims that can be considered by the Arbitrators during a specific period of time. So, to make this system scalable and facilitate operation with a large number of users, we should divide Arbitrators and Oracles into separate groups. The most obvious solution is to combine according to the geographical principle. There can be an unlimited number of such groups. In each group, the GALT holders vote to elect the Arbitrators. The Arbitrators deposit GALT as a deposit and provide their service in this group.
![Governance groups](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard17.png)
In addition to voting for the Arbitrators, by voting, the members of the group determine such parameters as:

- the size of the Oracles and Arbitrators deposits;
- the minimum amount of payment for the Oracle by role;
- the total number of Arbitrators in the group;
- the number of Arbitrators who consider the claim;
- the required number for making a decision
- etc.

### Arbitrators elections
To make the governance system more reliable, the Arbitrators should be easily elected and re-elected, they should have economic incentive to honestly resolve disputes and they should represent all the participants of the Protocol. GALT token holders use their stake to vote to add or remove Arbitrators in partucular group. 
![Arbitrators elections](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard29.png)
 
### Creating property records on the territories without existing states in Oracles property registry (OPR)
There are the territories that are out of a state's sovereignty and the territories the rights to which were renounced by the state. They're called "Terra nullius" or "nobody's land". Examples of such territories are Bir Tawil in Africa and Marie Byrd Land in Antarctica, to name a few. Due to their isolated geographical position, associated risks, and harsh climate conditions, the settlement of such territories implies substantial financial expenses and a high likelihood of losing investments. Neither states themselves, nor private enterprises and investors are ready to do this. However, with sufficient financial resources, it's possible to create anything one could imagine in these territories: cities, industries, commercial centers, tax-free areas, etc.

An effective solution to the settlement problem may be crowdfunding with a large number of backers supporting the project through smart contracts. A particular territory can be divided into land plots. Potential buyers would participate in auctions that sell those land plots. All the funds collected from selling them would be passed to the community fund that is used for developing the infrastructure and serves as a guarantee of physical protection and legal recognition (if needed). Several billion dollars collected in cryptocurrency by a strong community of like-minded people would make it possible to build an airport, energy and transportation infrastructure, hire a private military company, and get other states' support.

This approach can be used both on Earth and beyond it. For example, on Moon on Mars. In the near future, the cost of a flight to Mars may amount 100,000 dollars at most. Just as in the Age of Discovery, hundreds and thousands of explorers will rush to those new worlds trying to find a better life and opportunities. With smart contracts, such a settler community will be able to unite, gather necessary funds, and build the society devoid of the imperfections of the existing state systems.

#### Creating an updating property records for land
In this case, the auction mechanics are used for creating land-plot tokens. Anyone can pay a fee in ETH or GALT and create a Proposal to start an auction for land plots located on an unclaimed or disputed territory. The creator of the proposal creates Community of Homeowners in advance, to which all funds from the auction will be transferred, as well as the smart auction contract itself. The auction type is defined by the code of a smart contract (English auction ,Dutch auction, Sealed first-price auction, Vickrey auction and others). The proposal contains the geographical coordinates of the land and auction parameters, such as Min. number of Land Plots to sell to create tokens, Auction duration, Min. goal for crowdfunding, Address of Community of Homeowners contract, Auction currency ETH/ERC20 and others.

GALT token holders use their stake to vote on the Proposal through Governance Voting Contract. If it is accepted, then the auction begins. Anyone can bet on the land plot. If the bet is won, as well as the minimum required number of plots is sold or the goal of raising funds is achieved, new tokens of land plots are created. The tokens are transferred to new owners, and all received funds are sent to Community Multisig. Unsold land plots may be sold later.

The participants in the new community choose managers who will manage the funds – to pay for the construction of infrastructure, physical protection of property, etc. They also vote for the adoption of laws and the collection of additional funds(a detailed description of the Communities is provided in the corresponding section).
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard21.png" alt="Creating property records, property protection and use cases on the territories without existing states"/></p>
Unlike land plots in the territories of existing states, these land plots are unchanged. Their geographical coordinates (latitude and longitude) can't be changed. The altitude coordinates can be changed by Cadastral engineers.

#### Creating and updating property records for Real estate
Unlike land plots that are unchanged, buildings are created and destroyed. Thus, the creation of such tokens requires Cadastral engineers and Notaries. It happens the same way as in the territory of existing states. Anyone can pay a commission in ETH or GALT ERC20 and apply for creating or updating a token through a smart contract (as described in the "Creating property records, disputes resolution and use cases on the territories of existing States" section).

#### Commercial operations with property
Since the guarantor of the property rights are the owners themselves, in this case, commercial operations don't require the Custodians participation. Ownership is transferred only through a smart contract. Such transactions should be accepted by all property owners in these territories.

#### Property protection
In the territories not related to existing states, owners must provide protection of property themselves. For this purpose, they must create Homeowners Community (a detailed description of the communities is provided in the corresponding section). The owners create a regular tariff in the community and replenish the multisig with ETH, DAI, or any ERC20. These funds are used to pay for the services of the private police or army that provides physical protection for land and real estate.

### Oracles property registry (OPR) Governance
The described system of smart contracts has a large number of parameters that require changes (depending on the current situation) as well as updating the code. These actions should be as decentralized as possible and at the same time carried out in the interests of the majority of participants.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard5.png" alt="Decentralized governance"/></p>
There are two levels of Governance:

- Arbitrators Governance groups;
- Global governance;

On the "Arbitrators Governance groups" level, the GALT holders use their stake to elect the Arbitrators and determine the Group parameters such as:

- the Oracles and Arbitrators Deposit amounts;
- the Oracles and Arbitrators minimum fee;
- voting thresholds;
- the total number of the Arbitrators in the group;
- the number of the Arbitrators who consider the claim;
- the required number for making a decision;
- and others.

Also they upgrade group contracts. 

On the "Global governance" level, the GALT holders use their stake to determine global parameters such as:

- size of the general protocol commission and commision for particular smart contracts;
- upgrade contracts; 
- start Auctions for unclaimed territories (This is described in the "Creating property records, property protection and use cases on the territories without existing states" section);
- others.

#### Reputation in Oracles property registry (OPR)
The Property owners, GALT holders, and Oracles have Reputation, through which they manage the protocol. They elect the Arbitrators, determine protocol parameters, and upgrade smart contracts. The Property owners and GALT holders create a personal locker smart contract. They can transfer a Property token or GALT tokens to this contract and create Reputation in the Global Reputation contracts proportionally to the area of their property or the balance of the GALT tokens. From the global Reputation contracts, they create an additional Reputation in the Arbitrators Governance Group. The Oracles place a deposit in the GALT tokens in the Governance group and receive Reputation in exchange. All of the described roles stake Reputation on the Arbitrators and receive the reward from the general commission of the protocol.
![Reputation](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard18.png)
The Property owners and GALT holders create voting proposals in Global Governance and vote for them. The Oracles have Reputation only in the Governance groups, so they vote using it. 
For voting in a particular Governance Group, all the participants use their Reputation in this group.

#### Staking rewards in Oracles property registry (OPR)
Protocol participants are rewarded for choosing the Arbitrators. The reward is proportional to how much GALT staked on the Arbitrators in a particular group. The Reward is given to:

- the GALT token holders for locking GALT and staking Reputation on the Arbitrators;
- the Property owners for locking a land plot or real estate token and staking Reputation on the Arbitrators;
- the Oracles for depositing GALT and staking Reputation on the Arbitrators.

We provide the opportunity to receive rewards not only to the GALT holders to encourage people to become the Oracles and register their property (a land and real estate). For example, the Property owners participating in the election of the Arbitrators will receive a part of the commission from all future registrations of new land plots and real estate and other contracts.

#### Commission distribution in Oracles property registry (OPR)
Most of the smart contracts have a commission in Ether and GALT for land and real estate tokens registration, tokens trading, Creating smart contracts with Factories (communities of homeowners, personal lockers, etc.), and so on. Commission amounts for different operations, and its distribution is set by voting. Commission from all contracts goes to Commission distribution Contract, which distributes it between GALT Auto buyback Contract and Reputation Staking Reward Contract in proportion set by the Global governance. Reputation Staking Reward Contract distribute ETH and GALT to the GALT holders, Property owners, and Oracles proportionally to their Reputation stakes. The GALT Auto buyback Contract uses the ETHs received to automatically purchase GALT from the GALT Automated Market Maker Contract, thereby increasing their price. The GALT tokens purchased and received from the commission are locked forever in the GALT Auto buyback Contract.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard19.png" alt="Commission distribution" width="700"/></p>

## Use cases
With a consistent registry of property rights, various operations can be performed, like trading, collective investments, insurance, mortgages, and others. The guarantor of rights in such transactions can be the State itself (if a particular state accepts such transactions), international nominal owners – the Custodian (and the State they interact with) or the Property owners’ themselves.

### Custodians
In some jurisdictions, to make operations like land and real estate trading, mortgage and others on Ethereum, Property owners need a decentralized third-party - the Custodians. The Custodians are legal entities in reliable jurisdictions. They're temporary owners of land or real estate and are legally obliged to re-register these rights in the state registry to the token owner. Also, they can convert their income from real estate to Ether or Stablecoins and transfer it to token owners. To provide paid services, they need a deposit blocked in the smart contract. In case of an error or fraud, the deposit will be written off and used for prosecution and damages cover. The Custodians get a reward from token holders for interaction with government agencies and other Oracles. They act as a supranational property guarantor. For reducing the risks of fraud, each property can be divided between 2-3 Custodians. If dishonest behavior is detected, their deposits will be fully withdrawn and used to retrieve property to their real owners.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard13.png" alt="custodians"/></p>
Each Custodian has a unique address. This way, the very Custodian can be a DAO – decentralized autonomous organization. In some cases, the Custodians are not necessary, if a state accepts blockchain transactions or there is no state at all, and the community of property owners itself acts as the guarantor of their rights.

### Property trading with Custodians
It's essential to be able to perform fast international trading transactions with land and real estate tokens. The easiest way here is to use the Custodians' service. If the Sellers want to sell their token, they need to create a market order in a smart contract. The Buyers can make their offers. When buy and sell price are equal, the Seller can transfer the token to the escrow smart contract, and the Buyer can transfer ETH or other ERC20 tokens, including Stable Coins. Both parties can withdraw their tokens only if they confirm the deal and if the land and real-estate token has one or more Custodians. If there are no Custodian for the token, the Seller should register them, sign all necessary legal agreements and transfer the land or real estate to the Custodian. After that, both parties can confirm the deal and withdraw tokens. If at any stage of the deal the Buyer or Seller wants to cancel it, it's possible to make a cancellation request. Cancellation requests are reviewed by Arbitrators. They can apply a penalty on the Buyer or Seller according to the smart contract terms. 

In the future, if the custodian has already been appointed, the transaction can occur instantly and without the involvement of third parties.

### Property trading with State registration
In this case, Galt Protocol should be integrated with the Government property registry. After both Seller and Buyers tokens are transferred to the escrow contract, the State representative (a notary, judge, or state registrator) registers the deal in the government registry. After property rights were transferred from the Buyer to the Seller, he or she confirms the deal in the smart contract.

### Collective investment in real estate
Today, investment in Land and Real Estate can only be made through an inefficient process involving a lot of useless intermediaries and lots of paperwork. For many people, it's too complicated and expensive. One of the reasons is that most REITs (Real Estate Investment Trusts) have restrictions on the minimum amount of investment, which makes it unaffordable for most people. The second main reason is that they don't accept cryptocurrencies as payment, which makes a quick cross-border purchase impossible. As a result, a large number of retail investors don't have access to Real Estate investments, which are the safest way to build long term savings.

Any Land or Real estate token can be blocked in the smart contract, as collateral. At the same time, a fixed number of the ERC20 tokens is issued and can be sold to investors. Each token represents a share in a specific property. The Custodian manages the property and converts property rental income (if rental income comes in fiat currencies) minus his commission into ETH or Stable Coins. The ERC20 token holders can withdraw this income from the smart contract with their ERC20 token balance. Also, if they are no longer satisfied with the Custodian, they will be able to change it to another by voting. As a result, anyone, from a New York student to Jakarta fruit seller can invest 20 dollars a month in a real estate object using their smartphones and get income.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Artboard6.png" alt="Collective investment in real estate"/></p>

### Property protection from Custodian malicious behavior
One of the main risks is dishonest actions of the Custodians, who, in the eyes of the state, are the owners of real estate. The Custodian may violate the legal agreement and sell the property or restrict access to it from the token owner. In this case, the token owner will be forced to go to the court to cancel the transaction and terminate the agreement with the Custodian. Such a legal procedure is costly and time-consuming. The solution to this problem is insurance of the risk of the Custodians' dishonest behavior. The real-estate token holders unite into small groups (300 - 500 owners) and regularly send ETH or Stable Coin, like DAI, to an insurance smart contract. If one of the token holders has a problem with a dishonest Custodian, they may receive a payment from the smart contract equivalent to the value of their property. The token itself is transferred to a smart contract and becomes the common property of other participants of the insurance fund. To return their property, the participants may allocate funds from the fund by voting. After the property is returned, the token can be sold by the fund to its original owner or put up for sale on the market.

### Other use cases
The consistent global registry also makes it possible to perform the following range of operations:
- short or long term rental;
- mortgage. It can be issued in Stablecoins. The calculation of payments and the procedure for transferring a real estate token in case of violation of the payment schedule is determined by a smart contract;
- real-estate insurance;
- collective investment and construction management. For the construction of the property, a DAO can be created. The DAO Token Holders vote for contractor selection and construction financing. After the construction is completed, they receive shared ownership of the property;
- use ERC20 tokens as shares in co-op. Token holders can vote and decide on a board.

## ERC20 GALT Token
GALT token is the ERC20 standard Ethereum utility token with a fixed supply of 42 mln. All 100% of GALT is distributed by means of the Automated Market Maker contract with Bonding curve. The project team receives GALT tokens by buying them from a contract.

### Token purpose
By issuing a token, we pursue four main goals:
- to create a single base for double ownership verification;
- to create a single base for accounting the Oracles' deposits;
- to create a strong community of the Property owners, Oracles, Custodians, and sofware developers by incentive systems that enable coordination of network participants to achieve shared goals. Tokens incentivize them in an economic game towards an outcome that are mutually beneficial;
- create an incentive for the Arbitrators elections. The Galt holders can stake tokens to elect the Arbitrators and get the reward from protocol commission;
- create an incentive for Smart contracts governance;
- create an incentive to spread information about the project. The GALT token holders will distribute information about the project, as each subsequent buyer of tokens increases their value.

### Token distribution
The GALT token is distributed by means of the Automated Market Maker contract with a Bonding curve. A bonding curve is a mathematical curve that defines a relationship between price and token supply or in our case the number of sold tokens. When a person purchases the token, each subsequent buyer has to pay a slightly higher price for each token, generating a potential profit for the earliest buyer. As more people find out about the project and buying continues, the value of each token gradually increases along the bonding curve. Early buyers who find Galt Project promising earlier, buy the curve-bonded GALT token, and then they can sell their token back and earn a profit in the future.

The Automated Market Maker contract (forked from Bancor) holds a balance of ETH and all fixed supply of the GALT Tokens. To buy GALT, the buyer sends some amount of ETH to a bonding curve contract’s Buy function which calculates the price of the token in a ETH and send the correct amount of GALT to the buyer. The Sell function works in reverse: The contract will calculate the GALT’s current selling price and will send the correct amount of ETH to seller. All GALT tokens are backed by ETH on 100% at any moment and forever.

Automated Market Maker contract has a CW=20% in Bancor Formula.

#### GALT token Price by GALT sold
This chart describes how the price of the token changes depending on how many tokens are purchased from the contract. With each purchase, the price increases along the curve, and with the sale decreases.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Price-by-TotalSupply.png" alt="GALT Price by TotalSupply" width="700"/></p>

#### GALT token Price by ETH balance
This chart describes how the price of the token changes depending on the ETH balance on the contract. The buyer sends ETH to the contract and receives GALT back, while the contract balance in ETH increases, and in GALT decreases. The seller, on the contrary, sends GALT and receives ETH back. The GALT balance increases, and the ETH balance decreases.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Price-by-ETH-on-contract.png" alt="GALT Price by ETH on contract" width="700"/></p>

#### Galt sold by ETH received
This chart describes how the amount of GALT sold by the contract depends on its ETH balance. To buy all total supply (42 million GALT), it will take 10 million ETH.
<p align="center"> <img src="https://raw.githubusercontent.com/galtproject/galtproject-docs/master/whitepaper/images/Galt-sold-by-ETH-received.png" alt="GALT sold by ETH received" width="700"/></p>

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
- [FOAM
Whitepaper](https://foam.space/publicAssets/FOAM_Whitepaper.pdf)

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
