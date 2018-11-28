# NewOracleManager contract

## Simple summary

In order to become an oracle the account should collect enough approvals from Arbitrators.

## Specification


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

