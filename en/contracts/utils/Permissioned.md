# Permissioned.sol contract

## Simple Summary

An implementation of OpenZeppelin `Roles.sol` library with project-related helper methods.

## Rationale

There are multiple contracts within Galt Project which require roles functionality.
`Permissioned.sol` is a reusable set of methods to handle role management in contract.

We do not use `Owner` pattern to manage roles in order to keep `role_manager` straight enough and simple.

## Specification
### Utilities
* [Roles by OpenZeppelin v 2.0.0](https://github.com/OpenZeppelin/openzeppelin-solidity/blob/v2.0.0/contracts/access/Roles.sol)

````solidity
interface Permissioned {
    using Roles for Roles.Role;

    string public constant ROLE_MANAGER = "role_manager";

    modifier onlyRole(string _role) {
       require(has(role, account));
    }

    function hasRole(address _account, string _role) public returns (bool);
    function addRoleTo(address _account, string _role) external onlyRole(ROLE_MANAGER);
    function addRoleFrom(address _account, string _role) external onlyRole(ROLE_MANAGER);
}
````
