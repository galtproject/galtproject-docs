# ValidatorsStakesMultiSig

## Simple Summary

Gnosis MultiSigWallet fork with the owners list synchronizied from an external source. Options for add/remove owner proposal
are cutted off. Keeps stakes of all validators in the system.

## Golossary
* `Validator` - address who granted with validation permissions in application-like contracts depending on a roles list assigned to it.
* `Auditor` - validator with `CM_AUDITOR` role.

## Motivation
We need to collect stake deposits from validators who entitled to work within the system. If a user submits a claim for a compensation, auditors should punish corresponding validators and fulfill the claim using funds from culprits stakes.

## Specification
To improve security of this system, funds holding and accounting functionality is split into two separate contracts. `ValidatorsStakesMultiSig` contract is intended to store funds while `ValidatorStakes` performs stakes accounting. 

### Incoming funds
Although there are no restrictions on how funds can be transferred to this contracts, the default behaviour implies that the main source of incoming funds is stake deposits method of `ValidatorStakes` contract. This method creates required internal records about deposit value and immediately transfers it to the `ValidatorsStakesMultiSig` contract.
This contract is intended to operate only with GALT tokens. There is no way to manage such assets as ETH, ERC20, ERC721 and others, though there is no restrictions on accepting them.

### Funds claim fulfilment
The only way to transfer GALTS from this contract is using proposal-voting process. Transfer GALTS proposals could be created by any of participants.

## Code
The contract is a fork of Gnosis MultiSigWallet contract with cutted off `owners` self-management. The owners are managed in
external contract with role `owners_source` permission. This contract is granted with permissions to replace the `owners` list at any time.

### External Roles
Who should be granted with role management.
* `proposer` - addresses allowed create new GALT transfer proposals
* `owners_source` - addresses granted with `owners` list pushing permissions
