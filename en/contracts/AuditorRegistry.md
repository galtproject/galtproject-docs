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
  function pushAuditors() external onlyRole();
  function getAuditors() public view returns (address[]);
}
```

## External Roles
* `role_manager` - 
* `auditor_manager` - addresses allowed to add/remove auditors 
