# AuditorRegistry

## Simple Summary
Naive TCR Auditors Registry contract managed by `GaltCore` representative. In a mid term will be replaced with a more mature ERC721 holders voting system.

## Motivation
Space token holders should have a toolset to choose representative auditors. These auditors would operate Validators MultiSig and process
incoming claims in ClaimManager contract.

## Specification

```solidity
interface AuditorsRegistry is RBAC {
  struct Auditor {
    address addr;
    uint256 weight;
  }

  // Add a single auditor to the list
  function addAuditor(address _auditor, uint256 weight) external onlyRole(`auditor_manager`);

  // Remove a single auditor from the list
  function removeAuditor(address _auditor) external onlyRole(`auditor_manager`);
  
  // Set N and M values (see explanation below)
  function setNofM(uint256 n, uint256 m) external onlyRole(`auditor_manager`);
  
  // Synchronize auditors list with ValidatorStakeMultiSig and Validators contracts.
  // Also sets N and M values to ValidatorStakeMultiSig contract
  function pushAuditors() external onlyRole();
  
  // Getter for the sorted auditors list
  function getAuditors() public view returns (address[] auditors, uint256[] weights);

  // Add RBAC role
  function addRoleTo(address _operator, string _role) external onlyRole(`role_manager`);

  // Remove RBAC role
  function removeRoleFrom(address _operator, string _role) external onlyRole(`role_manager`);
}
```
* N - required minimum number of votes for `ValidatorStakeMultiSig` contract (this value doesn't used inside the current contract).
* M - total auditors to be pushed into dependend contracts.

Auditors list stored as a sorted Red-Black tree.

Auditor weight change consist of two steps:
1. Remove current record using `#removeAuditor()` method
2. Insert a new record using `#addAuditor()` method

## Rationale
Red-Black tree provides O(logn) insert/search complexity.

## External Roles
* `role_manager` - addresses allowed modifying other roles
* `auditor_manager` - addresses allowed to add/remove auditors 

## Owner
* no owner

## Upgradeability
New contract deployment by `CoreTeam` with roles reassigned in `ValidatorStakesMultiSig` and `Validators` contracts.

## Initial setup
* `GaltCore` multisig address assigned as an only `role_manager`. In a long term this role permissions will be transferred to the community.
* `GaltCore` assigns their represenative multisig contract as an only `auditor_manager`
