Fund Basic improvements

FineMemberProposal
* Add both ETH and any ERC20 support. Use an additional `contract address` field in ERC20 case. 
* Deny space token withdrawal if the fines haven’t been paid yet.

PeriodicallyPaymentsProposals.
* FundStorage map contains all required data
* Accounted data is represented like
    * paymentId
        * Type (ETH/ERC20)
        * Contract Address (For ERC20)
        * member (address)
            * balance (int256)
            * periods
                * Id (uint256)
                * balance (int256)
* Period length in seconds can be specified only once at payment creation transaction and cannot be modified after.
* Decision required:
    * Do we need cache all member debts from all proposals in all currencies and all periods?


