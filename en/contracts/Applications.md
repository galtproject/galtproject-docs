# Applications (Group of contracts)

## Simple Summary
A set of contracts for user interaction with internal registries.

## Specification

Simple flow of typical application contract:

* User submits some data
* Oracles (or arbitrators) lock their slot in a voting set in order to work on the application
* Oracles (or arbitrators) validates input (takes some time)
* Oracles (or arbitrators) perform one of the following actions:
    * Approve changes
    * Reject changes
    * Ask for more details
* Oracles (or arbitrators) withdraw their fees
* Galt Space withdraw their fees

In most cases application contracts are non-refundable.

## Permissions
| Permission | Location | Example | Initial holder | Planned holder
| --- | --- | --- | --- | ---
| minimal application fees ETH/GALT | Application contract | 2 ETH / 15 GALT | Galt Space | Oracles voting contract
| `galt space` share in fee | Application contract | `ETH: (Galt Space - 30% / Oracles - 70%)` <br />`GALT: (Galt Space - 13% / Oracles - 83%)` | Galt Space | Galt Space
| `oracle type` shares | Oracles contract | custodian - 30% <br> cadastral - 40% <br> appraiser - 30% | Galt Space | TBD
| `contract` upgrades | ... | ... | Galt Space | TBD

 ## Interface
 
 ````solidity

interface AbstractApplication is Permisisonable {

    function setGaltSpaceRewardsAddress(address _newAddress) external onlyRole(ROLE_FEE_MANAGER);
    function setPaymentMethod(PaymentMethod _newMethod) external onlyRole(ROLE_FEE_MANAGER);
    function setMinimalApplicationFeeInEth(uint256 _newFee) external onlyRole(ROLE_FEE_MANAGER);
    function setMinimalApplicationFeeInGalt(uint256 _newFee) external onlyRole(ROLE_FEE_MANAGER);
    function setGaltSpaceEthShare(uint256 _newShare) external onlyRole(ROLE_FEE_MANAGER);
    function setGaltSpaceGaltShare(uint256 _newShare) external onlyRole(ROLE_FEE_MANAGER);


    // After successful voting GaltSpace could withdraw their share of fee
    function claimGaltSpaceReward(bytes32 _applicationId) external onlyGaltSpaceCore;
    // After successful voting each oracle could withdraw his share of fee
    function claimOracleReward(bytes32 _applicationId) external onlyInvolvedOracle;
}
````