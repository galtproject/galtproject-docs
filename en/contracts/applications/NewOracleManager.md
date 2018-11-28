# NewOracleManager contract

## Simple summary

In order to become an oracle the account should collect enough approvals from Arbitrators.

## Specification
Is [ArbitratorApprovableApplication](./ArbitratorApprovableApplication.md) application. Inherits all arbitrators intraction and reward claiming logic.

Payload example:

| Field | Example 
| --- | ---
| oracle address | 0x38703a11659A119b6666a6bfE9B11C60F8254f03
| oracle name | `Bob`
| oracle position | `MN`
| descriptionHashes | `QmYNQJoKGNHTpPxCBPh9KkDpaExgd2duMa3aF6ytMpHdao`, `QmeveuwF5wWBSgUXLG6p1oxF3GKkgjEnhA6AAwHUoVsx6E`, `QmSrPmbaUKA3ZodhzPWZnpFgcPMFWF4QsxXbkWfEptTBJd`
| oracleTypes | `PC_AUDITOR_ORACLE_TYPE`, `PC_CUSTODIAN_ORACLE_TYPE`

In case of approval it executes `Oracles.addOracle` function with the submitted data.

### Interface

````solidity

interface NewOracleManager is ArbitratorApprovableApplication {
    function initialize(ERC20 _galtToken, ArbitratorsMultiSig _arbitratorsMultiSig, address _galtSpaceRewardsAddress);

    // MODIFIERS

    // An applicant submits a new application, providing his name, a list of IPFS document hashses 
    // and a list of roles he applying for
    function submit(bytes32 _name, bytes32[] _documents, bytes32[] _roles);
    
    // This function will be executed in case of approval
    function _execute(bytes32 _id) internal;

    // GETTERS

    function getApplicationOracle(
        bytes32 _id
    )
        external
        view
        returns (
          address addr,
          bytes32 name,
          bytes32 position,
          bytes32[] descriptionHashes,
          bytes32[] oracleTypes
        );
}
````

