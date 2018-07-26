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

8. GALT Project CORE Team together with the contract SpaceAuction launches the following contracts: Reputation, Controller, MultiSig, MultiSigProposal, FundRegistry, DelegateCandidateAuction, DelegateVoting, Emission:
- Pledged GALT tokens become a `Land Owner's` `Reputation`. This `Reputation`, he can distribute between different `Funds`. Together with the Reputation between the Funds, Ethers pass (if they exist in the Fund) and GALT Tokens, pledged for Land Plots. See more details - Reputation Contract.
- The `Land Owners` has a `Reputation` in each Fund to elect `Delegates`. Seven "Candidates in Delegates" with the largest number of votes become "Delegates" and are given the right to dispose of the "Fund" Ethers (if they are in the "Fund") and other ERC20 tokens of the Fund and receive remuneration for this. See details - DelegateVoting contract.
- Anyone can get the right to become a "Candidate for Delegates" at the Delegates' Auction. See details - DelegateCandidateAuction contract.
- Anyone can create a `Adjacent Fund`, any `Land Owner` can transfer there part of his `Reputation` and `Ethers` (if they are in the Fund) / GALT, which are at the `Fund`. See more details - Contract FundRegistry.
- Selected `Delegates` can create `Proposals` for the withdrawal of Ethers (if they exist in the Fund) and GALT from the `Fund`, and approve these applications. See details - MultiSigProposal Contract, MultiSig Contract.
- `Delegates` can create ballots for the need to raise funds for the `Fund`. If the application is accepted, the `Land Owners` will be required to replenish the `Fund` or receive a `Reputation` Fine. See more details - FundEthReplenish contract.
- GALT Project CORE Team launches the `Emission` contract. The `GALT Emission Auction` begins. Auction issues new GALTs and distributes them among those who have listed the ethers and the Land Owners. See more details - Emission contract.

9. GALT Project CORE Team launches ManagementFee contract. `Delegates` begin to receive remuneration based on the balance of the Ethers in the Fund and increasing their number. See the ManagementFee contract for details.

10. GALT Project CORE Team runs the HeightManagement contract. Land Owners will be able to determine by voting the upper and lower boundaries of the Land plots, buying each other's space over the Land plots. See the HeightManagement contract for details.

11. GALT Project CORE Team launches the ReputationFine contract. `Land Owners` will be able to vote and impose reputation fines on each other. `Land Owners` can replenish their `Reputation` with GALT tokens. See more details - ReputationFine contract.

12. GALT Project CORE Team launches the PropertyVerification contract. `Land Owners` will be able to confirm their right to own specific sites on GPS coordinates. See more details - the PropertyVerification contract.

13. GALT Project CORE Team launches SmartSpace-SharedSpace contracts for joint ownership of Land Plots and SmartSpace-Rental for individual and joint lease of Land Plots. See details - SmartSpace-SharedSpace contract and SmartSpace-Rental.

14. GALT Project CORE Team launches the GaltExit contract. `Project participants` who own GALT will be able to automatically exchange GALT for Ethers from the `Funds`. See details - GaltExit contract.

15. GALT Project CORE Team runs the CreateTerritory contract. Anyone can suggest to enter into the `Project` a new large piece of land (we call it the `Territory`). In this `Territory`, as may be the `Owner`, so it may not be due to any legal conflicts. When creating an order, you specify a specific set of parameters. The `Project participants` can vote for the application and create a new mint of GALT tokens for this land. See more details - CreateTerritory contract.

16. If the `Project participants` voted for the application and decided to enter a new land in the project and issue GALT tokens - the new `Territory Crowdsdale` starts. Anyone can buy GALT tokens for Ethers. If the necessary fund-raising goal is achieved, the released GALT tokens will be distributed among the addresses listed by the Ethers. The received Ethers will in general be divided between the one who created the application for entering new land in the project, the current Owner of the land that sells it to the `Project` and the `Fund` that will manage this territory. See more details - Contract GALTGenesis. At the same time, an unlimited number of `Territory Crowdsdale` can pass.

17. GALT Project CORE Team gives the right to own Smart Contracts to the Community.

18. The new Territory - Bir Tawil will be introduced into the Project and the Fund will be raised for its development and for creation of new type of Society.

