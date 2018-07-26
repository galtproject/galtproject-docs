# General scenario of the Project development

Special terms in the text begin with a capital letter or like `this`. To understand the terms - [Glossary](https://github.com/andromedaspace/galtproject-docs/blob/master/eng/Glossary.md).

The basis of the `Project` is the Token standard ERC20 GALT and Token standard ERC721 SPACE. The GALT Token is the right to share or dispose of land and the equivalent of a share in an investment Fund that is engaged in the development of the `Territory`, the SPACE token - the right to a specific Land with specific boundaries. These rights are determined by the smart contracts of the `Project`. See more details - GaltToken contract, SpaceToken contract.

The procedure for the GALT Project CORE Team to launch the Project:

1. GALT Project CORE Team runs on its own behalf the contract GaltToken and SpaceToken. SpaceToken contracts create SPACE tokens of `Territories` and SPACE tokens of The `Land plots` that will be passed on to the leaders of the cryptographic Community's opinion. See more details - GaltToken contract, SpaceToken contract.

2. GALT Project CORE Team launches the SplitMerge contract. See the SplitMerge contract for details.

3. GALT Project CORE Team launches `AddNewPlot` contract. Now everyone can register their Land plot in the Project by confirming their rights to GALT Project CORE Team and get a small ammount of GALT! More details - Contract AddNewPlot.

4. GALT Project CORE Team runs the CreateLandForSpaceAuction contract. With the help of it, the `Owner of the land`, which is the first to be sold to the `Project`, will be able to create all the SPACE tokens, which will then be auctioned in the `Land Auction`.

5. GALT Project CORE Team together with the First `Territory Owner` launches the `TerritoryCrowdsale` contract and begins the First  `Territory Crowdsdale`. GALT tokens will be issued for a pilot Territory Project managed using cryptography. This will be a place located in a good legal jurisdiction. See more details - TerritoryCrowdsale. All land plots for the `Land Auction` will be determined in advance according to the master plan.

6. While the First `Territory Crowdsdale` goes, everyone can send Ethers to the `TerritoryCrowdsale` contract. `Territory Crowdsdale`  will have a fundraising purpose in the Ethers. If the necessary fund-raising goal is achieved, the released GALT tokens will be distributed among the addresses listed by the Ethers. The resulting Ethers will be shared between the GALT Project CORE Team, the GALT Foundation and the current Territory Owner, who sells it to the Project. If the goal is not achieved, the released GALT tokens will be destroyed and the Ethers will be returned. See details - Contract GALTGenesis.

7. After the First `Territory Crowdsdale` is successfully completed, the GALT Project CORE Team will launch the SpaceAuction contract. The `Project participants` will be able to divide the `Territory` among themselves by auctioning land into separate `Land plots` within a large `Territory`. The main task is to honestly distribute specific `Land plots` between the owners of GALT tokens. Each `Land plot` is a token of ERC721 SPACE standard, which contains a `geohash` of a particular Land Plot (in fact, this is the exact address of the Land plot). If the Owner has won the site, then his GALT tokens, for which the site was won, are pledged to the Fund. See details - SpaceAuction contract.

