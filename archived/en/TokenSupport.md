# Token support

* `+`	- implemented
* `-` -	to be implemented
* ` ` - no support (empty cell)

## GALT Protocol Fees

| Service| Action | ETH| 	GALT (ERC20)| 	Any ERC20 |
| -- | -- | -- | -- | -- |
| @fund-basic/FundFactory	| Create a new fund fee	| - / 100%	| + / 100%	| 
| @core/MultiSigFactory	| Create a new multiSig fee	| - / 100%	| + / 100%	| 
| @core/SpaceLockerFactory	| Create a new locker fee	| - / 100%	| + / 100%	| 
| @core/GaltLockerFactory	| Create a new locker fee	| - / 100%	| + / 100%	| 
| @core/Applications	| Application submission fee	| + / custom	| + / custom	| 
| @market/PlotEscrow	| Application submission fee	| + / custom	| + / custom	| 
				
				
				
## Token support in contracts

| Contract	| Purpose	| ETH	| GALT (ERC20)	| Any ERC20 |
| -- | -- | -- | -- | -- |
| @core/ClaimManager	| Amount claimed by an applicant	| 		| + | | 
| @core/ClaimManager	| Oracle/Arbitrator fee proposed by an arbitrator		| 	| +| | 
| @core/OracleStakeAccounting	| Currency for oracle stakes	| 		| +| | 
| @core/ArbitratorStakeAccounting	| Currency for arbitrator stakes | 	|+ | | 
| @market/PlotEscrow	| Escrow currency	| +	| +	| + | 
| @fund-basic/FineMemberProposalManager	| Fee currency	| +	| +	| + |
| @fund-basic/RegularFee | Fee currency | +	| +	| + |
