# Arbitrators contract

## Simple Summary
Temporary centralized Arbitrator Registry contract managed by `GaltCore` representative. In a mid term will be replaced with a more mature ERC721 holders voting system.

## Motivation
Space token holders should have a toolset to choose representative arbitrators. These arbitrators would operate ArbitratorsMultiSig and process
incoming claims in ClaimManager contract.

## Specification

```solidity
interface Arbitrators is Permissioned {

  string public constant ROLE_ARBITRATOR_MANAGER = "arbitrator_manager";

  struct Arbitrators {
    address addr;
    uint256 weight;
  }

  // Add a single arbitrator to the list
  function addAuditor(address _arbitrator, uint256 weight) external onlyRole(ROLE_ARBITRATOR_MANAGER);

  // Remove a single arbitrator from the list
  function removeAuditor(address _arbitrator) external onlyRole(ROLE_ARBITRATOR_MANAGER);
  
  // Set N and M values (see explanation below)
  function setNofM(uint256 n, uint256 m) external onlyRole(ROLE_ARBITRATOR_MANAGER);
  
  // Synchronize arbitrators list with ArbitratorsMultiSig and Validators contracts.
  // Also sets N and M values to ArbitratorsMultiSig contract
  function pushArbitrator() external onlyRole();
  
  // Getter for the sorted arbitrators list
  function getArbitrator() public view returns (address[] arbitrators, uint256[] weights);
}
```
* N - required minimum number of votes for `ArbitratorsMultiSig` contract (this value doesn't used inside the current contract).
* M - total arbitrators to be pushed into dependent contracts.

Arbitrator list stored as a sorted Red-Black tree.

Auditor weight change consist of two steps:
1. Remove current record using `#removeAuditor()` method
2. Insert a new record using `#addAuditor()` method

## Rationale
To store arbitrators list with associated weight values we use Set data type.

In order to push arbitrators list to another contracts, off-chain descending sorting required. Contract only verifies that provided input array is a valid descending sorted array.

## External Roles
* `role_manager` - addresses allowed modifying other roles
* `arbitrator_manager` - addresses allowed to add/remove arbitrators

## Owner
* no owner

## Upgradeability
New contract deployment by `CoreTeam` with roles reassigned in `ArbitratorsMultiSig` and `Validators` contracts.

## Initial setup
* `GaltCore` multisig address assigned as an only `role_manager`. In a long term this role permissions will be transferred to the community.
* `GaltCore` assigns their represenative multisig contract as an only `arbitrator_manager`
