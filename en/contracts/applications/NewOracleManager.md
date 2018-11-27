# NewOracleManager contract

## Simple summary

In order to become an oracle the account should collect enough approvals from Arbitrators.

## Glossare

* M - required votes to eiter accept or reject an application
* N - total slots for arbitrators

## Specification

Any address could apply for being an oracle using `NewOracleManager` application. We don't perform checks is it a real user or
a contract.

Values M-of-N are copied from contract-level to a specific application at the moment of it's creation. If these
contract-level values are changed after an application was created, this application-level values won't be affected.

Any current arbitrator could lock working on application, if there are empty validators slots available. M - is a maximum arbitrators slots value. 

* AbstractApplication - toolset
### Interface

````solidity

interface NewOracleManager is AbstractApplication, Messagable {
    // An applicant submits a new application, providing his name, a list of IPFS document hashses 
    // and a list of roles he applying for
    function submit(bytes32 _name, bytes32[] _documents, bytes32[] _roles);

    // Any active arbitrator could lock an empty slot in voices stack if such one exists 
    function lock(bytes32 _applicationId) onlyArbitrator;
    // Any involved arbitrator who already has a slot in voices stack can unlock it, if he decide do not work
    // on the application
    function unlock(bytes32 _applicationId) onlyInvolvedArbitrator;

    // Any involved arbitrator could vote for the application approval
    function aye(bytes32 _applicationId) onlyInvolvedArbitrator;
    // Any involved arbitrator could vote for the application rejection
    function nay(bytes32 _applicationId) onlyInvolvedArbitrator;

    // After successful voting GaltSpace could withdraw their share of fee
    function claimGaltSpaceReward(bytes32 _applicationId) external onlyGaltSpaceCore;
    // After successful voting each arbitrator could withdraw his share of fee
    function claimOracleReward(bytes32 _applicationId) external onlyInvolvedArbitrator;
}
````

