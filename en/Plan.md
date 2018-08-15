# General GALT Project development plan.

Special terms in the text begin with a capital letter or like `this`. To understand the terms - [Glossary](https://github.com/andromedaspace/galtproject-docs/blob/master/eng/Glossary.md).

The basis of the `Project` is the Token standard ERC20 GALT and Token standard ERC721 SPACE. The GALT Token is the right to share or dispose of land and the equivalent of a share in an investment  `Fund` that is engaged in the development of the `Territory`, the SPACE token - the right to a specific Land with specific boundaries. These rights are determined by the smart contracts of the `Project`. See more details - GaltToken contract, SpaceToken contract.

The procedure for the Galt Core to launch the `Project`:

1. GALT Project CORE Team runs on its own behalf the contract GaltToken and SpaceToken.  See more details - GaltToken contract, SpaceToken contract.

2. GALT Project CORE Team launches the SplitMerge contract. See the SplitMerge contract for details.

3. GALT Project CORE Team launches `PlotManager` contract. Now everyone can register their `Land plot` in the `Project` by confirming their rights to GALT CORE or it's partners! Together with the contract, a service will be launched that will allow anyone with minimal effort to include their `Land PLot` in the `Project`. One of these `Land Plots` will be sold to the `Project`, as` Territory`. More details - Contract PlotManager.

4. Galt Core launches the GaltDEX contract. This is an automatic exchanger GALT for ETH and back. The rate will be calculated automatically based on the number of Ethers on the contract and the total number of GALTs issued.

5. Galt Core launches the PlotEscrow contract. With the help of this contract, anyone can sell his land plot for Tokens with all the necessary legal formalities.

6. GALT Project CORE Team runs the SPACEAuctionRegistry contract and GaltGenesisRegistry contract.

7. GALT Project CORE Team together with the First `Territory Owner` launches the `LandCrowdsaleManager` and `TerritoryCrowdsale` contract and begins the First `Territory Crowdsdale`. GALT tokens will be issued for a pilot `Territory`, managed by cryptography. This will be a place located in a good legal jurisdiction. See more details - TerritoryCrowdsale and `LandCrowdsaleManager`. All land plots for the `Land Auction` will be determined in advance according to the master plan.

8. While the First `Territory Crowdsdale` goes, everyone can send Ethers to the `TerritoryCrowdsale` contract. `Territory Crowdsdale`  will have a fundraising purpose in the Ethers. If the necessary fund-raising goal is achieved, the released GALT tokens will be distributed among the addresses listed by the Ethers. The resulting Ethers will be shared between the GALT Project CORE Team, the GALT Foundation and the current Territory Owner, who sells it to the Project. If the goal is not achieved, the released GALT tokens will be destroyed and the Ethers will be returned. See details - Contract TerritoryCrowdsale.

9. After the First `Territory Crowdsdale` is successfully completed, the GALT CORE will launch the SpaceAuction contract. The `Project participants` will be able to divide the `Territory` among themselves by auctioning land into separate `Land plots` within a large `Territory`. The main task is to honestly distribute specific `Land plots` between the owners of GALT tokens. Each `Land plot` is a token of ERC721 SPACE standard, which contains a `geohash` of a particular Land Plot (in fact, this is the exact address of the Land plot). If the Owner has won the site, then his GALT tokens, for which the site was won, are pledged to the Fund. See details - SpaceAuction contract.

10. GALT Project CORE Team together with the contract SpaceAuction launches the following contracts: Reputation, Controller, MultiSig, MultiSigProposal, FundRegistry, DelegateCandidateAuction, DelegateVoting, Emission:
- Pledged GALT tokens become a `Land Owner's` `Reputation`. This `Reputation`, he can distribute between different `Funds`. Together with the Reputation between the Funds, Ethers pass (if they exist in the Fund) and GALT Tokens, pledged for Land Plots. See more details - Reputation Contract.
- The `Land Owners` has a `Reputation` in each Fund to elect `Delegates`. Seven "Candidates in Delegates" with the largest number of votes become "Delegates" and are given the right to dispose of the "Fund" Ethers (if they are in the "Fund") and other ERC20 tokens of the Fund and receive remuneration for this. See details - DelegateVoting contract.
- Anyone can get the right to become a "Candidate for Delegates" at the Delegates' Auction. See details - DelegateCandidateAuction contract.
- Anyone can create a `Adjacent Fund`, any `Land Owner` can transfer there part of his `Reputation` and `Ethers` (if they are in the Fund) / GALT, which are at the `Fund`. See more details - Contract FundRegistry.
- Selected `Delegates` can create `Proposals` for the withdrawal of Ethers (if they exist in the Fund) and GALT from the `Fund`, and approve these applications. See details - MultiSigProposal Contract, MultiSig Contract.
- `Delegates` can create ballots for the need to raise funds for the `Fund`. If the application is accepted, the `Land Owners` will be required to replenish the `Fund` or receive a `Reputation` Fine. See more details - FundEthReplenish contract.
- GALT Project CORE Team launches the `Emission` contract. The `GALT Emission Auction` begins. Auction issues new GALTs and distributes them among those who have listed the ethers and the Land Owners. See more details - Emission contract.

11. GALT Project CORE Team launches ManagementFee contract. `Delegates` begin to receive remuneration based on the balance of the Ethers in the Fund and increasing their number. See the ManagementFee contract for details.

12. GALT Project CORE Team runs the HeightManagement contract. Land Owners will be able to determine by voting the upper and lower boundaries of the Land plots, buying each other's space over the Land plots. See the HeightManagement contract for details.

13. GALT Project CORE Team launches the ReputationFine contract. `Land Owners` will be able to vote and impose reputation fines on each other. `Land Owners` can replenish their `Reputation` with GALT tokens. See more details - ReputationFine contract.

14. GALT Project CORE Team launches the PropertyVerification contract. `Land Owners` will be able to confirm their right to own specific sites on GPS coordinates. See more details - the PropertyVerification contract.

15. GALT Project CORE Team launches SmartSpace-SharedSpace contracts for joint ownership of Land Plots and SmartSpace-Rental for individual and joint lease of Land Plots. See details - SmartSpace-SharedSpace contract and SmartSpace-Rental.

16. GALT Project CORE Team launches the GaltExit contract. `Project participants` who own GALT will be able to automatically exchange GALT for Ethers from the `Funds`. See details - GaltExit contract.

17. GALT Project CORE Team gives the right to own Smart Contracts to the Community.

18. The new Territory - Bir Tawil will be introduced into the Project and the Fund will be raised for its development.

