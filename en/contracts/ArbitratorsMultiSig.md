# ArbitratorsMultiSig

## Simple Summary

Gnosis MultiSigWallet fork with the owners list synchronizied from an external source. Options for add/remove owner proposal
are cut off. Keeps stakes of all validators in the system.

## Glossary
* `Oracle` - address who granted with validation permissions in application-like contracts depending on a `oracle type` list assigned to it.
* `Arbitrator` - an `owner` from `ArbitratorsMultiSig` contract.

## Motivation
We need to collect stake deposits from oracles who entitled to work within the system. If a user submits a claim for a compensation, arbitrators should punish corresponding oracles and fulfill the claim using funds from culprits stakes.

## Specification
To improve security of this system, funds holding and accounting functionality is split into two separate contracts. `ArbitratorsMultiSig` contract is intended to store funds while `OracleStakesAccounting` performs stakes accounting. 

```solidity
interface ArbitratorsMultiSig is MultiSigWallet, Permissioned {
  string public constant ROLE_PROPOSER = "proposer";
  string public constant ROLE_ARBITRATOR_MANAGER = "arbitrator_manager";

  modifier forbidden {
    assert(false);
    _;
  }

  // Custom methods
  function setArbitrators(address[] auditors) external onlyRole('owner_source');
  function proposeTransaction(address destination, uint value, bytes data)
        public
        onlyRole('proposer')
        returns (uint transactionId);

  // MultiSigWallet modified methods
  function submitTransaction(address destination, uint value, bytes data)
        public
        returns (uint transactionId);
  function confirmTransaction(uint transactionId)
        public
        ownerExists(msg.sender)
        transactionExists(transactionId)
        notConfirmed(transactionId, msg.sender);
  function revokeConfirmation(uint transactionId)
        public
        ownerExists(msg.sender)
        confirmed(transactionId, msg.sender)
        notExecuted(transactionId);
  function executeTransaction(uint transactionId)
        public
        ownerExists(msg.sender)
        confirmed(transactionId, msg.sender)
        notExecuted(transactionId);
  function external_call(address destination, uint value, uint dataLength, bytes data)
        private
        returns (bool);
  function isConfirmed(uint transactionId)
        public
        constant
        returns (bool);
  function addTransaction(address destination, uint value, bytes data)
        internal
        notNull(destination)
        returns (uint transactionId);
  function getConfirmationCount(uint transactionId)
        public
        constant
        returns (uint count);
  function getTransactionCount(bool pending, bool executed)
        public
        constant
        returns (uint count);
  function getOwners()
        public
        constant
        returns (address[]);
  function getConfirmations(uint transactionId)
        public
        constant
        returns (address[] _confirmations);
  function getTransactionIds(uint from, uint to, bool pending, bool executed)
        public
        constant
        returns (uint[] _transactionIds);

  // Forbidden methods
  function MultiSigWallet(address[] _owners, uint _required) forbidden;
  function addOwner(address owner) forbidden;
  function removeOwner(address owner) forbidden;
  function replaceOwner(address owner, address newOwner) forbidden;
  function changeRequirement(uint _required) forbidden;
}
```

### Incoming funds
This contract is intended to operate mostly with GALT tokens. Although there are no restrictions on how funds can be transferred to this contracts, the default behaviour implies that the main source of incoming funds is stake deposits method of `OrackeStakesAccounting` contract. This method creates required internal records about deposit value and immediately transfers it to the `ArbitratorsMultiSig` contract.

### Funds claim fulfilment
The only way to transfer assets from this contract is using proposal-voting process. Transfer assets proposals could be created by `proposer` role.

### Code
The contract is a fork of Gnosis MultiSigWallet contract with cutted off `owners` self-management. The owners are managed in
external contract with role `owners_source` permission. This contract is granted with permissions to replace the `owners` list at any time.

### External Roles
* `role_manager` - address allowed managing all the roles whithin this contract
* `proposer` - addresses allowed create new GALT transfer proposals
* `arbitrator_manager` - addresses granted with `arbitrators` (owners) list pushing permissions

## Owner
* No owner

## Upgradeability
* No upgradeability

## Initial setup
* `GaltCore` multisig address assigned as an only `role_manager`. In a long term this role permissions will be transferred to the community.
* `ClaimManager` proxy contract address assigned as an only `proposer`
* `ArbitratorsVoting` contract address assigned as an only `arbitrator_manager`
