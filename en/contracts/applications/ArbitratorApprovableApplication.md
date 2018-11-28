# ArbitratorApprovableApplication

Abstract application for the simple cases when arbitrators should either approve or reject execution of given logic.

Descendant contract implements `_execute()` function which will be executed in the case of arbitrators approval.

## Glossary

* M - required votes to eiter accept or reject an application
* N - total slots for arbitrators

## Specification

Values M-of-N are copied from contract-level to a specific application at the moment of it's creation. If these
contract-level values are changed after an application was created, this application-level values won't be affected.

Any current arbitrator could lock working on application, if there are empty validators slots available. M - is a maximum arbitrators slots value.

Voting is available immediately after locking.

Arbitrators reward is shared by equal shares among all the arbitrators who managed to lock the application. It doesn't matter whether he has voted or not.

### Interface

````solidity

interface ArbitratorApprovableApplication is AbstractArbitratorApplication, Statusable {
    // Descendant contract notifies about a new application, providing an unique id and payment in GALT
    function submit(bytes32 _id, uint256 _applicationFeeInGalt) internal;

    // Any active arbitrator could lock an empty slot in voices stack if such one exists 
    function lock(bytes32 _applicationId) external onlyArbitrator;
    // Any involved arbitrator who already has a slot in voices stack can unlock it, if he decide do not work
    // on the application
    function unlock(bytes32 _applicationId) external onlyInvolvedArbitrator;

    // Any involved arbitrator could vote for the application approval
    function aye(bytes32 _applicationId) external onlyInvolvedArbitrator;
    // Any involved arbitrator could vote for the application rejection
    function nay(bytes32 _applicationId) external onlyInvolvedArbitrator;

    // After successful voting GaltSpace could withdraw their share of fee
    function claimGaltSpaceReward(bytes32 _applicationId) external onlyGaltSpaceCore;
    // After successful voting each arbitrator could withdraw his share of fee
    function claimArbitratorReward(bytes32 _applicationId) external onlyInvolvedArbitrator;
}
````
