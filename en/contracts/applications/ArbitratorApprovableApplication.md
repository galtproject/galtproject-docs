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
    // Descendant contract initialization
    function _initialize(
        ERC20 _galtToken,
        ArbitratorsMultiSig _arbitratorsMultiSig,
        address _galtSpaceRewardsAddress
      )
        internal;

    // Descendant contract notifies about a new application, providing an unique id and payment in GALT
    function _submit(bytes32 _id, uint256 _applicationFeeInGalt) internal;

    // Any active arbitrator could lock an empty slot in voices stack if such one exists 
    function lock(bytes32 _applicationId) external onlyArbitrator;
    // Any involved arbitrator who already has a slot in voices stack can unlock it, if he decide do not work
    // on the application
    function unlock(bytes32 _applicationId) external onlyInvolvedArbitrator;
    // Any active arbitrator could lock an already locked slot, which was previously locked by another
    // arbitrator and this arbitrator were expelled from ArbitratorsMultiSig
    function lockSlot(bytes32 _applicationId, address _expelledArbitrator) external onlyArbitrator;

    // Any involved arbitrator could vote for the application approval
    function aye(bytes32 _applicationId) external onlyInvolvedArbitrator;
    // Any involved arbitrator could vote for the application rejection
    function nay(bytes32 _applicationId) external onlyInvolvedArbitrator;

    // After successful voting GaltSpace could withdraw their share of fee
    function claimGaltSpaceReward(bytes32 _applicationId) external onlyGaltSpaceCore;
    // After successful voting each arbitrator could withdraw his share of fee
    function claimArbitratorReward(bytes32 _applicationId) external onlyInvolvedArbitrator;
    
    // GETTERS
    
    function getApplicationById(
        bytes32 _id
      )
        external
        view
        returns (
          ApplicationStatus status,
          address applicant,
          address[] arbitrators,
          uint256 m,
          uint256 n,
          uint256 ayeCount,
          uint256 nayCount
        );

    function getApplicationFees(
        bytes32 _id
      )
        external
        view
        returns (
          Currency currency,
          uint256 arbitratorsReward,
          uint256 galtSpaceReward,
          bool galtSpaceRewardPaidOut
        );
}
````

### Methods
#### Inheritance
* AbstractArbitratorApplication
* Statusable

#### GALT_SPACE role metods
##### #setMofN()
Set values for required and total available slots correspondingly.

* M - required votes to make an application being accepted
* N - total slots available for arbitrators
* M should be greater or equal to 2
* N should be greater or equal to M

#### #lock()
Any active arbitrator locks an application if an empty slots available

* Requires SUBMITTED status
* There should be at least one empty slot available for an arbitrator

#### #unlock() - (not imlemented yet)
Any involved arbitrator who already has a slot in voices stack can unlock it, if he decide to not work on the application

* Requires SUBMITTED status
* Sender should be an active validator which has already locked the application

#### #lockSlot() - (not imlemented yet)
Any active arbitrator locks the slot which was left after an expelled arbitrator

* Requires SUBMITTED status
* Previous arbitrator shouldn't be in the multisig owners list, but should be in the application arbitrators list

#### #aye()
Any active arbitrator votes `aye`

* Should not wait for all slots being locked
* Requires SUBMITTED status
* Requireds arbitrator not voted `aye` yet
* If the arbitrator has already voted `nay`, `nayCount` decrements
* If `ayeCount` reaches the threshold `M`:
    * the application status changes to `APPROVED`
    * `_execute()` function of the descendant is called

#### #nay()
Any active arbitrator votes `nay`

* Should not wait for all slots being locked
* Requires SUBMITTED status
* Requireds arbitrator not voted `nay` yet
* If the arbitrator has already voted `aye`, `ayeCount` decrements
* If `nayCount` reaches the threshold `M`, the application status changes to `REJECTED`

