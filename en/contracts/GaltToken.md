# Galt Token
For `Terms` - [Glossary](https://github.com/andromedaspace/galtproject-docs/blob/master/en/Glossary.md).
## Problem Description
The `Project` needs an ERC20 contract and a `Token` to account for the investments of `Project participants` in the `Funds` that will develop the `Territory` and the equivalent of a digital right to all `Project Territories` without the right to specific `Land Plots`. The closest analogue is the land share.

## Contract goals
- the GALT `Token` allows to take into account the contribution of each `Project Participant` to the `Project Funds`;
- the GALT `Token` allows to provide liquidity of `Funds`. This means that all `Project Funds` at any time are required to automatically redeem GALT tokens from their owners;
- the GALT `Token` allows to determine by auction the true true of the `Land Plots`;
- the GALT `Token` allows to automatically transfer Ethers between `Project Funds`;
- the GALT `Token` is the equivalent of a share in all `Project Funds` and in all `Project Territories`;

## Contract Specification
- Token name (name) - `GALT Token`;
- Token symbol (symbol) - `GALT`;
- Number of decimal places (decimals) - `18`;
- Max. the possible number of minted Tokens - `2 ^ 256 / 1e18 = 1.1579209e + 59`;

The contract uses the implementation of the [OpenZeppelin Mintable ERC20](https://github.com/OpenZeppelin/openzeppelin-solidity/tree/master/contracts/token/ERC20) standard. The contract uses the implementation of the [BurnableToken](https://github.com/OpenZeppelin/openzeppelin-solidity/blob/master/contracts/token/ERC20/BurnableToken.sol) standard.

### Methods

| Method | Right to call |
| ------ | ------------- |
| mint () | Contract GaltGenesisRegistry |
| burn () | Contract GaltGenesisRegistry |
| transfer () ||
| approve () ||
| transferFrom () ||

## Implementation features on Solidity
### Contract Owner
GALT Project CORE Team. Later, ownership of the contract will be transferred to the Community.
### Upgradeability.
None.
### Who starts the contract.
GALT Project CORE Team.
## Features.
None.
## Ambiguous questions and answers to them.
None.
