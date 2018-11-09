# AuditorRegistry

## Simple Summary
Naive TCR Auditors Registry contract managed by `GaltCore` representative. In a mid term will be replaced with a more mature ERC721 holders voting system.

## Motivation
Space token holders should have a toolset to choose representative auditors. These auditors would operate Validators MultiSig and process
incoming claims in ClaimManager contract.

## Specification
```solidity
interface AuditorsRegistry is RBAC {
  function addAuditor(address _auditor) external onlyRole(`auditor_manager`);
  function removeAuditor(address _auditor) external onlyRole(`auditor_manager`);
  function setAuditorWeight(address _auditor, uint256 weight) external onlyRole(`auditor_manager`);
  function setNofM(uint256 n, uint256 M) external onlyRole(`auditor_manager`);
  function pushAuditors() external onlyRole();
  function getAuditors() public view returns (address[]);
}
```

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
